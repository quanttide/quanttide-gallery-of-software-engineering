# 命令行工具 API 设计风格

## 命令结构

各子系统应从领域中的对象和操作出发设计命令。命令层级从工具名起算。以 `qtcloud-media article render` 为例，`qtcloud-media` 是一级工具入口，`article` 是二级子命令，表示操作对象，`render` 是三级子命令，表示对该对象执行的动作。各子系统应按这一结构组织二、三级命令，使不同产品的命令行接口保持一致。

以新媒体运营为例，领域对象包括 `article`（文章）、`note`（图文）和 `video`（视频），常见动作包括 `publish`（发布）。动作名称应与实际行为一致。在媒体云中，`article push` 只将文章推送到公众号草稿箱。文章的正式发布由运营人员在公众号后台完成。

## API 文档审查

审查 AI 生成的命令行 API 文档时，应重点核对命令层级是否围绕领域对象和操作组织、命令名称是否符合使用者对实际行为的预期，以及文档示例中的命令及参数是否与实现一致。

## 版本发布

可以保持现有 API 兼容时，发布 patch 版本。需要破坏 API 兼容性时，`0.x` 可以通过 minor 版本发布破坏性变更。

媒体云 CLI 从 `0.1.5` 升到 `0.2.0` 时移除了旧命令入口，属于 `0.x` 的 minor 更新。仅修正 README 和内置技能中的命令示例时，API 保持兼容，这类修订归为 patch。

## 相关案例

- [媒体云 CLI 变更日志](https://github.com/quanttide/qtcloud-media/blob/4aa71108de8017221f4afba6bb5721a62bae476b/src/cli/CHANGELOG.md)
- [媒体云 CLI 文档与技能示例修订](https://github.com/quanttide/qtcloud-media/pull/2)
