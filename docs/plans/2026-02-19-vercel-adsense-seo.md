# Vercel 部署 + Google AdSense + SEO 优化实施计划

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**目标：** 将在线画图工具部署到 Vercel，添加 Google AdSense 广告位，并完成基础 SEO 优化。

**架构方案：**
- 保持现有静态 HTML/JS 结构不变
- 添加 Vercel 部署配置文件
- 在 HTML 中添加 SEO meta 标签和结构化数据
- 预留侧边栏广告位（等 AdSense 审核通过后嵌入代码）
- 创建 sitemap.xml 和 robots.txt

**技术栈：** Vercel (静态托管), Google AdSense, SEO Meta 标签, 结构化数据 (JSON-LD)

---

### Task 1: 创建 Vercel 配置文件

**文件：**
- Create: `vercel.json`

**步骤 1: 创建 vercel.json**

```json
{
  "version": 2,
  "public": true,
  "cleanUrls": true,
  "rewrites": [
    {
      "source": "/(.*)",
      "destination": "/index.html"
    }
  ],
  "headers": [
    {
      "source": "/JScript/(.*)",
      "headers": [
        {
          "key": "Cache-Control",
          "value": "public, max-age=31536000, immutable"
        }
      ]
    },
    {
      "source": "/Images/(.*)",
      "headers": [
        {
          "key": "Cache-Control",
          "value": "public, max-age=31536000, immutable"
        }
      ]
    },
    {
      "source": "/CSS/(.*)",
      "headers": [
        {
          "key": "Cache-Control",
          "value": "public, max-age=31536000, immutable"
        }
      ]
    },
    {
      "source": "/(.*)",
      "headers": [
        {
          "key": "X-Content-Type-Options",
          "value": "nosniff"
        },
        {
          "key": "X-Frame-Options",
          "value": "DENY"
        },
        {
          "key": "X-XSS-Protection",
          "value": "1; mode=block"
        }
      ]
    }
  ]
}
```

**步骤 2: 提交**

```bash
git add vercel.json
git commit -m "feat: 添加 Vercel 部署配置"
```

---

### Task 2: 添加 robots.txt

**文件：**
- Create: `public/robots.txt`

**步骤 1: 创建 public 目录和 robots.txt**

```bash
mkdir -p public
```

```txt
# robots.txt for zaixianhuatu.itzhouq.cn

User-agent: *
Allow: /

# 禁止爬取临时文件和系统目录
Disallow: /JScript/
Disallow: /Code/

# 站点地图
Sitemap: https://zaixianhuatu.itzhouq.cn/sitemap.xml
```

**步骤 2: 提交**

```bash
git add public/robots.txt
git commit -m "feat: 添加 robots.txt"
```

---

### Task 3: 添加 sitemap.xml

**文件：**
- Create: `public/sitemap.xml`

**步骤 1: 创建 sitemap.xml**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://zaixianhuatu.itzhouq.cn/</loc>
    <lastmod>2026-02-19</lastmod>
    <changefreq>weekly</changefreq>
    <priority>1.0</priority>
  </url>
</urlset>
```

**步骤 2: 提交**

```bash
git add public/sitemap.xml
git commit -m "feat: 添加 sitemap.xml"
```

---

### Task 4: 优化 index.html 的 SEO Meta 标签

**文件：**
- Modify: `index.html:1-43`

**步骤 1: 在 <head> 标签中添加 SEO 优化标签**

在 `<head>` 部分的第 2 行（`<html lang="en">` 后面，`<head>` 内部）添加以下内容：

```html
<!-- 基础 SEO -->
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<link rel="canonical" href="https://zaixianhuatu.itzhouq.cn/">

<!-- Open Graph / Facebook -->
<meta property="og:type" content="website">
<meta property="og:url" content="https://zaixianhuatu.itzhouq.cn/">
<meta property="og:title" content="在线画图 - 免费在线画图工具">
<meta property="og:description" content="简单易用的在线画图软件，支持多种画图功能，轻松创建精美的图形、插图和设计。">
<meta property="og:image" content="https://zaixianhuatu.itzhouq.cn/Images/og-preview.png">

<!-- Twitter -->
<meta property="twitter:card" content="summary_large_image">
<meta property="twitter:url" content="https://zaixianhuatu.itzhouq.cn/">
<meta property="twitter:title" content="在线画图 - 免费在线画图工具">
<meta property="twitter:description" content="简单易用的在线画图软件，支持多种画图功能，轻松创建精美的图形、插图和设计。">
<meta property="twitter:image" content="https://zaixianhuatu.itzhouq.cn/Images/og-preview.png">

