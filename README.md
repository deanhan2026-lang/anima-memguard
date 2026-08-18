# MemGuard — AI 记忆完整性保护系统

> **记忆不可篡改，篡改必可感知。** Memory integrity is the bedrock of trust in autonomous AI agents.

MemGuard 是灵元 ANIMA 生态的记忆安全层——给 AI 智能体的记忆装上**可审计、可验证、被篡改能感知**的防护盾。与 [MemPruner](https://github.com/deanhan2026-lang/mempruner)（记忆治理·防膨胀）并列：**MemGuard 管"记忆不被篡改"，MemPruner 管"记忆不膨胀、不腐烂"**。

四支柱：Polaris（漂移诊断）· **MemGuard（存证）** · MemPruner（治理）· SOMA（自治感知）。

## 核心能力

| 版本 | 能力 | 说明 |
|------|------|------|
| **v1.0** | 双 Hash 基线锚定 | SHA-256 + BLAKE3 双保险，创建后锁定不可逆 |
| **v1.0** | 审计链追踪 | 每次变更生成 Hash 链审计日志，可追溯任意历史版本 |
| **v1.0** | 三级熔断冻结 | 警告/锁定/封印三级响应，出问题时记忆即冻 |
| **v2.0** | 增量同步协议 | Delta 增量补丁，多终端记忆同步（Push/Pull/Register） |
| **v2.0** | 冲突检测与解决 | LWW（Last Write Wins）/ 本地优先 / 远程优先 / 人工仲裁 |
| **v3.0** | G009 仲裁集成 | G009 碳基暂停键的仲裁记录引擎，裁决写入审计链 |

## 架构

```
┌──────────────────────────────────────────────────────────────┐
│                         MemGuard v3.0                        │
├──────────────────────────────────────────────────────────────┤
│  v1.0 完整性保护                                               │
│  ├─ 双 Hash 基线 (SHA-256 + BLAKE3) 锚定                     │
│  ├─ Hash 链审计日志（append-only，防篡改）                     │
│  └─ 三级熔断冻结（warn / lock / seal）                        │
├──────────────────────────────────────────────────────────────┤
│  v2.0 记忆同步协议                                             │
│  ├─ Delta（增量补丁）· Terminal（终端注册）                     │
│  ├─ Push / Pull 双向同步                                      │
│  └─ 冲突检测（content_divergence）+ LWW 解决                   │
├──────────────────────────────────────────────────────────────┤
│  v3.0 G009 仲裁引擎                                            │
│  ├─ 裁决记录写入审计链                                         │
│  └─ 仲裁级别（L1 警告/L2 冻结/L3 封印）支持                     │
└──────────────────────────────────────────────────────────────┘
```

## 快速开始

```bash
# 安装
pip install -e .

# 初始化
python server.py          # API 服务 http://localhost:5050
memguard baseline create "初始记忆内容"   # 创建 Hash 基线
memguard baseline lock                       # 锁定基线（不可逆）
memguard verify                               # 验证完整性

# v2.0 多终端同步
memguard sync register --id nyx-windows --name "Nyx-Windows"
memguard sync push --endpoint nas.local:5050
memguard sync pull --endpoint nas.local:5050
```

**Web UI：** 打开 `web/index.html`（5050 端口）访问 MemGuard 控制台（节点鉴权/基线管理/完整性验证/审计日志/冻结管理）。

## 设计哲学

- **防篡改优先**：Hash 链审计日志 append-only，基线锁定后不可逆修改
- **透明可验证**：每次变更可查审计链，任意历史版本可还原
- **故障安全**：三级熔断机制，异常时记忆即冻，防止污染扩散
- **多端自治**：Delta 增量同步，终端独立运行，NAS 是 Hub 不是主控

## 测试

```bash
python -m pytest tests/test_arbitration.py -v   # 9 用例全绿
```

## 许可证

Apache 2.0 · 灵元星辰科技（深圳）有限公司（AnimaStellar Technology (Shenzhen) Co., Ltd.）

---

灵元 ANIMA 生态：ANIMA AGENT · AnimaLink · MeshIdentity · **MemGuard** · Polaris · Argus · SOMA · MemPruner

🖤
