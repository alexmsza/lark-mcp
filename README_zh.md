# Lark MCP

<p align="right">
    <a href="./README.md">English</a> | <b>简体中文</b>
</p>

[![GitHub last commit](https://img.shields.io/github/last-commit/ZhanZiyuan/lark-mcp)](https://github.com/ZhanZiyuan/lark-mcp/commits/main/)
[![GitHub License](https://img.shields.io/github/license/ZhanZiyuan/lark-mcp)](https://github.com/ZhanZiyuan/lark-mcp/blob/main/LICENSE)
[![GitHub Downloads (all assets, all releases)](https://img.shields.io/github/downloads/ZhanZiyuan/lark-mcp/total)](https://github.com/ZhanZiyuan/lark-mcp/releases)

本项目通过MCP（Model Context Protocol）将官方飞书（Lark）服务集成到Gemini CLI中。
您可以通过自然语言或自定义命令在终端中直接管理飞书文档、查询日程、搜索知识库以及查找联系人。

## 功能特性

- **文档管理**：读取和总结飞书文档内容。
- **搜索**：支持在知识库（Wiki）、聊天记录或云文档中进行精准搜索。
- **日程管理**：查询个人主日历和日程安排。
- **通讯录**：查找员工信息、部门及联系方式。

## 前置要求

- **Node.js**：请确保系统已安装Node.js环境。
- **Gemini CLI**：请确保已安装最新版本的Gemini CLI。
- **飞书/Lark账号**：需要拥有飞书租户的访问权限。

## 安装步骤

- 创建一个目录（例如 `lark-mcp`）并将本项目文件放入其中。
- 在终端中进入该目录。

## 配置说明 (重要)

在使用扩展之前，您**必须**在`gemini-extension.json`文件中配置您的飞书开放平台凭证。
这是MCP服务器连接飞书API的必要条件。

- 打开`gemini-extension.json`文件。
- 找到`mcpServers`下的`args`数组。
- 将其中的占位符替换为您实际的应用凭证。

  ```json
  {
    "name": "lark-mcp",
    "version": "1.0.0",
    "description": "A Gemini CLI extension for Lark's MCP server.",
    "contextFileName": "GEMINI.md",
    "mcpServers": {
      "lark-mcp": {
        "command": "npx",
        "args": [
          "-y",
          "@larksuiteoapi/lark-mcp",
          "mcp",
          "-a",
          "<your_app_id>",
          "-s",
          "<your_app_secret>",
          "-u",
          "<your_user_token>"
        ]
      }
    }
  }
  ```

**如何获取凭证：**

- **App ID 和 App Secret**：
  - 登录[飞书开发者后台](https://open.feishu.cn/app)。
  - 创建企业自建应用或选择已有应用。
  - 在“基本信息” -> “凭证与基础信息”页面可以找到**App ID**和**App Secret**。

- **User Token (用户访问凭证)**：
  - 为了快速测试，您可以使用API调试台生成临时Token。
  - 访问[飞书API调试台](https://open.feishu.cn/document/server-docs/docs/bitable-v1/app/create)（或任意API文档页面的调试工具）。
  - 点击调试界面上的**获取 Token**按钮，生成当前用户的`user_access_token`。
  - 将生成的Token复制并替换`<your_user_token>`。

## 启用扩展

完成配置文件的修改后，运行以下命令将扩展链接到Gemini CLI：

```bash
gemini extensions link .
```

或者通过以下命令安装：

```bash
gemini extensions install https://github.com/ZhanZiyuan/lark-mcp
```

运行完成后，请重启您的Gemini CLI会话以加载新配置。

## 使用指南

### 自然语言交互

您可以直接用自然语言向Gemini提问：

- “帮我搜一下知识库里关于项目启动的文档。”
- “我今天的日程安排是什么？”
- “查找一下[员工姓名]的联系方式。”

### 自定义命令

为了操作更安全且便捷，本扩展提供了一系列快捷指令（侧重于只读操作）：

- **/lark:agenda**：查询日程。
  - 用法：`/lark:agenda`或`/lark:agenda "下周一"`

- **/lark:search-wiki**：搜索知识库（Wiki）。
  - 用法：`/lark:search-wiki "Q3 季度报告"`

- **/lark:search-chat**：搜索聊天记录。
  - 用法：`/lark:search-chat "修复 bug"`

- **/lark:whois**：查找员工信息。
  - 用法：`/lark:whois "张三"`

- **/lark:read-doc**：读取特定文档内容。
  - 用法：`/lark:read-doc "[文档 Token 或 URL]"`

## 故障排除

如果扩展没有响应或报错，请检查以下几点：

- **凭证检查**：确认`gemini-extension.json`中的App ID/Secret正确，且User Token未过期。
- **权限检查**：确保您的飞书应用在开发者后台已开通必要的权限（如日历、文档、搜索、通讯录等权限）。
- **重新链接**：如果您移动了文件夹位置，请重新运行`gemini extensions link .`。

---

*基于[Gemini CLI扩展指南](https://geminicli.com/docs/extensions/getting-started-extensions/)与[飞书OpenAPI MCP](https://github.com/larksuite/lark-openapi-mcp/blob/main/README_ZH.md)构建。*
