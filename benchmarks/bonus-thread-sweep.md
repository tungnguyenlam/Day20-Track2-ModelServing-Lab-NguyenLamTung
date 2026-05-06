# Bonus — Thread sweep

Model: `Qwen3.5-0.8B-Q4_K_M.gguf`  ·  GPU layers: `99`

| threads | tg128 (tok/s) |
|---:|---:|
| 1 | 31.7 |
| 2 | 46.6 |
| 8 | 51.9 |
| 16 | 32.2 |
| 32 | 20.2 |

**Best**: `-t 8` at 51.9 tok/s.

Look at the curve. If it peaks around your **physical** core count and drops as you go higher, that's the memory-bandwidth ceiling: extra threads fight over the same memory channels and slow each other down.
