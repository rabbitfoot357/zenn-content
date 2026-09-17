---
title: "4. GPU / Local backend"
emoji: "🛠️"
type: "tech"
topics: ["iris", "local-llm"]
published: false
---

状況: 4. GPU / Local backend / 問題: - ハードウェア: Windows PC、RTX 5070 Ti 16GB(`docs/overnight_worker_v0.1.md`)。 - backend: Ollama(localhost API)。LM Studioは既知の競合プロセスとして検出対象(起動役ではない)。 Bionicは非Codex固定system prompt入口で、`context_assembler.py`をSKILL経由で使う別の入口(§Architecture文書§7参照)。 - **現在使用中のmodel**: `hf.co/unsloth/Qwen3.8-27B-GGUF:UD-Q3_K_XL`(標準、

## 記録された内容 [ev-001]

> GPU / Local backend - ハードウェア: Windows PC、RTX 5070 Ti 16GB(`docs/overnight_worker_v0.1.md`)。 - backend: Ollama(localhost API)。LM Studioは既知の競合プロセスとして検出対象(起動役ではない)。 Bionicは非Codex固定system prompt入口で、`context_assembler.py`をSKILL経由で使う別の入口(§Architecture文書§7参照)。 - **現在使用中のmodel**: `hf.co/unsloth/Qwen3.8-27B-GGUF:UD-Q3_K_XL`(標準、`DEFAULT_MODEL`/`WORKER_MODELS`)。 実E2E(§1)の全task JSONで`local_model`値として実際に記録されている。 - Gate/軽量model: `qwen3.5:9b-q8_0`(Worker本体からは選択不可)。手動比較専用: `qwen3.8-27b:latest`(Q4)。 除外: `gpt-oss:20b`(Structured Output benchmark失敗)。 - GPU preflight/calibration: `ollama_preflight()`/`gpu_capacity_diagnostics()`/`gpu_capacity_reason()`/ `attempt_gpu_calibration()`(`80_local_scripts/overnight_wo