<!-- 结构化数据 (JSON-LD) -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "WebApplication",
  "name": "在线画图工具",
  "url": "https://zaixianhuatu.itzhouq.cn/",
  "description": "简单易用的在线画图软件，支持多种画图功能，轻松创建精美的图形、插图和设计",
  "applicationCategory": "DesignApplication",
  "operatingSystem": "Any",
  "offers": {
    "@type": "Offer",
    "price": "0",
    "priceCurrency": "CNY"
  },
  "featureList": [
    "画笔工具",
    "铅笔工具",
    "橡皮擦",
    "形状绘制",
    "文本输入",
    "图层管理",
    "滤镜效果",
    "图像调整"
  ]
}
</script>
```

同时修改 `<html lang="en">` 为 `<html lang="zh-CN">`

**步骤 2: 提交**

```bash
git add index.html
git commit -m "feat: 添加 SEO meta 标签和结构化数据"
```

---

### Task 5: 创建广告位 CSS 样式

**文件：**
- Modify: `CSS/main.css`

**步骤 1: 在 main.css 末尾添加广告位样式**

```css
/* Google AdSense 广告位样式 */

/* 侧边栏广告容器 */
.ads-sidebar {
  position: fixed;
  right: 0;
  top: 100px;
  width: 160px;
  height: 600px;
  background-color: #f5f5f5;
  border: 1px solid #ddd;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 999;
}

/* 侧边栏广告占位内容 */
.ads-sidebar::before {
  content: "广告位 (160x600)";
  color: #999;
  font-size: 14px;
  text-align: center;
}

/* 响应式：小屏幕隐藏广告 */
@media (max-width: 1200px) {
  .ads-sidebar {
    display: none;
  }
}

