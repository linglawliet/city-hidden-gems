# 🗺 Hidden Gems City Guide — 执行手册

> 只需给出城市名，按此手册即可生成一份完整的本地隐藏宝藏 HTML 指南。

---

## 一、项目概述

**目标**：为刚搬到某城市的人，生成一份可交互的本地 Hidden Gem 指南，涵盖餐饮、咖啡、自然、文化艺术、书店、酒吧六大类，以精美 HTML 单文件呈现，可直接在浏览器打开或托管为网页。

**输出物**：一个 `[city-name]-hidden-gems.html` 文件，无需联网、无需框架，开箱即用。

---

## 二、数据搜索阶段

### 2.1 调用 `places_search` 工具

**一次性发起 6 条并行查询**，每条针对一个类别：

| 类别 | 查询语句示例 | max_results |
|------|-------------|-------------|
| 餐饮 | `"hidden gem restaurants [City] [State]"` | 8 |
| 咖啡 | `"best cafes coffee shops [City] [State]"` | 6 |
| 自然 | `"nature parks trails [City] [State]"` | 6 |
| 文化艺术 | `"art galleries museums [City] [State]"` | 5 |
| 书店 | `"independent bookstores unique shops [City] [State]"` | 6 |
| 酒吧 | `"bars cocktail wine [City] [State]"` | 6 |

**关键字段提取**（每个地点）：
- `name`、`address`、`rating`、`rating_count`
- `weekday_hours`（提炼为"营业时段"）
- `reviews`（前 2–3 条，用于提炼描述和 Tip）
- `types`（用于确定子标签，如 "Italian · BYOB"）

---

## 三、内容写作规范

### 3.1 每张卡片包含

```
card-tag     : 2–3个英文关键词，用 · 分隔（如 "Italian · Counter Service"）
card-name    : 地点名称
card-desc    : 100–130字中文描述，突出最独特之处，语气像朋友推荐
card-tip     : 1条本地秘籍，以"✦"开头，30–50字，具体可操作
card-meta    : 地址简写 + 营业时间关键信息 + 评分
```

### 3.2 写作语气

- 像一个在当地住了几年、真正热爱这座城市的朋友在写
- 避免旅游手册口吻，不用"著名"、"必去"等空泛词
- Tip 要具体：点什么、几点去、问谁、注意什么
- 每类开头的 `intro-banner` 用 1–2 句话点出该城市该类别的独特气质

### 3.3 数量目标

| 类别 | 最少卡片数 | 建议卡片数 |
|------|-----------|-----------|
| 餐饮 | 5 | 6–7 |
| 咖啡 | 4 | 5–6 |
| 自然 | 4 | 5–6 |
| 文化艺术 | 4 | 5 |
| 书店 | 3 | 5–6 |
| 酒吧 | 3 | 4–5 |

---

## 四、设计风格系统

### 4.1 每座城市选择一套独立的配色方案

**禁止两座城市使用相同的色系。** 参考已用方案：

| 城市 | 主色调 | 背景色 | 强调色 | 风格关键词 |
|------|--------|--------|--------|-----------|
| Montclair NJ | 米白/深墨 | `#f5f0e8` | `#b5421a` 锈红 | 编辑/杂志风 |
| Ann Arbor MI | 深海蓝/金 | `#060e1a` | `#d4a843` 琥珀金 | 典雅/大学城 |

**新城市配色方向参考**（可选其一再变化）：
- 深森绿 + 暖铜色（适合自然资源丰富的城市）
- 砖红 + 沙白（适合历史悠久的东岸城市）
- 炭灰 + 霓虹粉/绿（适合艺术/工业型城市）
- 奶油黄 + 深棕（适合南部或阳光系城市）

### 4.2 字体选择规范

每次从以下组合中**选一套未用过的**：

```
组合A（已用·Montclair）: DM Serif Display + Libre Baskerville + Outfit
组合B（已用·Ann Arbor）: Cormorant Garamond + EB Garamond + Josefin Sans
组合C（待用）: Playfair Display + Lora + DM Sans
组合D（待用）: Fraunces + Source Serif 4 + Space Grotesk
组合E（待用）: Editorial New + Instrument Serif + Neue Montreal
```

均从 Google Fonts 免费引入。

### 4.3 视觉元素清单（必须包含）

- **Masthead**：全屏封面，城市名大字排版，含副标题和氛围描述
- **导航栏**：Tab 切换，Sticky 固定，含 emoji 图标
- **Welcome 区**：左文右视觉（大字母/城市符号），中文欢迎语
- **Section Header**：大号罗马数字/章节数字 + 标题
- **Intro Banner**：每类开头的横幅引言
- **Card Grid**：自适应多列，每卡含色块线、标签、名称、描述、Tip、Meta
- **Footer**：城市名 + 经纬度或地区信息

---

## 五、HTML 文件结构模板

```html
<!DOCTYPE html>
<html lang="zh">
<head>
  <!-- Google Fonts（选当次组合） -->
  <!-- CSS变量 + 全局样式 -->
  <!-- Masthead / Nav / Section / Card / Footer 样式 -->
  <!-- 动画：fadeUp / fadeIn / pulse -->
</head>
<body>
  <!-- MASTHEAD：封面 -->
  <!-- NAV：7个Tab（序言 + 6类） -->

  <!-- SECTION #welcome：欢迎语 + 城市视觉 -->
  <!-- SECTION #food：餐饮 -->
  <!-- SECTION #coffee：咖啡 -->
  <!-- SECTION #nature：自然 -->
  <!-- SECTION #culture：文化艺术 -->
  <!-- SECTION #books：书店 -->
  <!-- SECTION #drinks：酒吧 -->

  <!-- FOOTER -->

  <script>
    // showSection(id) 函数：Tab切换 + 滚动到顶部
  </script>
</body>
</html>
```

**文件命名**：`[city-slug]-hidden-gems.html`（如 `boston-hidden-gems.html`）

**输出路径**：`/mnt/user-data/outputs/`

---

## 六、质检清单

生成完毕后，逐项核对：

- [ ] 每个类别至少有 4 张卡片
- [ ] 所有地址已简化（非完整 URL 格式）
- [ ] 营业时间已提炼为可读格式（如 "Wed–Sun from 4pm"）
- [ ] 每张卡片有独立的 Tip，内容具体而非泛泛
- [ ] 配色与之前城市明显区分
- [ ] 字体组合与之前城市不同
- [ ] Welcome 区有该城市的个性描述（非通用模板句）
- [ ] Intro Banner 反映该城市该类别的真实气质
- [ ] HTML 文件可在浏览器直接打开，无报错
- [ ] Tab 切换正常，所有 Section 可访问

---

## 七、分享方式（提示用户）

生成后可告知用户以下三种分享方式：

1. **直接发文件**：`.html` 文件发微信/邮件，对方用浏览器打开
2. **Netlify Drop**：拖入 [drop.netlify.com](https://drop.netlify.com)，30秒得到永久链接
3. **打印PDF**：浏览器 `Ctrl/Cmd+P` → 存储为 PDF，可作为实体礼物

---

## 八、触发指令

用户只需说：

> **"帮我做一个 [城市名] 的 hidden gems 指南"**

即可按此手册完整执行。无需重复解释流程。
