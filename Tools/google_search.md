
## Google Search 用法

### 1. 基本使用习惯
- 一个空格 ≈ AND：machine learning tutorial 会同时包含这三个词
- 操作符和关键词之间通常有一个空格：site:zhihu.com transformer
- 大小写一般不敏感：OR / or 效果相同（但建议用大写 OR 以便区分）


### 2. 逻辑与匹配操作符

| 语法 | 含义 | 示例 | 说明 |
| :--- | :--- | :--- | :--- |
| `"..."` | 精确匹配短语 | `"contrastive learning"` | 强制连续出现 |
| `word1 word2` | 同时包含 (隐含 AND) | `bayesian statistics tutorial` | 默认行为 |
| `word1 OR word2` | 至少包含其一 | `cat OR dog` | 逻辑或 |
| `-word` | 排除包含该词的结果 | `transformer -"vision transformer"` | 常用于排除噪音 |
| `*` | 通配符 (任意词) | `"neural * network"` | 多用于短语模板 |
| `()` | 组合条件 | `(deep OR representation) learning` | 复杂检索时重要 |
| `AROUND(n)` | 两词在 n 个词以内的近邻 | `"neural network" AROUND(3) compression` | 近似“靠得很近的两词” |


### 3. 限定位置：标题 / 正文 / URL / 锚文本

| 语法 | 作用位置 | 示例 | 说明 |
| :--- | :--- | :--- | :--- |
| `intitle:word` | 网页标题 | `intitle:"domain adaptation"` | 标题中包含 |
| `allintitle:...` | 标题中包含所有词 | `allintitle:domain adaptation survey` | 相当于多个 `intitle:` |
| `intext:word` | 正文内容 | `intext:"kernel trick" svm` | 正文出现该词 |
| `allintext:...` | 正文包含所有词 | `allintext:weak supervision nlp` | 更严格 |
| `inurl:word` | URL 中出现 | `inurl:pdf bert` | 常用于找特定路径 |
| `allinurl:...` | URL 中包含多词 | `allinurl:blog pytorch` | |
| `inanchor:word` | 锚文本 (链接文字) | `inanchor:"click here"` | 偏 SEO / 安全研究 |
| `allinanchor:...` | 锚文本包含多词 | `allinanchor:deep learning tutorial` | 相当于多个 `inanchor:` |


### 4. 限定站点 / 域名 / 文件类型 / 日期
### 4.1 站点与相似网站

| 语法 | 示例 | 用途 |
| :--- | :--- | :--- |
| `site:domain` | `site:zhihu.com transformer` | 只在某站内搜索 |
| `site:*.edu` | `site:*.edu "causal inference"` | 仅高教机构域名 |
| `related:domain` | `related:wikipedia.org` | 查找相似站点 |
| `info:url` | `info:https://pytorch.org` | 查看关于某 URL 的信息 |


### 4.2 文件类型

| 语法 | 示例 | 用途 |
| :--- | :--- | :--- |
| `filetype:ext` 或 `ext:ext` | `"graph neural networks" filetype:pdf` | 找 PDF 论文、报告等 |
| 组合 `site:` + `filetype:` | `site:arxiv.org "diffusion model" filetype:pdf` | 精准锁定来源与格式 |


例子：

- 教学 PPT: `"introduction to bayesian" filetype:pptx`
- 课件 PDF: `"convex optimization" filetype:pdf`


### 5. 专用功能类查询

这些不一定是“操作符”，但常用且实用。

| 用法 | 示例 | 说明 |
| :--- | :--- | :--- |
| 定义 | `define:entropy` | 直接给出单词定义 |
| 计算器 | `2^10 * 3^4` | 网页内计算器 |
| 单位换算 | `3kg in lb` | 量纲自动识别 |
| 货币换算 | `100 usd to jpy` | 实时汇率 |
| 天气 | `weather tokyo` | 当前天气卡片 |
| 时间 | `time london` | 当地时间 |
| 股价 | `tsla stock` | 股票信息卡片 |


### 6. 组合示例（科研/学习向）

### 6.1 站内 + 文件类型

找 arXiv 中与 “representation learning” 相关的 PDF 论文:
```
"representation learning" site:arxiv.org filetype:pdf
```

### 6.2 标题 + 正文双条件

标题专门讲 domain adaptation，正文必须出现 covariate shift
```
intitle:"domain adaptation" allintext:"covariate shift"
```

### 6.3 排除不想要的主题

想看 NLP 方向的 Transformer，排除视觉 / 语音相关结果
```
"transformer model" -vision -image -speech
```

### 6.4 查找特定网站的教程文章

在 TDS 上找 GNN 教程型文章
```
site:towardsdatascience.com "graph neural network" tutorial
```

### 6.5 近邻搜索（关键词靠得比较近）

两个概念在文本中相距不超过 5 个词（往往相关性更强）
```
"causal inference" AROUND(5) "instrumental variable"
```

### 7. 搜索流程建议 (个人搜索 workflow)

1.  先用自然语言问清楚自己要什么
    * 想要“教材级综述”？ -> 加 `survey`、`introduction`、`lecture notes`
    * 想要“代码”？ -> 加 `github`、`implementation`

2.  从宽到窄逐步收紧
    * 第一次： `diffusion model tutorial`
    * 发现噪声：加入 `filetype:pdf` / `site:arxiv.org` / 减去无关词

3.  善用“站点限定”锁定信息源
    * 学术： `site:arxiv.org`, `site:openreview.net`, `site:acm.org`, `site:neurips.cc`
    * 问答 / 经验： `site:stackoverflow.com`, `site:zhihu.com`

4.  遇到好 query, 记到笔记里
    * 可以在本 markdown 里开一个「我的常用查询模板」小节，按主题归类


### 8. 附：可参考的官方/非官方文档

用于后续学习补充。

- 博客: [Google Search Operators: The Complete List](https://ahrefs.com/blog/google-advanced-search-operators/?utm_source=chatgpt.com)

- PPT: [Advanced Google Search Operators Cheat Sheet](https://2886781.fs1.hubspotusercontent-na1.net/hubfs/2886781/Moz%20Website/Advanced%20Google%20Search%20Operators%20Cheat%20Sheet%20PDF.pdf?utm_source=chatgpt.com)


