# Llama-3.1-8B PQCache 0.1 实验记录

本次使用 LongBench v1 的 14 个任务，共 2750 条样本；生成、评分和汇总均已完成。

## 运行配置

| 参数 | 值 |
| --- | --- |
| 模型 | meta-llama/Llama-3.1-8B-Instruct |
| 模型 revision | 0e9e39f249a16976918f6564b8830bc894c89659 |
| GPU | 单张 NVIDIA A800-SXM4-40GB |
| 精度 | FP16 |
| COMPRESSOR | pq_search |
| EXP_NAME | default |
| COMPRESS | 0.1 |
| RECENT_RATIO | 0.5 |
| SINK_SIZE | 32 |
| SUBVEC / SUBBITS | 2 / 6 |
| MAX_ITER | 0，自适应迭代 |
| MAX_CPU_IN_USE | 16 |
| Python / PyTorch / Transformers | 3.10.20 / 2.1.2+cu121 / 4.43.3 |
| FlashAttention | 2.5.8 |

## 结果

- 14 项任务分数之和：652.67；宏平均分：46.62。
- 论文表 2 的 PQCache 10% token 预算列平均分为 47.19，本次低约 0.57 分。
- [各任务汇总](../pred/llama-3.1/default_summary.json)
- [逐项论文对照 CSV](../pred/llama-3.1/paper_table2_pq_0.1_comparison.csv)
- [论文表 2](https://arxiv.org/html/2407.12820v2#S4.SS2.SSS1)

按 tmux 会话创建时间与最终汇总文件写入时间估算，端到端耗时约 8 小时 52 分钟：北京时间 2026-10-27 16:47 至 2026-10-28 01:40。

当前 `run_llama.sh` 已切换到下一轮 Full 配置（`original`、`EXP_NAME=full`）。若重跑本次实验，需要先恢复上表中的 PQCache 配置。模型、数据、虚拟环境和登录凭据仅保存在本地，不随实验记录提交。
