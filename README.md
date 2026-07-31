# seo-image-prompt

> 读懂 SEO 页面语义 → 为每个模块生成高质量配图 Prompt → 输出完整的图片 SEO 元数据。

一个给 Claude Code / Codex / Cursor / Windsurf 等支持 Agent Skills 规范的编程 agent 使用的技能。它不绑定任何生图工具：你可以用 VisualGPT、Midjourney、DALL·E 或任意图像 API 把生成的 prompt 变成图。

## 为什么需要它

普通「AI 配图提示词合集」的问题是：给个模块名就出图，画出来千篇一律、和你的产品无关。本技能的核心思路是 **先读懂页面，再决定画什么**——每张图生成前必须先回答 `Who / Problem / Action / Result` 四问，且必须能溯源到页面里具体的一句 H2 文案。这样产出的配图才贴你的产品、在 Google Image 里有点击竞争力。

## 安装

### 方式一：skills CLI（推荐）

```bash
npx skills add visualgptio/seo-image-prompt
```

会自动装进 `.agents/skills/`，并软链一份到 `.claude/skills/`，兼容 Claude Code。

### 方式二：手动复制

把 `skills/seo-image-prompt/` 整个目录复制到你的项目：

```bash
mkdir -p .claude/skills
cp -r skills/seo-image-prompt .claude/skills/
```

## 使用

直接用自然语言提需求，agent 会自动调用：

```
"给我的 SEO 落地页配图，主色是奶油白+炭灰，风格写实摄影"
```

首次使用会先向你确认四组信息（品牌视觉 / 页面内容 / 图片规格 / 已配图页面），确保风格统一、不撞图。

## 模块配图策略

| 模块 | 生图 | 默认构图 |
|------|:---:|---------|
| intro | ✅ | transformation / analysis / capability / scenario（按产品类型选） |
| pain | ✅ | split_screen（Before vs After） |
| usecase | ✅ | persona / scenario / industry / before-after（4 张图区分模式） |
| highlight | ✅ | feature_proof（功能证据） |
| howto / review / cta / faq | ❌ | 真机截图或暂不配图 |

## Prompt 写作铁律（节选）

1. 说物品不说标签：`cream cashmere coat with visible weave texture` 而非 `luxury aesthetic`
2. 说光源不说氛围：`late afternoon sun through tall windows` 而非 `warm atmosphere`
3. 说材质不说风格：`matte black turtleneck against raw concrete` 而非 `Vogue editorial`
4. 限色调不堆色：限定 1-2 主导色 + 1 中性色
5. 不教 AI 排版：`top half empty for text` 是 CSS 的事
6. 否定词必加：`No text, no words, no watermarks, no logos...`

完整方法论、人物/场景描述公式、常见出图问题修正、QA 评分维度见 [`skills/seo-image-prompt/SKILL.md`](skills/seo-image-prompt/SKILL.md)。

## 许可证

[MIT](LICENSE) —— 随便拿去改，随便商用。
