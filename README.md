# lute-skills-create

`lute-skills-create` 是一个可复用的 Agent Skill，用于指导创建、评审、发布符合 [Agent Skills 开放标准](https://agentskills.io/specification) 的 Skills，适用于 Claude Code、Cursor 及兼容该标准的其他工具。

## 安装

### OpenSkills

安装：

```bash
npx openskills install zjgulai/Claude_Skills_Create_Skills
```

更新：

```bash
npx openskills update lute-skills-create
```

如果你的 OpenSkills 版本不支持 `update` 子命令，可重新执行 `install` 完成更新。

### Claude Code

项目级安装：

```bash
mkdir -p .claude/skills
cp -R lute-skills-create .claude/skills/
```

用户级安装：

```bash
mkdir -p ~/.claude/skills
cp -R lute-skills-create ~/.claude/skills/
```

安装后可直接用：

```text
/lute-skills-create
```

也可以让 agent 在你提到“创建 skill、写 SKILL、frontmatter、openskills、发布 skill”等需求时自动匹配调用。

### Cursor / 兼容工具

如果通过 OpenSkills 安装，兼容工具通常会把该 Skill 安装到各自约定的 Skills 目录。若需手动安装，可将 `lute-skills-create/` 复制到对应工具的项目级或用户级 skills 目录。

## 为什么当前仓库可直接安装

本仓库采用“仓库根说明文件 + 单 Skill 目录”的发布结构：

```text
.
├── README.md
├── LICENSE
├── .gitignore
└── lute-skills-create/
    ├── SKILL.md
    ├── reference.md
    ├── examples.md
    └── scripts/
        └── validate-skill.sh
```

其中 `lute-skills-create/` 目录名与 `SKILL.md` 中的 `name: lute-skills-create` 保持一致，这更符合 Agent Skills 规范，也更适合安装工具直接识别。

## 使用

本 Skill 适用于以下场景：

- 创建新的 Agent Skill / Claude Skill
- 修改 `SKILL.md`、frontmatter、安装说明
- 将现有流程、规范或文档提炼为可复用 Skill
- 检查 Skill 的可发现性、兼容性和发布质量

主要命令与动作：

- 通过 slash command：`/lute-skills-create`
- 运行校验脚本：`./lute-skills-create/scripts/validate-skill.sh`
- 校验任意 Skill：`./lute-skills-create/scripts/validate-skill.sh /path/to/skill-dir`

## 发布检查

在发布前，建议至少确认：

- `lute-skills-create/SKILL.md` 中的 `name` 与目录名一致
- `description` 包含明确触发条件
- 主文件保持精简，参考内容放到 `reference.md`
- 安装命令、目录结构、slash command 名称全部一致

## 许可证

见 [LICENSE](LICENSE)。
