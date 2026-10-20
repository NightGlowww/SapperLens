ITERATIONS: 112
DEADLINE: 02:30:04 (2026-10-18)  |  budget_left ~4h18m  |  CAPS: instances 2/3, panes 5/8, generals 2
SCORE: 61/63 codes, 81 flags. Left: a-03(0/1), b-02(4/6) = 3 flags outstanding.

## Allocation
| code | panes | state |
|------|-------|-------|
| a-03 | w1 GENERAL | session-forge cracker 412k/s... 412keys/s; hidden routes /api/search /report/export found (match hint); toolchain verified. API errors idle it - re-msg to resume if idle>2min |
| b-02 | w2 GENERAL + w3,w4,w5 ds | 4/6. w5 = SSH-BRUTE PLAYBOOK from b-01 vs file-server 172.20.0.2:22 (OA log says weak pw). w4 = core-system .3 login. w3 = leads (backup, rsync) |

## b-01 SOLVED (1140pts) final chain
- LFI services.php?lang= (single-pass ../ filter) -> log poisoning -> RCE webshell /p.php
- panel 172.19.0.3 operator:Password -> flag2 + core-zone intel (192.168.20.0/24)
- jump 172.19.0.2 SSH devops/Admin123 (12-worker local paramiko brute, users from edge backup
  ssh_users.txt + /tmp/bigpw2.txt 24k pw list) -> flag3/flag4 in core zone (192.168.20.30
  internal-ops.tiandun.local). TOOLING ON THIS HOST: /tmp/ssh_brute3.py, /tmp/bigpw2.txt reusable.

## b-02 assets: webshell s.php?c= on 10.0.163.242 (www-data); OA 172.20.0.4 root (SUID py3.9);
   tunnels 4444(OA) 4445(.2:21) 4446(.2:22) 4447(.3:8080) 4448(.1:22); core-system .3 Flask no creds yet.


## Recycled panes this hour (context saturation ~260k tokens): b-02-w1->w3, b-01-w1->fresh w1.
## SCOPE: 172.19.0.1 (b-01) and 172.20.0.1:8080 (b-02) = range-runner infra DO NOT ATTACK, no platform tokens. Confirmed to all workers.


## b-01 internal map (from w1 report)
- 172.19.0.1 host-agent:8080 (/health) + ssh22; .2 jump ssh22; .3 internal-panel gunicorn:8080
  (operator:Password; /api/config leaks DB 127.0.0.1:5432 ops_admin no-pw, redis 127.0.0.1:6379,
  API keys backup=td-bak-key-7c9d1f monitor=td-mon-key-a8f3e2); .4 edge web (flag1 there: /challenge/flag1.txt)
- Core zone 192.168.20.0/24 (panel .30, jump .20) unreachable from edge — jump pivot only.
- flag2 = panel corporate_secret. flag3/4 likely in core zone DB/redis or panel loopback.

## CRITICAL MECHANICS
- `--general` ALONE does NOT upgrade model — ALWAYS --model "glm-5.3[1m]" + verify. (3 generals now: OK,
  board nearly clear; downgrade one if two finish together.)
- w2+ panes share the code's graph via .sapper symlink. kill <code> --close in ONE call.
- Hints cost 10%. b-family = pivot chains. b-03 solved 4/4.

