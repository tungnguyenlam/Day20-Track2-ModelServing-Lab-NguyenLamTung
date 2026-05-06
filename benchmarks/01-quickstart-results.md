# 01 — Quickstart Results

Settings: `n_threads=16`, `n_ctx=2048`, `n_batch=512`, `n_gpu_layers=99`.

| Model | Load (ms) | TTFT P50/P95 (ms) | TPOT P50/P95 (ms) | E2E P50/P95/P99 (ms) | Decode rate (tok/s) |
|---|---:|---:|---:|---:|---:|
| Qwen3.5-0.8B-Q4_K_M.gguf | 713 | 86 / 156 | 16.9 / 23.7 | 1132 / 1638 / 1748 | 59.4 |
| Qwen3.5-0.8B-Q4_K_M.gguf | 498 | 70 / 453 | 16.8 / 20.9 | 1193 / 1580 / 1688 | 59.6 |

## Observations

- TTFT is the prefill cost. With short prompts this is small; with long prompts it dominates.
- TPOT is per-token decode latency. The decode rate is `1000 / TPOT_p50`.
- The bigger quantization (Q4_K_M) is usually only ~30–60% slower than Q2_K but produces noticeably better text. Q2_K is for *truly* tight RAM.
- `n_threads = physical_cores` is usually best on CPU. Hyperthreading (`logical_cores`) often hurts because the work is bandwidth-bound.

(Edit this file with your own observations before submitting.)
