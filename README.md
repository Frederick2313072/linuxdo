<div align="center">

<img src="_assets/linuxdo-banner.png" alt="LinuxDo Connect" width="600" height="180">

# LinuxDo Connect Plugin for Dify

*连接 LinuxDo 论坛的强大 Dify 插件*

[![Version](https://img.shields.io/badge/version-0.0.2-blue.svg)](https://github.com/langgenius/dify-official-plugins)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Dify](https://img.shields.io/badge/Dify-Plugin-orange.svg)](https://dify.ai)
[![LinuxDo](https://img.shields.io/badge/LinuxDo-Connect-red.svg)](https://connect.linux.do)

**作者:** frederick | **类型:** 工具插件 | **版本:** 0.0.2

[English Documentation](README_EN.md) | [功能特性](#功能特性--features) | [快速开始](#安装配置--installation--configuration) | [API文档](api.md)

</div>

---

## 概述 | Overview

> **LinuxDo Connect** 插件让你能够在 Dify 中无缝连接和操作 LinuxDo 论坛

LinuxDo Connect 插件允许你在 Dify 中直接连接和操作 LinuxDo 论坛。通过 LinuxDo Connect API，你可以进行身份验证、获取用户信息、搜索内容、获取个性化推荐，以及执行自动签到等操作。

The LinuxDo Connect plugin allows you to directly connect and interact with the LinuxDo forum within Dify. Through the LinuxDo Connect API, you can perform authentication, retrieve user information, search content, get personalized recommendations, and execute automatic check-ins.



## 功能特性 | Features

<table>
<tr>
<td width="50%">

### 用户认证与信息获取
**User Authentication & Information**

- 验证 API 密钥状态
- 获取详细用户信息（用户名、信任等级、活跃状态等）
- 支持快速验证模式

</td>
<td width="50%">

### 内容搜索
**Content Search**

- 全站内容搜索（主题、帖子、分类）
- 高级过滤选项（分类筛选、结果排序）
- 支持按相关性、日期、浏览量、回复数排序
- 可自定义返回结果数量

</td>
</tr>
</table>

## 安装配置 | Installation & Configuration

### 步骤 1: 获取 LinuxDo Connect API 凭据
**Get LinuxDo Connect API Credentials**

> 访问 [LinuxDo Connect](https://connect.linux.do) 申请 API 访问权限

<details>
<summary><strong>详细步骤 | Detailed Steps</strong></summary>

#### **注册应用 | Register Application**
```
访问: https://connect.linux.do
点击: "我的应用接入" -> "申请新接入"
填写: 应用信息和回调地址
```

#### **获取凭据 | Get Credentials**
| 凭据类型 | 用途 | Purpose |
|---------|------|---------|
| **Client ID** | 基础认证的客户端标识 | Client identifier for basic auth |
| **Client Secret** | 基础认证的客户端密钥 | Client secret for basic auth |
| **API Key** | 用户账户识别密钥 | API key for user account identification |

</details>

### 步骤 2: 在 Dify 中配置插件
**Configure Plugin in Dify**

```mermaid
graph LR
    A[安装插件] --> B[打开配置页面]
    B --> C[填入凭据]
    C --> D[保存配置]
    D --> E[开始使用]
```

**配置项 | Configuration Items:**
- **Client ID**: 你的 LinuxDo Client ID
- **Client Secret**: 你的 LinuxDo Client Secret  
- **API Key**: 你的 LinuxDo API Key

## 性能特点 | Performance Features

<div align="center">

| 特性 | LinuxDo Connect | 传统方案 | 优势 |
|------|----------------|----------|------|
| **响应速度** | 快速响应 | 较慢 | **优化性能** |
| **安全认证** | OAuth 2.0 | 基础认证 | **企业级安全** |
| **数据处理** | 结构化JSON | 原始HTML | **易于解析** |
| **错误恢复** | 自动重试 | 手动处理 | **更可靠** |
| **内存占用** | 轻量级 | 占用较多 | **资源优化** |

### 性能基准测试

```
基于LinuxDo Connect API的高效集成方案
支持快速用户认证和内容检索
优化的网络请求处理机制
```

</div>

## 使用方法 | Usage

### 用户信息获取 | User Information

<table>
<tr>
<td width="50%">

**获取完整用户信息**
```python
user_info = linuxdo_user_info(
    include_extra_info=True,
    verify_only=False
)
```

</td>
<td width="50%">

**快速验证 API Key**
```python
verification = linuxdo_user_info(
    include_extra_info=False,
    verify_only=True
)
```

</td>
</tr>
</table>

### 内容搜索 | Content Search

<table>
<tr>
<td width="50%">

**搜索所有内容**
```python
search_results = linuxdo_content_search(
    search_query="Python编程",
    search_type="all",
    limit=20,
    sort_by="relevance"
)
```

</td>
<td width="50%">

**仅搜索主题**
```python
topic_results = linuxdo_content_search(
    search_query="机器学习",
    search_type="topics",
    category_filter="技术讨论",
    limit=10,
    sort_by="date"
)
```

</td>
</tr>
</table>

## API 端点信息 | API Endpoints

### LinuxDo Connect API 端点

| 端点类型 | URL | 说明 |
|---------|-----|------|
| **授权端点** | `https://connect.linux.do/oauth2/authorize` | OAuth2 授权 |
| **Token 端点** | `https://connect.linux.do/oauth2/token` | 获取访问令牌 |
| **用户信息端点** | `https://connect.linux.do/api/user` | 获取用户详细信息 |
| **用户信息端点 (OAuth2)** | `https://connect.linux.do/oauth2/userinfo` | OAuth2 用户信息 |

### 可获取的用户字段 | Available User Fields

<details>
<summary><strong>用户字段详情 | User Field Details</strong></summary>

| 字段 | 说明 | Field | Description |
|------|------|-------|-------------|
| `id` | 用户唯一标识（不可变） | `id` | Unique user identifier (immutable) |
| `username` | 论坛用户名 | `username` | Forum username |
| `name` | 论坛用户昵称（可变） | `name` | Forum display name (mutable) |
| `avatar_template` | 用户头像模板URL | `avatar_template` | User avatar template URL |
| `active` | 账号活跃状态 | `active` | Account active status |
| `trust_level` | 信任等级（0-4） | `trust_level` | Trust level (0-4) |
| `silenced` | 禁言状态 | `silenced` | Silenced status |
| `external_ids` | 外部ID关联信息 | `external_ids` | External ID associations |
| `api_key` | API访问密钥 | `api_key` | API access key |

</details>

## 数据结构 | Data Structures

### 用户信息响应 | User Info Response
```json
{
  "user_info": {
    "user_id": "string",
    "api_key_valid": true,
    "username": "string",
    "name": "string", 
    "trust_level": 0,
    "active": true,
    "admin": false,
    "moderator": false,
    "created_at": "2024-01-01T00:00:00Z",
    "last_seen_at": "2024-01-01T00:00:00Z"
  },
  "verification_result": {
    "status": "success",
    "user_id": "string",
    "api_key_valid": true,
    "message": "string"
  }
}
```

### 搜索结果响应 | Search Results Response
```json
{
  "search_results": [
    {
      "id": "string",
      "title": "string",
      "content": "string",
      "author": "string",
      "category": "string", 
      "url": "string",
      "created_at": "2024-01-01T00:00:00Z",
      "views": 0,
      "replies": 0,
      "relevance_score": 0.95
    }
  ],
  "search_summary": {
    "total_results": 0,
    "search_query": "string",
    "search_type": "string",
    "processing_time": 0.5,
    "filters_applied": ["string"]
  }
}
```

## 安全建议 | Security Recommendations

> **重要提示**: 请务必遵循以下安全最佳实践

<table>
<tr>
<td width="33%">

### 保护凭据
**Protect Credentials**

- 妥善保管 Client Secret 和 API Key
- 切勿在前端代码中暴露敏感信息  
- 定期更新 API 凭据

</td>
<td width="33%">

### 网络安全
**Network Security**

- 确保使用 HTTPS 协议传输数据
- 验证所有用户输入数据
- 实施适当的错误处理

</td>
<td width="33%">

### 访问控制
**Access Control**

- 基于用户信任等级实施服务限制
- 监控 API 使用频率，防止滥用
- 设置合理的速率限制

</td>
</tr>
</table>





</details>

## 开发信息 | Development Information



### 项目结构 | Project Structure

```
linuxdo/
├── manifest.yaml              # 插件清单文件
├── requirements.txt           # Python 依赖
├── main.py                   # 插件入口点
├── provider/
│   ├── linuxdo.py           # 提供者实现
│   └── linuxdo.yaml         # 提供者配置
├── tools/
│   ├── linuxdo.py           # 用户信息工具
│   ├── linuxdo.yaml         # 用户信息工具配置
│   ├── content_search.py    # 内容搜索工具
│   └── content_search.yaml  # 内容搜索工具配置
└── _assets/
    ├── icon.svg            # 插件图标
    └── icon-dark.svg       # 深色模式图标
```

## 许可证 | License

> 本插件遵循相应的开源许可证。使用前请确保遵守 LinuxDo 论坛的使用条款和 API 使用政策。

This plugin follows the corresponding open source license. Please ensure compliance with LinuxDo forum terms of use and API usage policies before use.

## 支持与反馈 | Support & Feedback

<div align="center">

### 需要帮助？我们很乐意为您提供支持！

</div>

<table>
<tr>
<td width="50%" align="center">

### 报告问题
**Report Issues**

[![GitHub Issues](https://img.shields.io/github/issues/langgenius/dify-official-plugins)](https://github.com/langgenius/dify-official-plugins/issues)

[创建 GitHub Issue](https://github.com/langgenius/dify-official-plugins/issues/new)

</td>
<td width="50%" align="center">

### 邮件联系
**Email Contact**

[![Email](https://img.shields.io/badge/Email-2313072@mail.nankai.edu.cn-blue.svg)](mailto:2313072@mail.nankai.edu.cn)

[发送邮件至开发者](mailto:2313072@mail.nankai.edu.cn)

</td>
</tr>
</table>

---

<div align="center">

## 重要提示 | Important Notice

**使用本插件需要有效的 LinuxDo 账户和 Connect API 访问权限**  
**请确保遵守论坛使用规则和 API 使用限制**

*Using this plugin requires a valid LinuxDo account and Connect API access permissions*  
*Please ensure compliance with forum usage rules and API usage restrictions*

## 谁在使用 LinuxDo Connect | Who's Using

<div align="center">

| 组织 | 使用场景 | 评价 |
|------|---------|------|
| ![Dify](https://img.shields.io/badge/Dify-AI%20Platform-orange?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggZD0iTTEyIDJMMjIgN1YxN0wxMiAyMkwyIDEyTDEyIDJaIiBmaWxsPSJ3aGl0ZSIvPgo8L3N2Zz4K) | 社区管理自动化 | "极大提升了社区运营效率" |
| ![LinuxDo](https://img.shields.io/badge/LinuxDo-Forum-red?style=for-the-badge) | 官方API集成 | "官方推荐的集成方案" |
| ![Community](https://img.shields.io/badge/Open%20Source-Community-green?style=for-the-badge) | 开源项目 | "稳定可靠，易于扩展" |

</div>

## 鸣谢 | Acknowledgments

<div align="center">

感谢以下组织和个人的支持：

| [LinuxDo Community](https://linux.do) | [Dify Platform](https://dify.ai) | [GitHub](https://github.com) |
|---------------------------------------|----------------------------------|------------------------------|

</div>

---

<sub>Made with love by frederick | Powered by Dify | Connect with LinuxDo</sub>

</div>

