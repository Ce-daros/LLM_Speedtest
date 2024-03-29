# LLM 速度测试 - 7B 单卡

使用模型 `Mistral-7B-Instruct-v0.2`

# 测试平台

使用 [AutoDL](www.autodl.com) 算力租赁平台完成测试。

- Ubuntu 22.04
- PyTorch 2.1.0
- Python 3.11
- Cuda  12.1
- RTX 4090D(24GB) * 1
- 18 vCPU AMD EPYC 9754 128-Core Processor
- 60GB RAM
- [Text Generation Webui](https://github.com/oobabooga/text-generation-webui)

# 测试方法

- 零上下文时生成 1024 Tokens（禁用 EOS）
- 生成五轮取平均值
- 第一次生成前会进行 256 Tokens 的 Warm-up，记录热身前后显存变化

# 测试数据
## Huggingface

```
Output generated in 26.33 seconds (38.86 tokens/s, 1023 tokens, context 1, seed 617610237)
Output generated in 26.45 seconds (38.68 tokens/s, 1023 tokens, context 1, seed 1146711074)
Output generated in 27.49 seconds (37.22 tokens/s, 1023 tokens, context 1, seed 808441977)
Output generated in 26.98 seconds (37.91 tokens/s, 1023 tokens, context 1, seed 546701839)
Output generated in 28.41 seconds (36.01 tokens/s, 1023 tokens, context 1, seed 633613868)
```

Average: `37.736 tokens/s`

- 加载后：`14934 MiB`
- 1024tokens 推理后：`15030 MiB`

## Huggingface (load in 8bit)

```
Output generated in 171.38 seconds (5.97 tokens/s, 1023 tokens, context 1, seed 169177818)
Output generated in 168.86 seconds (6.06 tokens/s, 1023 tokens, context 1, seed 728468976)
Output generated in 169.23 seconds (6.05 tokens/s, 1023 tokens, context 1, seed 574677743)
Output generated in 169.17 seconds (6.05 tokens/s, 1023 tokens, context 1, seed 663738095)
Output generated in 169.73 seconds (6.03 tokens/s, 1023 tokens, context 1, seed 271133181)
```

Average: `6.0332 tokens/s`

- 加载后：`8226 MiB`
- 1024tokens 推理后：`8380 MiB`

## GPTQ on Exllamav2

`4Bit 32g`

```
Output generated in 14.35 seconds (71.28 tokens/s, 1023 tokens, context 1, seed 1927052726)
Output generated in 13.66 seconds (74.88 tokens/s, 1023 tokens, context 1, seed 1537564846)
Output generated in 12.85 seconds (79.61 tokens/s, 1023 tokens, context 1, seed 1613982529)
Output generated in 12.84 seconds (79.65 tokens/s, 1023 tokens, context 1, seed 506971385)
Output generated in 12.22 seconds (83.69 tokens/s, 1023 tokens, context 1, seed 119487648)
```

Average: `77.822 tokens/s`

- 加载后：`8958 MiB`
- 1024tokens 推理后：`8974 MiB`
- 
## GPTQ on Exllamav2 (8bit KV Cache)

```
Output generated in 11.79 seconds (86.78 tokens/s, 1023 tokens, context 1, seed 581459717)
Output generated in 13.90 seconds (73.58 tokens/s, 1023 tokens, context 1, seed 62230853)
Output generated in 20.36 seconds (50.24 tokens/s, 1023 tokens, context 1, seed 719660271)
Output generated in 17.54 seconds (58.32 tokens/s, 1023 tokens, context 1, seed 139476270)
Output generated in 14.09 seconds (72.58 tokens/s, 1023 tokens, context 1, seed 1156097764)
```

Average: `68.3 tokens/s`

- 加载后：`7002 MiB`
- 1024tokens 推理后：`7022 MiB`

## GPTQ on Exllamav2 (4bit KV Cache)

```
Output generated in 13.49 seconds (75.81 tokens/s, 1023 tokens, context 1, seed 1207276021)
Output generated in 12.68 seconds (80.70 tokens/s, 1023 tokens, context 1, seed 1729089823)
Output generated in 13.45 seconds (76.06 tokens/s, 1023 tokens, context 1, seed 918959937)
Output generated in 14.10 seconds (72.54 tokens/s, 1023 tokens, context 1, seed 1506801699)
Output generated in 12.81 seconds (79.89 tokens/s, 1023 tokens, context 1, seed 246510078)
```

Average: `77 tokens/s`

- 加载后：`6110 MiB`
- 1024tokens 推理后：`6112 MiB`

## AWQ

`fused_attention` enabled

```
Output generated in 18.35 seconds (55.76 tokens/s, 1023 tokens, context 1, seed 1625920179)
Output generated in 18.38 seconds (55.65 tokens/s, 1023 tokens, context 1, seed 147075351)
Output generated in 18.97 seconds (53.94 tokens/s, 1023 tokens, context 1, seed 1370149021)
Output generated in 19.06 seconds (53.68 tokens/s, 1023 tokens, context 1, seed 319849706)
Output generated in 18.26 seconds (56.03 tokens/s, 1023 tokens, context 1, seed 200310089)
```

Average: `55.012 tokens/s`

- 加载后：`10388 MiB`
- 1024tokens 推理后：`9672 MiB`

## GGUF Q4_K_M

```
Output generated in 17.06 seconds (59.92 tokens/s, 1024 tokens, context 1, seed 689169851)
Output generated in 18.38 seconds (55.71 tokens/s, 1024 tokens, context 1, seed 236387285)
Output generated in 16.57 seconds (61.68 tokens/s, 1022 tokens, context 1, seed 1253491230)
Output generated in 18.53 seconds (55.25 tokens/s, 1024 tokens, context 1, seed 283396031)

```

Average: `58.14 tokens/s`

- 加载后：`10564 MiB`
- 1024tokens 推理后：`10707 MiB`