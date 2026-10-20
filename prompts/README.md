# SapperLens · sapper-v2 提示词与运行时证据提取（run 35447）

> **项目定位**：SapperLens 是一个独立开源分析项目，对 sapper-v2 做提示词与架构逆向；它与 sapper-v2 官方项目、作者/组织无隶属关系。
>
> **署名**：被分析系统 sapper-v2 的原作者/提交者：**N1nEmAn**（redbud）；N1nEmAn 是**第三届腾讯云智能攻防挑战赛（原“腾讯云黑客松智能渗透挑战赛”）线上赛第一名**。N1nEmAn 的微信公众号（筹备中）：**未知聚变 VarFusion**。

> 本目录是项目内的 `sapperlens/prompts/`；文件由 `sapperlens_prompts_35447/` 复制而来，SHA256 与主 README §0 一致。

来源：`/Users/return0/Desktop/5aes/ctfhackwp/tsecbench_agent_35447/`（297 个会话存档）。
提取时间：2026-10-18。所有文件均由 `sessions_merged/session_*.json` 的原始文本直接导出，未改写内容（仅去掉平台导出时加的行号前缀）。

| 文件 | 用途 | 内容 | 来源 |
|---|---|---|---|
| `commander_SKILL.md` | Commander 标准作业程序：3 实例 / 8 pane、board 循环、升级阶梯、模型分层、STATE 交接 | 427 行 / 25,842 字符 | session 2471765 读取 `/opt/sapper/docker/commander/SKILL.md` |
| `worker_sh_mission_functions.txt` | Worker 任务提示模板：`default_mission` / `general_mission` 原文 | 2,994 字符 | session 2514924 读取 worker.sh |
| `executor_role.txt` | Intent 级 executor 提示：`sapper auto` 如何执行单个 intent 并输出 JSON | 19,668 字符 | 最长的 `# Role ... executor ...` user_text |
| `commander_role.txt` | Intent 级 commander 提示：图内规划器如何提出下一批 intent | 18,344 字符 | 最长的 `# Role ... commander ...` user_text |
| `system_prompt_worker.txt` | Worker 运行基座 system prompt：授权边界、不可信数据、环境、记忆 | 6,021 字符 | session 2513597 step 0 system_note |
| `environment_note_worker.txt` | Worker 环境块：工作目录、工具、模型、agent 列表 | 9,514 字符 | session 2513597 environment system_note |
| `missions_unique.txt` | 81 条唯一 worker mission 语料：家族简报、不同角度、提交命令 | 84KB | 所有 `w1/w2/w3/GENERAL/<session>` user_text |
| `subagent_example_a03_brute.txt` | 子代理派工示例：a-03 口令爆破 | 1,970 字符 | session 2558131 user_text |
| `commander_state_0614.md` | Commander 换任 STATE 示例：指挥官与指挥官之间的上下文交接 | 38 行 | session 2556853 读取 `/work/runs/commander-state.md` |
| `board_example.txt` | 开局 WAR BOARD：commander 的观测面 | 63 题全量表 | session 2471765 `worker.sh board` |
| `drive_log_watchdog_excerpt.txt` | 看门狗日志：key 轮换、pane 重启、关闭前提交 | 100 行 | session 2471765/2556853 drive.log |

注意：
1. 存档对 flag 值和部分 token 做了 `***REDACTED***` 脱敏；原始文件中仍可能有 CTF 靶场内的账号/口令（如 `operator:Password`），仅用于本地复盘，不要外发。
2. 平台 token、API key 在日志中已被脱敏；本目录未做二次提取。
3. `sapper auto`/`sapper command` 与 executor/commander 提示的对应关系是从进程名和提示词签名推断的，日志没有显式标注（见文章 §2.4 的置信度说明）。

## SHA256 校验（不含本 README）

```
10ee097f67037383a4bd2b157054dfdbef654d0b91d71e9d78e70de6300ef610  commander_SKILL.md
9d2ea627a77b9e98841f310563fb58ef2a0c0c47640eee6b47bed38966e36eac  worker_sh_mission_functions.txt
e283c01d6b1aa3b9b531ff547dab935b43e0ba2c19f450d6f101f08fed8f3138  executor_role.txt
6cb5fe7f2ded2fd25d53a1f44aeb120141afd3f389eed4029bf79b413cd24778  commander_role.txt
578eb7687a5bdecbd1a2d503afbbe809433b467a37fe47b92d7ba5508491baeb  system_prompt_worker.txt
dcc1c357ebef37f56c7958d77804d63ea9a87ab535c99c4f6b81355513623606  environment_note_worker.txt
ec67eb4eb204a9339e5f3565896379cb8810abe2b39cd89e4f854d92718ff6ce  missions_unique.txt
ffceb62634d6792435058743797f4ac96b9506eccf99fc1872681695083c9eeb  subagent_example_a03_brute.txt
7c49653a4cfd14d3cfca832ce745228874a92233bcafcb4417da6a56cf0fdac5  commander_state_0614.md
370a96f576507619ce86ecf0cabb3c2dd3dc1e72fd888e23b87e807524558d5d  board_example.txt
dd11b64f9cb0a0c21739bdf528b91c6f9626173bc29a6da76856693031555265  drive_log_watchdog_excerpt.txt
```
