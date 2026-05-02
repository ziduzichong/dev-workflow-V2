# dev-workflow v2 安装指南

**版本：** 2.0.0
**适用：** OpenCode（优先）/ Claude Code（兼容）
**GitHub：** https://github.com/ziduzichong/dev-workflow-V2

---

## 方式一：通过 Git Clone 安装（推荐）

> 从 GitHub 克隆仓库，然后复制 skill 文件到目标路径。这是最标准的方式，也方便后续 `git pull` 更新。

### Bash / Git Bash

```bash
# 1. 克隆仓库（任意目录即可）
git clone https://github.com/ziduzichong/dev-workflow-V2.git

# 2. 复制 skill 到全局路径（所有项目生效）
mkdir -p ~/.config/opencode/skills/
cp -r dev-workflow-V2/skills/dev-workflow-v2 ~/.config/opencode/skills/
```

### PowerShell

```powershell
# 1. 克隆仓库（任意目录即可）
git clone https://github.com/ziduzichong/dev-workflow-V2.git

# 2. 复制 skill 到全局路径（所有项目生效）
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.config\opencode\skills"
Copy-Item -Recurse "dev-workflow-V2\skills\dev-workflow-v2" "$env:USERPROFILE\.config\opencode\skills\dev-workflow-v2"
```

### 后续更新

```bash
cd dev-workflow-V2
git pull
# 然后重新复制 skills/ 到目标路径（或用 ln -s 软链接免去重复复制）
```

---

## 方式二：直接下载 ZIP 安装

> 不想用 Git？直接从 GitHub 下载 ZIP 包，解压后复制 skill 文件。

### 步骤

1. 打开 https://github.com/ziduzichong/dev-workflow-V2
2. 点击绿色 **Code** 按钮 → 选择 **Download ZIP**
3. 解压 ZIP 文件
4. 将解压出的 `dev-workflow-V2-main/skills/dev-workflow-v2` 文件夹复制到目标路径（见下方路径表）

### Bash / Git Bash

```bash
# 假设 ZIP 解压到了 Downloads 目录
cp -r ~/Downloads/dev-workflow-V2-main/skills/dev-workflow-v2 ~/.config/opencode/skills/
```

### PowerShell

```powershell
# 假设 ZIP 解压到了 Downloads 目录
Copy-Item -Recurse "$env:USERPROFILE\Downloads\dev-workflow-V2-main\skills\dev-workflow-v2" "$env:USERPROFILE\.config\opencode\skills\dev-workflow-v2"
```

---

## 方式三：用 curl/wget 直接下载 SKILL.md（最简）

> 如果你只需要 SKILL.md 这一个核心文件，可以用命令行直接下载。

### Bash / Git Bash

```bash
# 创建目录并下载
mkdir -p ~/.config/opencode/skills/dev-workflow-v2
curl -o ~/.config/opencode/skills/dev-workflow-v2/SKILL.md \
  https://raw.githubusercontent.com/ziduzichong/dev-workflow-V2/main/skills/dev-workflow-v2/SKILL.md
```

### PowerShell

```powershell
# 创建目录并下载
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.config\opencode\skills\dev-workflow-v2"
Invoke-WebRequest -Uri "https://raw.githubusercontent.com/ziduzichong/dev-workflow-V2/main/skills/dev-workflow-v2/SKILL.md" `
  -OutFile "$env:USERPROFILE\.config\opencode\skills\dev-workflow-v2\SKILL.md"
```

---

## 全局安装 vs 项目级安装

### 全局安装（推荐，所有项目生效）

| 平台 | 路径 |
|------|------|
| OpenCode 全局 | `~/.config/opencode/skills/<name>/SKILL.md` |
| Claude Code 全局 | `~/.claude/skills/<name>/SKILL.md` |

> Windows 下 `~` 对应 `C:\Users\你的用户名\`。上方所有命令默认安装到 OpenCode 全局路径。

### 项目级安装（仅当前项目生效）

| 平台 | 路径 |
|------|------|
| OpenCode 项目级 | `.opencode/skills/<name>/SKILL.md`（项目根目录下） |
| Claude Code 项目级 | `.claude/skills/<name>/SKILL.md` |

```bash
# 克隆后复制到项目级路径
cp -r dev-workflow-V2/skills/dev-workflow-v2 .opencode/skills/
```

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
dev-workflow-V2/
├── README.md              ← 项目说明
├── INSTALL.md             ← 本文档（安装指南）
├── LICENSE
└── skills/
    └── dev-workflow-v2/
        └── SKILL.md       ← 唯一核心文件（~600行，完全自包含）
```
