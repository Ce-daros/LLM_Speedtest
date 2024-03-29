# LLM 速度测试 - 多卡

使用模型 `Yi-34B-Chat`
机器配置 `4*2080 ti`

# 测试方法

- 零上下文时生成 512 Tokens（禁用 EOS）
- 生成五轮取平均值
- 第一次生成前会进行 256 Tokens 的 Warm-up，记录热身前后显存变化

# GGUF-不开启 row split

```
llama_print_timings:        load time =     938.23 ms
llama_print_timings:      sample time =    1219.87 ms /   511 runs   (    2.39 ms per token,   418.90 tokens per second)
llama_print_timings: prompt eval time =       0.00 ms /     1 tokens (    0.00 ms per token,      inf tokens per second)
llama_print_timings:        eval time =   62383.93 ms /   511 runs   (  122.08 ms per token,     8.19 tokens per second)
llama_print_timings:       total time =   66174.49 ms /   512 tokens
Output generated in 66.76 seconds (7.67 tokens/s, 512 tokens, context 1, seed 1997312786)

llama_print_timings:        load time =     938.23 ms
llama_print_timings:      sample time =    1221.87 ms /   511 runs   (    2.39 ms per token,   418.21 tokens per second)
llama_print_timings: prompt eval time =       0.00 ms /     1 tokens (    0.00 ms per token,      inf tokens per second)
llama_print_timings:        eval time =   62371.98 ms /   511 runs   (  122.06 ms per token,     8.19 tokens per second)
llama_print_timings:       total time =   65992.48 ms /   512 tokens
Output generated in 66.60 seconds (7.69 tokens/s, 512 tokens, context 1, seed 315702465)

llama_print_timings:        load time =     938.23 ms
llama_print_timings:      sample time =    1207.37 ms /   511 runs   (    2.36 ms per token,   423.23 tokens per second)
llama_print_timings: prompt eval time =       0.00 ms /     1 tokens (    0.00 ms per token,      inf tokens per second)
llama_print_timings:        eval time =   62271.31 ms /   511 runs   (  121.86 ms per token,     8.21 tokens per second)
llama_print_timings:       total time =   66573.53 ms /   512 tokens
Output generated in 67.17 seconds (7.62 tokens/s, 512 tokens, context 1, seed 1633136255)
```

Average: `7.66 Tokens/s`

显存占用

```
9361
8897
8897
8697
```

# GGUF-开启split row

```
llama_print_timings:        load time =     175.30 ms
llama_print_timings:      sample time =    1228.11 ms /   511 runs   (    2.40 ms per token,   416.09 tokens per second)
llama_print_timings: prompt eval time =       0.00 ms /     1 tokens (    0.00 ms per token,      inf tokens per second)
llama_print_timings:        eval time =   48687.75 ms /   511 runs   (   95.28 ms per token,    10.50 tokens per second)
llama_print_timings:       total time =   52296.23 ms /   512 tokens
Output generated in 52.90 seconds (9.68 tokens/s, 512 tokens, context 1, seed 797024257)

llama_print_timings:        load time =     175.30 ms
llama_print_timings:      sample time =    1212.57 ms /   511 runs   (    2.37 ms per token,   421.42 tokens per second)
llama_print_timings: prompt eval time =       0.00 ms /     1 tokens (    0.00 ms per token,      inf tokens per second)
llama_print_timings:        eval time =   48738.61 ms /   511 runs   (   95.38 ms per token,    10.48 tokens per second)
llama_print_timings:       total time =   52473.24 ms /   512 tokens
Output generated in 53.07 seconds (9.65 tokens/s, 512 tokens, context 1, seed 611835546)

llama_print_timings:        load time =     175.30 ms
llama_print_timings:      sample time =    1204.94 ms /   511 runs   (    2.36 ms per token,   424.09 tokens per second)
llama_print_timings: prompt eval time =       0.00 ms /     1 tokens (    0.00 ms per token,      inf tokens per second)
llama_print_timings:        eval time =   48714.09 ms /   511 runs   (   95.33 ms per token,    10.49 tokens per second)
llama_print_timings:       total time =   52173.59 ms /   512 tokens
Output generated in 52.77 seconds (9.68 tokens/s, 511 tokens, context 1, seed 734858489)
```

Average: `9.67 Tokens/s`

显存占用

```
10511
8639
8639
8639
```
