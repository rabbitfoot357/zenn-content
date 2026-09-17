---
title: "Model selection"
emoji: "🛠️"
type: "tech"
topics: ["iris", "local-llm"]
published: false
---

状況: Model selection / 問題: - Standard: `hf.co/unsloth/Qwen3.8-27B-GGUF:UD-Q3_K_XL` - Standard context: 8192 tokens; thinking disabled - Direct/Gate lightweight model: `qwen3.5:9b-q8_0` (not selectable by Worker) - Manual rollback/comparison only: `qwen3.8-27b:latest` (Q4) - Excluded: `gpt-oss:20b` (Structured Output benchmark

## 記録された内容 [ev-001]

> Model selection
> 
> - Standard: `hf.co/unsloth/Qwen3.8-27B-GGUF:UD-Q3_K_XL`
> - Standard context: 8192 tokens; thinking disabled
> - Direct/Gate lightweight model: `qwen3.5:9b-q8_0` (not selectable by Worker)
> - Manual rollback/comparison only: `qwen3.8-27b:latest` (Q4)
> - Excluded: `gpt-oss:20b` (Structured Output benchmark failure)
> 
> The standard Q3 model was selected on the Windows RTX 5070 Ti 16 GB host
> after it remained 100% GPU-resident and completed structured-output,
> tool-calling, Safety-boundary, and Local Worker end-to-end checks. Model
> selection never permits an automatic fallback; an unavailable selected model
> fails closed during preflight.
> 
> The 2026-08-26 production pilot found the 9B mod
