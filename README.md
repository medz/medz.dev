# medz.dev

Seven 的个人网站。Astro 静态生成，中英文、明暗主题、自适应布局；字体随站点托管，无客户端框架。

## 开发

需要 Node.js 24 或更新版本。

```sh
npm ci
npm run dev
```

```sh
npm run verify  # 类型检查、构建、链接与双语路由检查
npm run preview # 查看构建结果
```

## 内容

- `src/data/projects.json`：项目仓库、分类、中英文介绍和上游文档链接。
- `src/data/github.json`：GitHub 元数据快照，可用 `npm run sync:projects` 更新。
- `src/components/pages/`：首页、项目列表、项目主页和简历。
- `src/styles/site.css`：布局、主题与动效。

项目按默认分支最近一次提交排序，首页取前四个。构建时从 GitHub 获取 Stars、语言、许可证和更新时间；请求失败则保留快照。可选 `GITHUB_TOKEN` 仅用于构建，不进入浏览器。当前文档链接指向上游，跨仓库 MDX 文档和目录规则后续单独设计。

中文使用 `/`、`/projects/`、`/resume/`、`/<project>/`，英文使用对应的 `/en/` 路径。语言切换保留当前页面。主题默认跟随系统，手动选择保存到本地；减少动态效果的系统设置会禁用入场和切换动画。

## 部署

推送到 `main` 或手动运行 **Site** 工作流会更新元数据、验证并部署到 GitHub Pages。Pull request 只运行构建验证。元数据不定时轮询，手动运行工作流即可刷新。

GitHub Pages 的发布源设为 **GitHub Actions**，自定义域名设为 `medz.dev`。`public/CNAME` 与 Astro 的 `site` 保持一致。Cloudflare 将根域和 `www` 代理到 `medz.github.io`，使用 **Full (strict)** TLS；域名切换前应确认 Pages 部署及证书已就绪。

静态资源带内容哈希，页面无需服务端运行时。`npm run verify` 检查生成页面的语言、链接、资源、站点地图，并报告压缩后的客户端脚本体积。