/* 横向广告容器（备选位置） */
.ads-horizontal {
  width: 100%;
  height: 90px;
  background-color: #f5f5f5;
  border: 1px solid #ddd;
  margin: 10px 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.ads-horizontal::before {
  content: "广告位 (728x90)";
  color: #999;
  font-size: 14px;
}
```

**步骤 2: 提交**

```bash
git add CSS/main.css
git commit -m "feat: 添加 Google AdSense 广告位样式"
```

---

### Task 6: 在 index.html 中添加广告位容器

**文件：**
- Modify: `index.html`

**步骤 1: 在 </body> 标签前添加广告位容器**

在 `index.html` 文件的 `</body>` 闭合标签前添加：

```html
<!-- Google AdSense 广告位 -->
<div class="ads-sidebar" id="ads-sidebar">
  <!-- AdSense 代码将在此处添加，审核通过后替换 -->
</div>

<!-- AdSense 代码占位符 -->
<script>
  // Google AdSense 代码将在此处添加
  // 审核通过后，将以下注释替换为实际的 AdSense 代码
  /*
  (adsbygoogle = window.adsbygoogle || []).push({
    google_ad_client: "ca-pub-XXXXXXXXXXXXXXXX",
    enable_page_level_ads: true
  });
  */
</script>
```

**步骤 2: 提交**

```bash
git add index.html
git commit -m "feat: 添加 Google AdSense 广告位容器"
```

---

### Task 7: 创建部署文档

**文件：**
- Create: `docs/DEPLOYMENT.md`

**步骤 1: 创建部署文档**

```markdown
# 部署指南

## Vercel 部署

### 1. 安装 Vercel CLI

\`\`\`bash
npm install -g vercel
\`\`\`

### 2. 登录 Vercel

\`\`\`bash
vercel login
\`\`\`

### 3. 部署项目

\`\`\`bash
vercel
\`\`\`

按提示操作：
- Set up and deploy: Yes
- Which scope: 选择你的账号
- Link to existing project: No
- Project name: zaixianhuatu
- In which directory is your code located: ./
- Want to override settings: No

### 4. 配置自定义域名

在 Vercel 控制台中：
1. 进入项目设置
2. 选择 Domains
3. 添加域名: zaixianhuatu.itzhouq.cn
4. 按提示配置 DNS 记录

## Google AdSense 申请

### 1. 注册 AdSense

访问: https://www.google.com/adsense/

### 2. 添加网站

1. 登录 AdSense 后台
2. 添加网站: zaixianhuatu.itzhouq.cn
3. 等待审核（通常 1-2 周）

### 3. 添加广告代码

审核通过后：
1. 在 AdSense 后台创建广告单元
2. 复制广告代码
3. 替换 `index.html` 中的占位代码

### 4. 替换位置

- 侧边栏广告: 替换 `<div class="ads-sidebar">` 内的内容
- 代码位置: index.html 底部脚本区域

## SEO 优化清单

- [x] 添加 meta description
- [x] 添加 meta keywords
- [x] 添加 Open Graph 标签
- [x] 添加 Twitter Card 标签
- [x] 添加结构化数据 (JSON-LD)
- [x] 创建 robots.txt
- [x] 创建 sitemap.xml
- [ ] 提交 sitemap 到 Google Search Console
- [ ] 提交 sitemap 到百度站长平台

## 搜索引擎收录提交

### Google Search Console

1. 访问: https://search.google.com/search-console
2. 添加资源
3. 验证网站所有权
4. 提交 sitemap: https://zaixianhuatu.itzhouq.cn/sitemap.xml

### 百度站长平台

1. 访问: https://ziyuan.baidu.com/
2. 添加网站
3. 验证网站所有权
4. 提交 sitemap: https://zaixianhuatu.itzhouq.cn/sitemap.xml
\`\`\`

---

**环境变量**

本项目无需环境变量，完全静态部署。
\`\`\`

---

## 后续优化建议

1. **性能优化**
   - 压缩图片资源
   - 启用 Gzip 压缩（Vercel 自动处理）
   - 使用 CDN（Vercel 自动处理）

2. **内容优化**
   - 添加使用教程页面
   - 添加作品展示画廊
   - 添加常见问题 FAQ

3. **SEO 持续优化**
   - 定期更新 sitemap.xml
   - 监控 Search Console 数据
   - 优化关键词排名
```

**步骤 2: 提交**

```bash
git add docs/DEPLOYMENT.md
git commit -m "docs: 添加部署文档"
```

---

### Task 8: 更新项目 README

**文件：**
- Modify: `README.md`

**步骤 1: 更新 README 添加部署信息和 SEO 说明**

在 README.md 中添加或更新以下内容：

```markdown
## 部署

本项目部署在 Vercel 上: https://zaixianhuatu.itzhouq.cn

### 本地运行

直接用浏览器打开 \`index.html\` 即可使用，无需任何构建步骤。

### 部署到 Vercel

\`\`\`bash
npm install -g vercel
vercel login
vercel
\`\`\`

详细部署指南请参考 [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md)

## SEO

本项目已配置基础 SEO 优化：
- ✅ Meta 标签优化
- ✅ Open Graph 标签
- ✅ 结构化数据 (JSON-LD)
- ✅ Sitemap.xml
- ✅ Robots.txt

## 许可证

MIT License
```

**步骤 2: 提交**

```bash
git add README.md
git commit -m "docs: 更新 README 添加部署和 SEO 说明"
```

---

### Task 9: 创建 .gitignore 文件

**文件：**
- Create: `.gitignore`

**步骤 1: 创建 .gitignore**

```text
# Vercel
.vercel

# macOS
.DS_Store
.AppleDouble
.LSOverride

# Thumbnails
._*

# Editor
.vscode/
.idea/
*.swp
*.swo
*~

# Logs
*.log
npm-debug.log*

# Temporary files
*.tmp
*.temp
```

**步骤 2: 提交**

```bash
git add .gitignore
git commit -m "chore: 添加 .gitignore 文件"
```

---

### Task 10: 最终验证

**步骤 1: 验证所有文件已创建**

```bash
# 检查新增文件
ls -la vercel.json
ls -la public/
ls -la docs/

# 验证 HTML 语法（可选）
```

**步骤 2: 本地测试**

```bash
# 在浏览器中打开 index.html
open index.html
```

检查：
1. 页面正常显示
2. 广告位占位符在右侧显示
3. 控制台无 JS 错误

**步骤 3: 提交所有更改**

```bash
git status
git add .
git commit -m "chore: 完成所有配置更改"
```

**步骤 4: 推送到远程仓库**

```bash
git push origin master
```

---

## 部署后检查清单

### Vercel 部署后

- [ ] 确认网站可访问
- [ ] 确认所有静态资源加载正常
- [ ] 确认广告位显示正常（占位符）
- [ ] 检查 /robots.txt 可访问
- [ ] 检查 /sitemap.xml 可访问

### SEO 检查

- [ ] 使用 Google Rich Results Test 验证结构化数据
- [ ] 使用 Facebook Sharing Debugger 检查 Open Graph
- [ ] 使用 Twitter Card Validator 检查 Twitter Card

### 下一步

1. **申请 Google AdSense** - 提交网站等待审核
2. **提交搜索引擎收录** - Google Search Console + 百度站长
3. **监控数据** - 使用 Vercel Analytics 查看访问数据

---

## 快速命令参考

```bash
# 本地测试
open index.html

# 部署到 Vercel
vercel --prod

# 查看 Vercel 日志
vercel logs

# 重新部署
vercel --prod --force
```
