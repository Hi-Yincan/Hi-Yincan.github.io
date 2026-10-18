# hyc.ac 发布入口

本站的完整产品源码、Issues、PR 和上游升级历史位于 [Hi-Yincan/LifeOS](https://github.com/Hi-Yincan/LifeOS)。此仓库仅保存 GitHub Pages 发布配置，保持 hyc.ac 根域名及 blog/gallery 项目站入口。

## 仓库内容

- `deployment.json`：来源仓库及固定的完整提交 SHA。
- `.github/workflows/deploy.yml`：检出、构建、验证和手动发布。
- 本说明：职责与回退方法。

不使用模板或 Git submodule；CI 临时检出 LifeOS，源码、依赖和构建产物不提交到此仓库。读取公开源码使用工作流自带的只读权限，无需额外长期 token。

## 发布

1. 在 LifeOS 完成功能、合并和产品 CI。
2. 将此仓库 `deployment.json` 的 commit 更新为已验证的 LifeOS **40 位完整 SHA**，评审后提交 main。
3. 在 Actions 手动运行 **Publish visitor OS**。`deploy=false` 只构建验证；`deploy=true` 才部署。普通 push 不自动上线。
4. 工作流使用固定 Node/Yarn，完成访客构建、lint、单元/服务和浏览器测试。只上传 `source/out`，包含所需 `.index`；不会上传运行目录或密钥。
5. 检查 https://hyc.ac/release.json 的源码及发布配置 SHA，验证首页、作品集、商店、设置、https://hyc.ac/blog/ 和 https://hyc.ac/gallery/。

Pages 使用 GitHub Actions 模式，自定义域名在本仓库 Pages 设置中为 `hyc.ac`。域名现有 DNS 保持不变；LifeOS 源码仓库不再直接托管生产 Pages。部署 job 使用 pages:write + OIDC；构建 job 不获得 Pages 写权限。

## 回退

将 deployment.json 恢复到已验证的 LifeOS SHA，提交 main 后手动发布。已知首次 OS 版本为 `86620989ec6446ab55aba0a16c237a200254bfb1`。产物保留 30 天，部署日志与线上 release.json 用于追踪版本。不要强推 main 或改 DNS 来回退代码。

旧首页 pages-live 分支保留于 LifeOS，此发布仓库没有该分支。生产使用静态展示版；LifeOS 已取消站点管理员功能，所有浏览者读取相同内容。独立信息源管理与真实看板数据接入继续单独规划。完整范围和限制见 [LifeOS 发布手册](https://github.com/Hi-Yincan/LifeOS/blob/main/specs/deployment/pages.md)。

## 历史链接

原 Hi-Yincan.github.io 仓库已改名为 LifeOS。旧的 Issue、PR、源码链接请把仓库名改为 LifeOS；本仓库不承接原 Issue 编号，外部旧收藏不会自动重定向。
