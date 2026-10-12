# WorkBuddy 记忆防丢失工具包 (workbuddy-memory-kit)

**中文** | [English](#english)

让 AI 助手（WorkBuddy / 类工具）长期稳定记住你，解决三大焦虑：

1. **换窗口 / 开新对话，AI 忘了之前说的** —— 对话气泡不跨窗口，记忆必须落盘。
2. **长对话后，AI 突然"记错"或"截断"了记忆** —— 系统自动生成的 profile 会漂移、会被覆盖。
3. **不知道哪些该写文件、哪些不用** —— 重要约定只停在聊天里，一关窗口就没。

本工具包把一套经过实战验证的"记忆治理 + 跨窗口交接"方法，固化成两个可直接安装的技能。

---

## 包含两个技能

| 技能 | 管什么 | 触发词示例 |
|------|--------|-----------|
| `memory-anchor` | 记忆**怎么不丢**：三层记忆架构、锚点指针目录、每日守门、灾备快照、系统 profile 漂移修正 | "怎么防止失忆" / "记忆丢了" / "AI 怎么老忘事" |
| `cross-window-handoff` | 窗口**怎么交接**：换窗口时抢救编辑历史、接上上下文、重建显示 | "换新窗口" / "来这里" / "接上" |

两者配合 = 完整防失忆方案：平时靠 `memory-anchor` 不丢，换窗口靠 `cross-window-handoff` 不丢。

---

## 安装

把 `skills/` 下的两个目录复制到你的 WorkBuddy **用户级技能目录**：

```bash
# macOS / Linux
cp -r skills/* ~/.workbuddy/skills/

# Windows (PowerShell)
Copy-Item -Recurse skills/* $env:USERPROFILE/.workbuddy/skills/
```

复制后**重启 WorkBuddy 或开新对话**，提到上文"触发词"即会自动加载。

> 用户级技能仅对你本机生效，不会影响其他用户，也不会被系统自动覆盖。

---

## 使用

- **担心 AI 忘事** → 说"怎么防止失忆"，加载 `memory-anchor`，照它的三层架构梳理你的记忆文件。
- **要换窗口** → 老窗口说"换新窗口"（AI 会抢救编辑历史并留衔接锚点），新窗口说"来这里"（AI 接上上下文并重建显示）。
- **发现 AI 记错** → 多半是系统 profile 漂移，按 `memory-anchor` 的"系统 profile 漂移修正 SOP"处理。

---

## 占位符（部署前按需替换）

技能文件内使用占位符，请替换为你自己的实际路径：

- `{{WORKBUDDY_HOME}}` — WorkBuddy 配置根目录（Windows `C:/Users/<你>/.workbuddy`，macOS/Linux `~/.workbuddy`）
- `{{KB_DIR}}` — 你存放知识库/文档的固定目录
- `{{BACKUP_ROOT}}` — 你的外部备份盘根目录
- `<OLD_UUID>` / `<your-user-id>` — 你本机 WorkBuddy 生成的会话/用户标识

> 注：原版技能在作者机器上使用了具体路径与个人信息，本开源版已全部泛化为占位符，不含任何隐私。

---

## 适用人群

- **第一次给 AI 配长期记忆的新手** —— 照做即可避免"换窗口就失忆"的坑。
- **重度使用 AI、会话多、怕丢成果的用户** —— 锚点 + 守门 + 交接三件套，保证成果不随窗口消失。

---

## 许可证

MIT —— 自由使用、修改、再分发，包括商业化。详见 [LICENSE](LICENSE)。

---

## 贡献

欢迎提 Issue / PR：更多记忆治理技巧、其他 AI 工具的适配、翻译成英文等。

---

<a name="english"></a>
# WorkBuddy Memory Kit (workbuddy-memory-kit) — English

Help your AI assistant (WorkBuddy / similar tools) remember you reliably over the long term, and fix three common anxieties:

1. **New window / new chat → the AI forgot what we said** — chat bubbles don't cross windows; memory must be persisted to disk.
2. **After a long conversation, the AI suddenly "misremembers" or "truncates" memory** — the system-generated profile drifts and can be overwritten.
3. **No idea what should be written to a file vs. left in chat** — important conventions live only in the conversation and vanish when the window closes.

This kit turns a battle-tested "memory governance + cross-window handoff" method into two installable skills.

## Two skills included

| Skill | Governs | Trigger examples |
|-------|---------|------------------|
| `memory-anchor` | How memory **stays** — 3-layer architecture, anchor-pointer directory, daily guard, disaster-recovery snapshot, system-profile drift fix | "how do I stop it forgetting" / "memory lost" / "why does my AI keep forgetting" |
| `cross-window-handoff` | How windows **hand off** — salvage edit history, reconnect context, rebuild display when switching windows | "new window" / "come here" / "pick up where we left off" |

Together they form a complete anti-amnesia solution: `memory-anchor` keeps things safe day-to-day; `cross-window-handoff` keeps things safe across windows.

## Install

Copy the two directories under `skills/` into your WorkBuddy **user-level skills directory**:

```bash
# macOS / Linux
cp -r skills/* ~/.workbuddy/skills/

# Windows (PowerShell)
Copy-Item -Recurse skills/* $env:USERPROFILE/.workbuddy/skills/
```

Restart WorkBuddy or start a new conversation; mentioning the triggers above auto-loads the skill.

> User-level skills affect only your machine — they don't impact other users and won't be auto-overwritten by the system.

## Usage

- **Worried the AI will forget** → say "how do I stop it forgetting" to load `memory-anchor`; follow its 3-layer architecture to organize your memory files.
- **Switching windows** → in the old window say "new window" (the AI salvages edit history and leaves a handoff anchor); in the new window say "come here" (the AI reconnects context and rebuilds the display).
- **AI remembered wrong** → usually a system-profile drift; follow `memory-anchor`'s "system-profile drift fix SOP".

## Placeholders (replace before deploying)

Skill files use placeholders — swap them for your actual paths:

- `{{WORKBUDDY_HOME}}` — WorkBuddy config root (`C:/Users/<you>/.workbuddy` on Windows, `~/.workbuddy` on macOS/Linux)
- `{{KB_DIR}}` — your fixed knowledge-base / documents directory
- `{{BACKUP_ROOT}}` — your external backup drive root
- `<OLD_UUID>` / `<your-user-id>` — the session / user identifiers your WorkBuddy generated locally

> Note: the original skills used concrete paths and personal info on the author's machine; this open-source edition generalizes everything to placeholders and contains no private data.

## Who it's for

- **First-timers setting up long-term memory for an AI** — follow the steps to avoid the "loses memory on window switch" trap.
- **Heavy AI users with many sessions who fear losing work** — anchor + guard + handoff keeps outputs from disappearing with the window.

## License

MIT — free to use, modify, and redistribute, including commercially. See [LICENSE](LICENSE).

## Contribute

Issues / PRs welcome: more memory-governance tips, adapters for other AI tools, English translations, etc.
