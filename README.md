# DatabaseReleases

此仓库包含 EhTagTranslation 数据库的发布版本。

## 同步流程

此仓库通过 GitHub Actions 自动与 [EhTagTranslation/Database](https://github.com/EhTagTranslation/Database) 的 `release` 分支同步。

### 自动同步

同步流程运行于：
- **每 6 小时** 通过定时工作流
- **按需** 通过手动工作流调度
- **被触发时** 通过 Database 仓库的 repository_dispatch

### 工作原理

1. **变更检测**：比较存储在 `sha` 文件中的 SHA 与 Database release 分支上的最新提交
2. **文件同步**：如果检测到变更，从 Database release 分支下载所有文件
3. **安全更新**：保留仓库特定文件（`.github/`、`.gitignore`、`README.md`）
4. **提交**：创建新提交并引用源 Database 提交

### 手动同步

手动触发同步：

1. 前往 [Actions 标签页](../../actions)
2. 选择"Sync from Database Release Branch"工作流
3. 点击"Run workflow"

### 权限

工作流使用具有 `contents: write` 权限的 `GITHUB_TOKEN`：
- 从 Database 仓库获取（公开，无需认证）
- 提交并推送变更到此仓库

### 文件

仓库包含以下数据库文件：
- `db.ast.js` / `db.ast.json` - AST 格式数据库
- `db.full.js` / `db.full.json` - 包含所有字段的完整数据库
- `db.html.js` / `db.html.json` - HTML 格式数据库
- `db.raw.js` / `db.raw.json` - 原始数据库格式
- `db.text.js` / `db.text.json` - 纯文本数据库
- `*.gz` 文件 - JSON 文件的压缩版本
- `sha` - 包含来源 Database 仓库的提交哈希

## 使用方法

这些文件可以直接用于 Web 应用程序或下载离线使用。有关数据格式和使用说明的文档，请参阅 [主 Database 仓库](https://github.com/EhTagTranslation/Database)。