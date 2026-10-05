# Win Software 软件清单导航（Win-software-WPD）

一个**软件装机清单导航站**：左侧分类树、右侧卡片网格，点击软件名查看该软件的完整信息与下载地址。数据用 CSV 维护——**改一行 CSV，页面自动更新**。换电脑时按分类找回以前用过的软件、查看用途并下载。

## 特性

- pintree 风格：左侧分类树 + 右侧卡片网格
- 点击软件名 → 右侧滑出详情面板（版本 / 厂商 / 安装方式 / 官网 / 多下载地址 / 备注）
- 卡片显示：图标 + 软件名 + 一句话说明 + 下载按钮（+备用地址标记 / 必备徽章）
- 搜索：按名称 / 用途 / 厂商模糊过滤
- 图标自动抓取官网 favicon，失败自动降级为首字母色块（也可在 CSV「图标」列填图床链接）
- 明暗主题切换、移动端适配（抽屉侧栏 + 双列卡片）

## 文件结构

```
Win-software-WPD/
├── index.html       # 页面（单文件自包含，无构建步骤）
├── 软件清单.csv      # 数据（UTF-8 with BOM）
└── README.md
```

## 维护方法

1. 用 Excel / WPS 打开 `软件清单.csv`（保存时务必选「CSV UTF-8」格式，否则中文会乱码）
2. 增删行、修改内容、拖动行调整顺序（**CSV 行顺序 = 页面展示顺序**）
3. 刷新页面即生效，无需任何构建

### 字段说明

| 列 | 说明 | 备注 |
|---|---|---|
| 软件名称 | 必填，展示与搜索用 | |
| 分类 | 必填，格式「emoji + 空格 + 分类名」，如 `📄 办公效率` | 决定左侧分类树与分类图标 |
| 用途说明 | 一句话说明，卡片小字展示 | 可选 |
| 版本 | 当前安装版本 | 可选 |
| 厂商 | 开发商 | 可选 |
| 安装方式 | 如「绿色免安装」 | 可选 |
| 优先级 | 填 `必备` 显示黄色徽章 | 可选 |
| 官网 | 官网链接 | 可选 |
| 下载地址1/2/3 | 下载链接，支持维护多个备用地址防止失效 | 可选 |
| 图标 | 图标图床链接（留空则自动抓官网 favicon） | 可选 |
| 备注 | 补充说明 | 可选 |

## 本地预览

```bash
python -m http.server 8899
# 浏览器打开 http://localhost:8899
```

## 部署到 GitHub Pages

1. 在 GitHub 新建仓库（如 `Win-software-WPD`，Public）
2. 本地执行：

```bash
git remote remove origin
git remote add origin https://github.com/<你的用户名>/Win-software-WPD.git
git add .
git commit -m "软件清单导航站"
git branch -M main
git push -u origin main
```

3. 仓库 **Settings → Pages → Branch 选 `main` → 保存**
4. 几分钟后访问：`https://<你的用户名>.github.io/Win-software-WPD/`

> 提示：发布只需 `index.html` + `软件清单.csv` 两个文件；`.git` 是本地版本库，不会被推送到仓库文件列表中。
