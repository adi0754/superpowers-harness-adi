# Superpowers Harness ADI

> 不是让 AI 接管复杂项目，而是帮你在复杂项目里继续当主导者。  
> 用 `sh-start / sh-pack / sh-run / sh-recover` 4 个短入口，把 superpowers 的复杂 workflow 收成一个更稳、更轻、更容易坚持的默认用法。

`superpowers-harness-adi` 是一个绑定 superpowers 的场景入口型 workflow skill。

它适合这样的开发者：

- 已经在用 AI 辅助开发
- 一做大需求、新项目、多轮规划、多轮执行就容易失控
- 不想再靠一长串 prompt 硬撑 workflow
- 希望既提升推进效率，又保留自己对项目的理解、判断和讲述能力

---

## 你可能也遇到过这些问题

当项目开始变大，很多 AI 协作会慢慢变成这样：

- prompt 越写越长，自己都不想再复制第二遍
- brainstorming、writing-plans、executing-plans 要靠人手动切来切去
- 文档和阶段越来越多，但主线越来越不清楚
- AI 做了很多事，人却越来越难讲清楚“为什么这么做”
- 一轮轮推进后，项目虽然没停，但你对它的掌控感在下降

这不是“不会用 AI”，而是复杂项目天然会把协作拉向失控。

---

## 用它之后，会有什么变化

| 没有 Harness | 有了 Harness |
| --- | --- |
| 靠自己记住一整套 workflow prompt | 只记 4 个短入口 |
| 一上来就开跑，信息不全也硬做 | 先做输入预检，缺信息先补模板 |
| AI 容易顺着惯性扩需求、长阶段 | 默认带边界、停机线和人工拍板点 |
| 文档越写越多，但主线越来越散 | 先定锚，再压包，再执行，跑偏再收敛 |
| 人越来越像最后验收者 | 人重新回到主目标、边界和路线的主导位 |

它的目标不是“更强自动化”，而是：

**给复杂项目一个更稳定的默认 workflow，让开发者在不牺牲主导权的前提下，把 AI 真正用顺。**

---

## 它是什么，不是什么

### 它是什么

- 一个绑定 superpowers 的 workflow 入口层
- 一个面向复杂项目的轻量协作护栏
- 一个减少重复 prompt 成本的默认用法
- 一个帮助开发者保留主导权的产品化入口

### 它不是什么

- 不是一键全自动开发系统
- 不是多 agent 编排平台
- 不是通用项目管理系统
- 不是软件工程百科
- 不是大而全的工程框架

---

## 四个入口

| 入口 | 什么时候用 | 会产出什么 | 主要绑定 |
| --- | --- | --- | --- |
| `sh-start` | 新项目启动；已有项目上的大功能启动 | 目标、MVP、明确不做、推荐路线、主文档 | `brainstorming` -> `writing-plans` |
| `sh-pack` | 当前目标已定，要生成这一轮执行包 | 当前执行包 | `writing-plans` |
| `sh-run` | 已经有执行包，准备开始做 | 实现结果、风险、难点、学习沉淀 | `executing-plans` |
| `sh-recover` | 项目或功能已经漂了 | 当前真相、收敛结论、必要时重写文档 | `brainstorming` -> `writing-plans` |

以后你脑子里不需要再记：

`brainstorming -> 你拍板 -> writing-plans -> writing-plans -> executing-plans`

只需要记：

`sh-start -> sh-pack -> sh-run`

跑偏了就：

`sh-recover`

---

## 一个很关键的设计

所有入口都先过一层 `Input Check`。

这意味着：

1. 不是用户随便输一句，Skill 就直接开跑
2. Skill 会先判断关键信息够不够
3. 如果缺少关键项，会先回对应模板
4. 模板补齐后，再正式进入 workflow

这件事看起来很小，但非常关键。  
因为复杂项目最容易出问题的地方，往往不是“不会写代码”，而是：

**一开始输入就不完整，后面每一轮都在错误上下文上继续推进。**

---

## 快速开始

### 1. 安装

阅读与你当前工具对应的安装说明：

- [Codex 安装说明](.codex/INSTALL.md)
- [Claude Code 安装说明](.claude/INSTALL.md)
- [Cursor 安装说明](.cursor/INSTALL.md)

### 2. 重启工具

安装完成后，重启你的 AI 工具，让 Skill 元数据重新加载。

### 3. 开始用

第一次使用，你只需要发出这样的请求：

```text
use superpowers-harness-adi to handle this request with sh-start:

- 当前项目 / 功能背景：
- 这次想解决的问题：
- 为什么现在做：
- 已知约束：
```

---

## 简单上手示例

假设你要在一个已有项目里新增一个大功能：

**给企业短视频平台增加“声音复刻”能力。**

你第一次可以这样用：

```text
use superpowers-harness-adi to handle this request with sh-start:

- 当前项目 / 功能背景：
  企业短视频生成平台，当前已有文案生成、视频剪辑、普通 TTS 配音、字幕和导出能力。

- 这次想解决的问题：
  现在要增加“声音复刻”能力，让企业客户可以基于授权音频生成品牌专属配音。

- 为什么现在做：
  当前普通 TTS 的品牌识别度不够，业务希望提升视频配音的品牌一致性。

- 已知约束：
  必须先控制授权与合规风险；
  当前只做 MVP，不扩展成完整语音平台；
  优先考虑接入第三方底层能力。
```

理想情况下，Skill 会先帮你做这些事：

1. 收敛这次功能真正要解决的问题
2. 帮你明确 MVP 和明确不做
3. 给出 1 到 3 条路线比较
4. 要求你留下拍板结果
5. 拍板后再整理成功能主文档

如果你给的信息不够，Skill 不会直接开跑，而是会先回一个 `sh-start` 模板让你补。

---

## 最短调用模板

### `sh-start`

```text
sh-start

- 当前项目 / 功能背景：
- 这次想解决的问题：
- 为什么现在做：
- 已知约束：
```

### `sh-pack`

```text
sh-pack

- 当前主目标：
- 当前这一轮要完成的结果：
- 当前明确不做：
- 依赖的上游结论 / 主文档：
```

### `sh-run`

```text
sh-run

- 当前执行包：
- 本轮主目标：
- 本轮明确不做：
- 哪些情况必须停下来汇报：
```

### `sh-recover`

```text
sh-recover

- 当前项目 / 功能：
- 最漂移的地方：
- 我这次最想先收回什么：
- 当前已有线索：
```

---

## 仓库结构

```text
superpowers-harness-adi/
├─ README.md
├─ .codex/
├─ .claude/
├─ .cursor/
├─ docs/
├─ scripts/
├─ skills/
│  └─ superpowers-harness-adi/
│     ├─ SKILL.md
│     ├─ agents/openai.yaml
│     ├─ references/
│     └─ templates/
└─ tests/
```

---

## 本地校验

校验 Skill 结构：

```powershell
python .\scripts\quick_validate.py .\skills\superpowers-harness-adi
```

运行校验脚本测试：

```powershell
python -m unittest .\tests\test_quick_validate.py
```

---

## 当前 v1 范围

当前 v1 重点只放在：

- 4 个固定入口
- 入口预检
- superpowers 绑定方式
- 轻量安装与分发

当前明确不做：

- 自动化平台
- 多 agent 编排框架
- Web 控制台
- 通用项目管理系统
- 大而全的软件工程百科
