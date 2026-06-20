# 🌿 FoodReliefSA · CommonGround

**南澳大利亚免费及低价食物资源双语目录**
**Bilingual free food resource directory for South Australia**

> 🌐 Live site: [https://luoli0530-yunzi.github.io/foodrelief-sa/](https://luoli0530-yunzi.github.io/foodrelief-sa/)
> 📬 Contact: yunziluo520@gmail.com

---

## 项目简介 / About

FoodReliefSA（CommonGround）是一个面向南澳大利亚华语社区及英语用户的**单页食物援助目录网站**，帮助有需要的人快速找到离自己最近的免费或低价食物服务点。

This is a single-file, zero-dependency bilingual website that helps people in South Australia locate free and low-cost food relief services near them — with full Chinese and English support.

---

## 功能特性 / Features

### 🔍 智能地址搜索 / Smart Location Search
- 支持输入**郊区名称、邮编或街道地址**进行搜索
- 三层地理编码策略：本地邮编表 → 郊区名称映射 → OpenStreetMap Nominatim API 兜底
- 输入时实时显示**自动补全建议**（服务点名称 + 郊区名）

### 📍 距离排序与分层展示 / Distance-based Display Logic
- 搜索后按 Haversine 公式计算真实直线距离，结果按距离升序排列
- **10km 以内**：直接显示，标注距离
- **10km 内少于 3 个结果**：自动扩展至 25km，并显示提示横幅
- **超出已显示范围**：折叠为"查看更多服务"按钮，点击展开

### 🏷️ 筛选器 / Filter Chips
7 个快速筛选标签：
| 标签 | 说明 |
|------|------|
| 全部 / All | 显示所有服务 |
| 完全免费 / Free | 完全免费服务 |
| 低价优惠 / Low cost | 低价或优惠服务 |
| 北部 / North | Adelaide 北部 |
| 南部 / South | Adelaide 南部 |
| 市区 / CBD | Adelaide 市中心 |
| 无需预约 / No appointment | 无需提前预约 |

### 🌏 中英双语 / Bilingual
- 自动根据浏览器语言偏好（`navigator.language`）选择中文或英文
- 右上角语言切换按钮，随时切换
- 所有服务卡片、搜索提示、筛选标签、页脚均双语适配

### 🎴 服务卡片 / Service Cards
每张卡片包含：服务名称、简介、地址、开放时间、电话（如有）、距离标注、预约提醒、官网链接。全部 **54 个服务点**，覆盖 Adelaide 大都会区及部分区域服务。

### 🌲 视觉动效 / Visual Effects
- Canvas 树叶粒子系统（仅在 hero 区域运行，支持暂停/恢复）
- 点击/触摸 hero 区域触发**风吹动效**，树冠跟随摇摆
- 卡片进入视口时的**滚动渐显动画**（Intersection Observer）
- 所有动效遵循 `prefers-reduced-motion` 无障碍设置

---

## 服务数据 / Service Data

共收录 **54 个服务点**，涵盖以下机构：

- OzHarvest 免费市场
- Heart & Soul（Wingfield / Noarlunga）
- Cos We Care
- Fred's Van（CBD / Kilburn / Salisbury / Elizabeth / Gawler / Semaphore / Aldinga / Christie Downs）
- Foodbank 食物站（Bowden）
- Baptist Care、Salvation Army（救世军）
- St Vincent de Paul、Anglicare SA
- Uniting Communities、Hutt St Centre
- Bedford Group、Centacare、Junction Australia
- Meals on Wheels（送餐上门）
- Lighthouse Foodbank、Community Centres SA
- 以及更多本地食物救助机构

每个服务点包含字段：`名称（中/英）`、`简介（中/英）`、`类别（free/low/appt）`、`地址`、`营业时间（中/英）`、`电话`、`官网 URL`、`地区标签`、`GPS 坐标`

---

## 技术实现 / Technical Details

| 项目 | 说明 |
|------|------|
| 架构 | 纯单文件 HTML，无框架，无构建工具 |
| 字体 | Bricolage Grotesque + Plus Jakarta Sans（Google Fonts） |
| 地理编码 | 内置 SA 邮编表 + 郊区映射 + Nominatim API fallback |
| 距离计算 | Haversine 公式（球面距离） |
| 动效 | HTML Canvas + requestAnimationFrame |
| 滚动动画 | Intersection Observer API |
| SEO | Open Graph、Twitter Card、Schema.org JSON-LD、canonical URL |
| 部署 | GitHub Pages（单文件，零依赖） |

---

## 部署方式 / Deployment

本项目为**单文件静态网站**，直接部署至 GitHub Pages：

```
仓库结构：
/
└── index.html   ← 整个网站
```

1. Fork 或克隆此仓库
2. 进入仓库 Settings → Pages
3. Source 选择 `main` 分支 / `root` 目录
4. 保存后稍等片刻，网站即可通过 `https://<username>.github.io/<repo>/` 访问

---

## 如何添加新服务点 / Adding a New Service

在 `index.html` 的 `SITES` 数组中添加一条记录，格式如下：

```javascript
{
  sid: 54,                          // 唯一 ID（递增）
  zh: { name: "服务名称", desc: "简介" },
  en: { name: "Service Name", desc: "Description" },
  ic: "🏪",                         // 图标 emoji
  t: "free",                        // "free" | "low" | "appt"
  appt: false,                      // 是否需要预约
  addr: "123 Example St, Suburb SA 5000",
  zh_hrs: "周一至周五 9am–5pm",
  en_hrs: "Mon–Fri 9am–5pm",
  ph: "08 8xxx xxxx",               // 电话（可留空 ""）
  url: "https://example.org",       // 官网（可留空 ""）
  areas: ["north"],                  // "north" | "south" | "cbd" | "regional"
  lat: -34.9000,                    // GPS 纬度
  lng: 138.6000                     // GPS 经度
}
```

---

## 目录结构 / File Structure

```
index.html
├── <head>           — Meta / SEO / 字体引入
├── <style>          — 全部 CSS（Design tokens → 组件）
├── <body>
│   ├── <nav>        — 顶部导航栏 + 语言切换
│   ├── .hero-section — Hero 区域（标题 + 搜索框 + 筛选器 + canvas 粒子）
│   ├── .cards-area  — 服务卡片区域
│   └── .footer-band — 页脚（引言 + 邮箱）
└── <script>
    ├── LANG{}       — 双语文案对象
    ├── SITES[]      — 54 个服务点数据
    ├── POSTCODES{}  — SA 邮编坐标表
    ├── SUBURBS{}    — 郊区名称 → 邮编映射
    ├── geocode()    — 三层地理编码
    ├── render()     — 卡片渲染与距离逻辑
    ├── Scroll reveal — 滚动渐显动画
    └── Leaf canvas  — 树叶粒子系统
```

---

## 致谢 / Acknowledgements

感谢所有在南澳大利亚默默提供食物援助的机构和志愿者。
此网站的诞生，是希望语言和信息不再成为获取帮助的障碍。

*This site was built to ensure that language and information are never a barrier to finding help.*

---

## 联系 / Contact

📬 yunziluo520@gmail.com
