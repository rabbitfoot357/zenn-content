---
title: "4. GPU / Local backend"
emoji: "🛠️"
type: "tech"
topics: ["iris", "local-llm"]
published: false
---

# 4. GPU / Local backend

## 現状

- **ハードウェア**: Windows PC、RTX 5070 Ti 16GB [ev-001]
- **Backend**: Ollama (localhost API) [ev-001]
- **競合プロセス**: LM Studioは既知の競合プロセスとして検出対象だが、起動役ではない [ev-001]
- **Bionic**: 非Codex固定system prompt入口であり、`context_assembler.py`をSKILL経由で利用する別の入口 [ev-001]

## モデル構成

- **現在使用中の標準モデル**: `hf.co/unsloth/Qwen3.8-27B-GGUF:UD-Q3_K_XL` (`DEFAULT_MODEL`/`WORKER_MODELS`) [ev-001]
- **Gate/軽量モデル**: `qwen3.5:9b-q8_0` (Worker本体からは選択不可) [ev-001]
- **手動比較専用**: `qwen3.8-27b:latest` (Q4) [ev-001]
- **除外対象**: `gpt-oss:20b` (Structured Output benchmark失敗のため) [ev-001]

## 実装・検証状態

- **GPU Preflight/Calibration**: `ollama_preflight()` 等の関数が実装済みであり、無効化されていない [ev-001]
- **VRAM Headroom**: `DEFAULT_GPU_HEADROOM_MIB = 1024` が設定されている [ev-001]
- **Real E2Eでの挙動**: 2026-09-17の実E2E 3 taskは全て `vram.capacity = REUSED_LOADED_MODEL` であり、既にロード済みのモデルを再利用した [ev-001]
- **未検証経路**: 新規ロード時のGPU容量チェック分岐は今回のE2Eでは経由しておらず、コード・単体テストのみで裏付けられている [ev-001]

## 安全策

- **競合処理**: 他のローカル推論プロセス（LM Studio等）との同時ロードによる16GB GPU競合に対し、事前チェックで `BLOCKED` にするだけでプロセスを終了させない設計となっている [ev-001]
- **禁止事項**: 自動killや強制解放は行わない [ev-001]
