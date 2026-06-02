# 西方古典音乐史 · Western Classical Music History

一个交互式的西方古典音乐导览：从文艺复兴到二十世纪，**28 位作曲家**、跨越五个时期的生平、代表作与可直接播放的 Spotify 链接，串联成一条可浏览的音乐时间线。

> 纯前端、零构建。克隆下来用浏览器打开 `index.html` 即可运行。

## 特点

- **时间线导览** —— 28 位作曲家按时期（文艺复兴 / 巴洛克 / 古典 / 浪漫 / 二十世纪）排列，从若斯坎（Josquin）到格拉斯（Glass）。
- **作曲家详情页** —— 生平简介、所属时期、生卒年，以及精选代表作。
- **一键试听** —— 每部作品都对应一条经过校准的 Spotify 曲目链接（单一数据源，直达播放）。
- **数据驱动** —— 所有内容存于 `data/*.json`，新增或修改作曲家无需改动页面逻辑。
- **响应式** —— 移动端将时间线降级为纵向列表，桌面端为横向时间轴。
- **暗金配色** —— Playfair Display + Lato 字体，深色背景配金色点缀。

## 运行

无需安装依赖、无需构建步骤：

```bash
# 直接打开
open index.html

# 或用任意静态服务器（推荐，避免 file:// 的跨域限制）
python3 -m http.server 8000
# 然后访问 http://localhost:8000
```

## 项目结构

```
.
├── index.html          # 首页：时期时间线 + 作曲家导航
├── composer.html       # 作曲家详情页（按 ?id= 参数渲染）
├── data/
│   ├── composers_list.json      # 28 位作曲家的排序索引
│   ├── <composer>.json          # 每位作曲家：生平、时期、代表作
│   └── spotify_canonical_map.json  # 作品 → Spotify 曲目的权威映射
├── js/
│   └── canonical-spotify.js     # 加载并注入 Spotify 链接
└── scripts/            # 构建 Spotify 映射的辅助脚本（Python）
```

## 数据格式

每位作曲家一个 JSON 文件，例如 `data/bach.json`：

```json
{
  "id": "bach",
  "name": "约翰·塞巴斯蒂安·巴赫",
  "nameEn": "Johann Sebastian Bach",
  "years": "1685 — 1750",
  "period": "巴洛克",
  "periodEn": "Baroque",
  "avatar": "B",
  "brief": "……生平简介……",
  "works": [ /* 代表作，含 Spotify 链接 */ ]
}
```

新增作曲家：放入一份 `data/<id>.json`，并把 `id` 加进 `data/composers_list.json` 的对应时期位置即可。

## 许可

[MIT](LICENSE)
