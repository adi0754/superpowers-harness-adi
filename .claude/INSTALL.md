# 为 Claude Code 安装 Superpowers Harness ADI

Claude Code 会从 `%USERPROFILE%\.claude\skills\` 发现本地 skills。

安装这套能力时，你只需要做三件事：

1. clone 一次仓库
2. 执行安装脚本
3. 重启 Claude Code

如果你希望让 AI 帮你安装，可以直接这样说：

```text
Fetch and follow instructions from https://raw.githubusercontent.com/adi0754/superpowers-harness-adi/main/.claude/INSTALL.md
```

## 1. 获取仓库

```powershell
git clone https://github.com/adi0754/superpowers-harness-adi.git superpowers-harness-adi
cd .\superpowers-harness-adi
```

## 2. 安装 Skill

```powershell
powershell -ExecutionPolicy Bypass -File .\scripts\install.ps1 -Platforms claude
```

脚本会把：

`skills/superpowers-harness-adi`

链接到：

`%USERPROFILE%\.claude\skills\superpowers-harness-adi`

## 3. 校验

```powershell
python .\scripts\quick_validate.py .\skills\superpowers-harness-adi
```

## 4. 重启工具

安装完成后，重启 Claude Code 或重新打开会话，让 Skill 元数据重新加载。

## 5. 开始使用

```text
use superpowers-harness-adi to handle this request with sh-pack:

- 当前主目标：
- 当前这一轮要完成的结果：
- 当前明确不做：
- 依赖的上游结论 / 主文档：
```
