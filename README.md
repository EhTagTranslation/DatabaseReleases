# DatabaseReleases 自动化配置

此分支包含用于自动镜像 [EhTagTranslation/Database](https://github.com/EhTagTranslation/Database) `release` 分支到 `master` 分支的 GitHub Actions 工作流。

## 镜像策略

`master` 分支是 Database/release 分支的直接镜像，不保留历史记录。每次更新时会完全替换 master 分支的内容。

## 自动镜像流程

镜像流程运行于：
- **每 6 小时** 通过定时工作流
- **按需** 通过手动工作流调度  
- **被触发时** 通过 Database 仓库的 repository_dispatch

### 工作原理

1. **变更检测**：比较 master 分支当前 SHA 与 Database release 分支上的最新提交
2. **完整镜像**：如果检测到变更，创建全新的 master 分支内容，完全替换现有内容
3. **强制推送**：使用 force push 将 Database/release 的内容推送到 master，不保留历史
4. **提交信息**：引用源 Database 提交的哈希和消息

### 手动触发镜像

手动触发镜像：

1. 前往 [Actions 标签页](../../actions)
2. 选择"Mirror Database Release Branch to Master"工作流
3. 点击"Run workflow"

### 分支结构

- **master** - Database/release 的直接镜像，包含所有数据库文件
- **当前分支** - 包含工作流配置和文档的自动化分支

### 数据库文件

master 分支包含以下数据库文件：
- `db.ast.js` / `db.ast.json` - AST 格式数据库
- `db.full.js` / `db.full.json` - 包含所有字段的完整数据库  
- `db.html.js` / `db.html.json` - HTML 格式数据库
- `db.raw.js` / `db.raw.json` - 原始数据库格式
- `db.text.js` / `db.text.json` - 纯文本数据库
- `*.gz` 文件 - JSON 文件的压缩版本
- `sha` - 包含来源 Database 仓库的提交哈希

## 使用方法

从 master 分支获取最新的数据库文件用于 Web 应用程序或下载离线使用。有关数据格式和使用说明的文档，请参阅 [主 Database 仓库](https://github.com/EhTagTranslation/Database)。