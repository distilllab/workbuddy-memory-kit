---
name: cross-window-handoff
description: WorkBuddy 跨任务窗口交接的可复用 SOP。当用户说"换新窗口/换窗口/开新对话/来这里/接上"，或计划删除老任务窗口、发现 workspace/sessions 目录堆积老 UUID 时触发。解决"换窗口会不会丢东西、老窗口能不能删"的核心焦虑——把编辑历史与关键产物可靠地接手到新窗口，保证记忆与成果不随窗口消失。核心：文件产物不在窗口里，删窗口只丢编辑历史备份+对话气泡+未挪出的孤本；老窗口说"换新窗口"立即抢救并留衔接锚点，新窗口说"来这里"接上并重建显示。
agent_created: true
---

# 跨窗口交接 SOP（保证记忆不随窗口消失）

## 一句话结论
文件产物（研报卡/.py/.md/HTML）最终版**从不住在窗口里**，都在固定路径（你的知识库目录 / 项目目录 / 桌面存档目录）。删窗口真正会丢的只有三样：编辑历史备份 `.modify_backup_meta` + 对话气泡 + 未挪出的孤本。把"接手"做成标准动作，老窗口就能安心删。

## 一句话触发协议（用户提炼）
- **老窗口说「换新窗口」**（或等价：换窗口/开新对话/建新任务）→ 立即执行 **②③**：
  - ② 抢救编辑历史：把老窗口 `sessions/<OLD_UUID>/.modify_backup_meta/` 整目录 `robocopy /E` 归档到 `{{KB_DIR}}/.workbuddy/session-backups/<OLD_UUID>/`
  - ③ 查孤本：比对老窗口 `modify_backup/` 里的 .md/.py 与固定路径，列「外面找不到的」给用户确认
  - **留衔接锚点**：把「老UUID + 归档路径 + 交接清单路径」写入当日日志 / MEMORY
- **新窗口说「来这里」**（或等价：接上/换新了）→ 执行 **①④**：
  - ① 读 MEMORY.md + 最新存档篇，重建上下文（已自动注入）
  - ④ 产物显示重建：用 present_files / 文字清单，把老窗口关键成果（最终版路径）复现一遍，补对话气泡断层

## 时序铁律
老窗口的「换新窗口」**必须在删老窗口之前**完成。一旦老窗口被删，`sessions/<OLD_UUID>/.modify_backup_meta` 物理消失，②③ 无法补做，编辑历史永久丢失——这是唯一不可后悔的环节。

## 衔接靠"写文件"不靠"对话气泡"
两个窗口之间唯一可靠的线，是老窗口写进日志/MEMORY 的「UUID + 归档路径」。新窗口靠读文件接上，绝不依赖记忆对话内容（对话气泡不跨窗口）。

## 与系统自动化的边界
WorkBuddy 无「对话说某句就跨窗口执行」的系统钩子。「固定去完成」是**AI 按记忆/技能约定的标准动作**，不是系统魔法——前提是 AI 在该会话里还活着、能执行命令。若老窗口已关/已删，则只能做 ①④（接上），②③ 已不可逆。

## 实操命令（② 抢救编辑历史，Windows）
```bash
# MSYS_NO_PATHCONV 防止 Git Bash 改写 Windows 绝对路径；其他 shell 去掉前缀即可
MSYS_NO_PATHCONV=1 robocopy "{{WORKBUDDY_HOME}}/workspace/sessions/<OLD_UUID>/.modify_backup_meta" "{{KB_DIR}}/.workbuddy/session-backups/<OLD_UUID>/.modify_backup_meta" /E /R:1 /W:1 /XJ
MSYS_NO_PATHCONV=1 robocopy "{{WORKBUDDY_HOME}}/workspace/sessions/<OLD_UUID>/modify_backup" "{{KB_DIR}}/.workbuddy/session-backups/<OLD_UUID>/modify_backup" /E /R:1 /W:1 /XJ
```
归档后生成 `交接清单-YYYY-MM-DD.md`（含：老UUID、归档路径、孤本核查结论、可安全删确认），present 给用户。

## 删前兜底（可选）
整目录 `robocopy /E` 老窗口到 `{{BACKUP_ROOT}}`（你的备份盘），成本近乎零，能 100% 找回。

## 占位符说明（部署时替换）
- `{{WORKBUDDY_HOME}}` = WorkBuddy 配置根目录（Windows `C:/Users/<你>/.workbuddy`，macOS/Linux `~/.workbuddy`）
- `{{KB_DIR}}` = 你存放知识库/文档的固定目录
- `{{BACKUP_ROOT}}` = 你的外部备份盘根目录
- `<OLD_UUID>` = 老窗口会话目录的 UUID（在 `sessions/` 下可查，形如 `xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`）

## 关联
- 记忆治理总纲：`skills/memory-anchor/SKILL.md`
- 长期记忆索引：`{{WORKBUDDY_HOME}}/user-<your-user-id>-personal/MEMORY.md`
- 归档落点：`{{KB_DIR}}/.workbuddy/session-backups/<OLD_UUID>/`
