# Reference: Agent Skills Spec, Compatibility, and Publishing

本文件是 `SKILL.md` 的重型参考，保留完整矩阵、安装速查与发布检查项。

## 1) Frontmatter Fields

### Required

| Field | Constraint | Notes |
|------|------------|-------|
| `name` | 1-64 chars, lowercase letters/numbers/hyphens | 必须与目录名一致，避免 `--` |
| `description` | 1-1024 chars | 聚焦触发条件；不要把 workflow 摘要塞进去 |

### Optional (Agent Skills Spec)

| Field | Notes |
|------|-------|
| `license` | 许可证信息 |
| `compatibility` | 环境约束 |
| `metadata` | 扩展键值 |
| `allowed-tools` | 实验字段，按实现支持 |

### Optional (Claude Code Extensions)

| Field | Purpose | Cursor Support |
|------|---------|----------------|
| `argument-hint` | 参数提示 | Partial |
| `disable-model-invocation` | 禁止自动调用，仅手动 | Partial |
| `user-invocable` | 是否在 `/` 菜单显示 | Partial |
| `allowed-tools` | skill 生命周期内工具白名单 | Partial |
| `context: fork` | 在子代理中运行 | No |
| `agent` | 指定子代理类型 | No |
| `hooks` | skill 生命周期钩子 | Partial |

## 2) Compatibility Matrix

| Field | Agent Skills Spec | Claude Code | Cursor |
|------|--------------------|-------------|--------|
| `name` | Required | Required | Required |
| `description` | Recommended | Recommended | Recommended |
| `license` | Optional | Supported | Supported |
| `compatibility` | Optional | Supported | Supported |
| `metadata` | Optional | Supported | Supported |
| `allowed-tools` | Experimental | Supported | Partial |
| `argument-hint` | N/A | Supported | Partial |
| `disable-model-invocation` | N/A | Supported | Partial |
| `user-invocable` | N/A | Supported | Partial |
| `context: fork` | N/A | Supported | Not supported |
| `agent` | N/A | Supported | Not supported |
| `hooks` | N/A | Supported | Partial |

## 3) Skill Paths by IDE

| IDE | Project Scope | User Scope |
|-----|----------------|------------|
| Claude Code | `.claude/skills/` | `~/.claude/skills/` |
| Cursor | `.cursor/skills/` | `~/.cursor/skills/` |
| Codex | `.codex/skills/` | `~/.codex/skills/` |
| OpenCode | `.opencode/skill/` | `~/.config/opencode/skill/` |

注意：`~/.cursor/skills-cursor/` 是 Cursor 内置目录，不用于自定义 Skill。

## 4) Install and Update

### OpenSkills

```bash
npx openskills install zjgulai/Claude_Skills_Create_Skills
npx openskills update lute-skills-create
```

若当前版本没有 `update` 子命令，可重新执行 `install`。

### Claude Code Direct Install

```bash
# project scope
mkdir -p .claude/skills
cp -R lute-skills-create .claude/skills/

# user scope
mkdir -p ~/.claude/skills
cp -R lute-skills-create ~/.claude/skills/
```

安装完成后可直接调用：

```text
/lute-skills-create
```

### Repository Layout Options

推荐当前仓库采用单 Skill 发布目录：

```text
repo-root/
├── README.md
├── LICENSE
└── lute-skills-create/
    └── SKILL.md
```

这种结构便于归档，也便于 OpenSkills / Claude Code 直接安装。

## 5) Publish Checklist

- `name` 合法、可检索、且与目录名 `lute-skills-create` 一致。
- `description` 聚焦触发条件，不描述步骤流程。
- 主文件 < 500 行，引用深度一层。
- 通过验证脚本与安装说明检查。
- 完成一次本地结构验证，必要时再做真实安装验证。

## 6) Content Extraction Mapping

| Extract | Ask This | Place Into |
|--------|----------|------------|
| Core objective | 解决什么问题？ | overview + description WHAT |
| Trigger scenarios | 何时触发？ | description WHEN + usage section |
| Required constraints | 哪些不可违反？ | checklist / guardrails |
| Workflow steps | 最小执行路径？ | workflow section |
| Common mistakes | 常见错误？ | anti-pattern section |
| Evidence/examples | 如何判断好坏？ | examples.md |

## 7) CSO Quick Rules

- Description starts with `Use when...`
- Include search terms users will actually say
- Do not summarize the workflow in description
- Keep high-frequency skills concise
- Keep terminology consistent
