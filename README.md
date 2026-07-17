# Skills

潘坤的 Codex / ChatGPT 个人 skill 集合。每个子目录都是一套独立、可安装和可版本化维护的 skill。

## 目录

- `skills/adaptive-learning-tutor/`：先诊断学习者的知识结构，再生成个性化技术讲解与学习笔记。
- `skills/study-motor-papers/`：面向电机、电机控制与电力电子文献的全文翻译、阅读前基础诊断、逐段精读和 Fig 图解。

## 仓库结构

```text
skills/
├── adaptive-learning-tutor/
│   ├── SKILL.md
│   └── agents/openai.yaml
└── study-motor-papers/
    ├── SKILL.md
    ├── agents/openai.yaml
    └── references/
```

两套 skill 分别独立维护；不要把论文原文、生成的学习笔记或临时产物提交到 skill 源码目录。
