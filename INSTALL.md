# dev-workflow v2 安装指南

**版本：** 2.0.0
**适用：** OpenCode（优先）/ Claude Code（兼容）

---

## ⚠️ 重要说明

OpenCode **没有** `skill install` 命令。

Skills 是**自动发现**的：只需把 `SKILL.md` 放到约定路径，OpenCode/Claude Code 启动时会自动加载。

**路径说明（Windows）：**
- `~/.config/opencode/skills/` 对应 `C:\Users\你的用户名\.config\opencode\skills\`
- `.opencode/skills/` 对应你的**项目根目录**下的 `.opencode\skills\`

---

## 方式一：全局安装（推荐，所有项目生效）

### Bash / Git Bash

```bash
mkdir -p ~/.config/opencode/skills/
cp -r /e/WorkBuddy_workspace/dev-workflow-v2/skills/dev-workflow-v2 ~/.config/opencode/skills/
```

### PowerShell

```powershell
# 创建目标目录
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.config\opencode\skills"

# 复制 skill（注意：dev-workflow-v2 文件夹在 E:\WorkBuddy_workspace\ 下）
Copy-Item -Recurse "E:\WorkBuddy_workspace\dev-workflow-v2\skills\dev-workflow-v2" "$env:USERPROFILE\.config\opencode\skills\dev-workflow-v2"
```

### 验证全局安装

```bash
# Bash
ls ~/.config/opencode/skills/dev-workflow-v2/SKILL.md

# PowerShell
Get-ChildItem "$env:USERPROFILE\.config\opencode\skills\dev-workflow-v2\SKILL.md"
```

---

## 方式二：项目级安装（仅当前项目生效）

### Bash / Git Bash

```bash
cd /e/WorkBuddy_workspace
mkdir -p .opencode/skills/
cp -r dev-workflow-v2/skills/dev-workflow-v2 .opencode/skills/
```

### PowerShell

```powershell
cd E:\WorkBuddy_workspace
New-Item -ItemType Directory -Force -Path .opencode\skills
Copy-Item -Recurse dev-workflow-v2\skills\dev-workflow-v2 .opencode\skills\
```

---

## Claude Code 兼容路径

如果你也用 Claude Code，可以额外复制到兼容路径：

```bash
# 全局级（Bash）
mkdir -p ~/.claude/skills/
cp -r /e/WorkBuddy_workspace/dev-workflow-v2/skills/dev-workflow-v2 ~/.claude/skills/
```

```powershell
# 全局级（PowerShell）
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.claude\skills"
Copy-Item -Recurse "E:\WorkBuddy_workspace\dev-workflow-v2\skills\dev-workflow-v2" "$env:USERPROFILE\.claude\skills\dev-workflow-v2"
```

---

## OpenCode 自动扫描路径（无需手动安装）

只需把文件放对位置，OpenCode 启动时会自动发现：

| 类型 | 路径 | 说明 |
|------|------|------|
| 项目级（OpenCode 原生） | `.opencode/skills/<name>/SKILL.md` | 仅当前项目生效 |
| 全局级（OpenCode 原生） | `~/.config/opencode/skills/<name>/SKILL.md` | 所有项目生效 |
| 项目级（Claude 兼容） | `.claude/skills/<name>/SKILL.md` | Claude Code 也能识别 |
| 全局级（Claude 兼容） | `~/.claude/skills/<name>/SKILL.md` | Claude Code 全局 |

---

## 验证安装

启动 OpenCode / Claude Code，输入：

```
帮我用 dev-workflow 规划一个链表库
```

**预期行为：**
1. AI 触发 dev-workflow-v2
2. 执行 Scope Gate 判定
3. 苏格拉底追问（4个维度，每次一问）
4. 回述需求确认
5. 输出设计文档 → 逐阶段推进

---

## 卸载

### Bash

```bash
# OpenCode 项目级
rm -rf .opencode/skills/dev-workflow-v2/

# OpenCode 全局级
rm -rf ~/.config/opencode/skills/dev-workflow-v2/

# Claude Code
rm -rf .claude/skills/dev-workflow-v2/
rm -rf ~/.claude/skills/dev-workflow-v2/
```

### PowerShell

```powershell
# OpenCode 项目级
Remove-Item -Recurse -Force .opencode\skills\dev-workflow-v2\

# OpenCode 全局级
Remove-Item -Recurse -Force "$env:USERPROFILE\.config\opencode\skills\dev-workflow-v2\"

# Claude Code
Remove-Item -Recurse -Force .claude\skills\dev-workflow-v2\
Remove-Item -Recurse -Force "$env:USERPROFILE\.claude\skills\dev-workflow-v2\"
```

---

## 目录结构

```
dev-workflow-v2/
├── README.md
├── INSTALL.md
└── skills/
    └── dev-workflow-v2/
        └── SKILL.md      ← 唯一核心文件（~600行，完全自包含）
```
