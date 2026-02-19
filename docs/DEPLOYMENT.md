# 部署指南

## Vercel 部署

### 1. 安装 Vercel CLI

```bash
npm install -g vercel
```

### 2. 登录 Vercel

```bash
vercel login
```

### 3. 部署项目

```bash
vercel
```

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

---

**环境变量**

本项目无需环境变量，完全静态部署。

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
