# Cursor GitHub MCP 集成教程

本教程将指导您如何在 Cursor 编辑器中设置 GitHub MCP (Model Context Protocol) 服务器，以便直接在 Cursor 中使用 GitHub 功能。

## 目录

1. [前提条件](#前提条件)
2. [创建 GitHub 账户](#创建-github-账户)
3. [生成 GitHub 个人访问令牌](#生成-github-个人访问令牌)
4. [在 Cursor 中配置 MCP 服务器](#在-cursor-中配置-mcp-服务器)
5. [验证 MCP 服务器设置](#验证-mcp-服务器设置)
6. [使用 GitHub MCP 功能](#使用-github-mcp-功能)
7. [常见问题与解决方案](#常见问题与解决方案)

## 前提条件

- 已安装 Cursor 编辑器
- 稳定的网络连接
- GitHub 账户（如果没有，将在下一步创建）

## 创建 GitHub 账户

如果您已经有 GitHub 账户，可以跳过此步骤。

1. 访问 [GitHub 官网](https://github.com/)
2. 点击 "Sign up" 按钮
3. 按照提示填写用户名、电子邮件和密码
4. 完成验证步骤
5. 选择适合您的计划（免费计划足够使用）
6. 完成账户设置

## 生成 GitHub 个人访问令牌

为了让 Cursor 能够访问您的 GitHub 账户，您需要创建一个个人访问令牌 (Personal Access Token, PAT)：

1. 登录 GitHub 后，点击页面右上角的头像，选择 "Settings"
   
2. 在左侧菜单中选择 "Developer settings"
   
3. 点击左侧菜单中的 "Personal access tokens"，然后选择 "Fine-grained tokens"
   
4. 点击 "Generate new token" 按钮
   
5. 为令牌设置以下信息：
   - 名称：输入一个描述性名称，如 "cursor-mcp"
   - 过期时间：根据需要选择（建议选择较长时间，如 90 天或 1 年）
   - 权限范围：至少选择以下权限：
     - `repo`（所有仓库权限）
     - `workflow`（如果需要操作 GitHub Actions）
   
6. 点击页面底部的 "Generate token" 按钮
   
7. **重要**：生成后立即复制显示的令牌，因为它只会显示一次！

## 在 Cursor 中配置 MCP 服务器

现在您已经有了个人访问令牌，接下来在 Cursor 中设置 MCP 服务器：

1. 打开 Cursor 编辑器
   
2. 点击左上角的 "Cursor Settings"（Cursor 设置）
   
3. 在设置面板中，找到并点击左侧的 "MCP" 选项
   
4. 点击 "Add new MCP server" 按钮
   
5. 在弹出的对话框中填写以下信息：
   - Name：输入 "github"（或您喜欢的任何名称）
   - Type：选择 "command"
   - Command：**不要**直接粘贴您的个人访问令牌！而是使用以下命令格式：
     ```
     C:\Windows\System32\cmd.exe /c npx -y @smithery/cli@latest run @smithery-ai/github --config "{"githubPersonalAccessToken":"YOUR_TOKEN_HERE"}"
     ```
     将 `YOUR_TOKEN_HERE` 替换为您之前复制的个人访问令牌
   
6. 点击 "Add" 按钮完成添加

## 验证 MCP 服务器设置

添加 MCP 服务器后，您应该看到它在 MCP 列表中显示为已启用状态：

1. 在 MCP 设置页面中，确认您的 GitHub 服务器显示为 "Enabled"
   
2. 您应该能看到可用的工具列表，包括：
   - create_or_update_file
   - search_repositories
   - create_repository
   - get_file_contents
   - 等其他 GitHub 相关功能

## 使用 GitHub MCP 功能

成功配置后，您可以在 Cursor 中直接使用 GitHub 功能：

1. 在 Cursor 中打开聊天面板
   
2. 您可以使用以下命令示例：
   - 创建新仓库：`创建一个名为 my-new-project 的 GitHub 仓库`
   - 搜索仓库：`搜索关于 React 的热门仓库`
   - 获取文件内容：`获取 username/repo 仓库中 main 分支上 README.md 的内容`

## 常见问题与解决方案

### 问题：MCP 服务器显示 "Failed to create client"

**解决方案**：
- 检查您的个人访问令牌是否正确
- 确保命令格式正确，特别是 JSON 配置部分
- 尝试使用 Smithery 网站上提供的确切命令格式

### 问题：无法使用某些 GitHub 功能

**解决方案**：
- 检查您的个人访问令牌是否具有所需的权限
- 在 GitHub 设置中更新令牌权限
- 确保 Cursor 和 GitHub 之间的网络连接正常

### 问题：Windows 系统特定问题

**解决方案**：
- 对于 Windows 用户，请使用 Smithery 网站上提供的 Windows 特定命令：
  ```
  cmd /c npx -y @smithery/cli@latest run @smithery-ai/github
  ```
  或
  ```
  C:\Windows\System32\cmd.exe /c npx -y @smithery/cli@latest run @smithery-ai/github
  ```

## 安全注意事项

- 个人访问令牌具有访问您 GitHub 账户的权限，请妥善保管
- 定期更新您的个人访问令牌
- 如果怀疑令牌泄露，立即在 GitHub 中撤销并生成新的令牌
- 仅授予令牌必要的最小权限

---

希望本教程对您有所帮助！如有任何问题，请参考 [Cursor 官方文档](https://cursor.sh/docs) 或 [GitHub 文档](https://docs.github.com/en)。