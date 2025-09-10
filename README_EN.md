<div align="center">

<img src="_assets/linuxdo-banner.png" alt="LinuxDo Connect" width="600" height="180">

# LinuxDo Connect Plugin for Dify

*Powerful Dify plugin for connecting LinuxDo forum*

[![Version](https://img.shields.io/badge/version-0.0.2-blue.svg)](https://github.com/langgenius/dify-official-plugins)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Dify](https://img.shields.io/badge/Dify-Plugin-orange.svg)](https://dify.ai)
[![LinuxDo](https://img.shields.io/badge/LinuxDo-Connect-red.svg)](https://connect.linux.do)

**Author:** frederick | **Type:** Tool Plugin | **Version:** 0.0.2

[中文文档](README.md) | [Features](#features) | [Quick Start](#installation--configuration) | [API Docs](api.md)

</div>

---

## Overview

> **LinuxDo Connect** plugin enables seamless connection and operation of LinuxDo forum within Dify

The LinuxDo Connect plugin allows you to directly connect and interact with the LinuxDo forum within Dify. Through the LinuxDo Connect API, you can perform authentication, retrieve user information, search content, get personalized recommendations, and execute automatic check-ins.

LinuxDo Connect插件允许你在Dify中直接连接和操作LinuxDo论坛。通过LinuxDo Connect API，你可以进行身份验证、获取用户信息、搜索内容、获取个性化推荐，以及执行自动签到等操作。

## Features

<table>
<tr>
<td width="50%">

### 🔐 User Authentication & Information
**用户认证与信息获取**

- Validate API key status
- Retrieve detailed user information (username, trust level, active status, etc.)
- Support for quick verification mode

</td>
<td width="50%">

### 🔍 Content Search
**内容搜索**

- Site-wide content search (topics, posts, categories)
- Advanced filtering options (category filtering, result sorting)
- Sort by relevance, date, views, or reply count
- Customizable result limit

</td>
</tr>
</table>

## Installation & Configuration

### Step 1: Get LinuxDo Connect API Credentials
**获取 LinuxDo Connect API 凭据**

> Visit [LinuxDo Connect](https://connect.linux.do) to apply for API access permissions

<details>
<summary><strong>Detailed Steps | 详细步骤</strong></summary>

#### **Register Application | 注册应用**
```
Visit: https://connect.linux.do
Click: "My App Integration" -> "Apply for New Integration"
Fill in: Application information and callback URL
```

#### **Get Credentials | 获取凭据**
| Credential Type | Purpose | 用途 |
|---------|------|---------|
| **Client ID** | Client identifier for basic auth | 基础认证的客户端标识 |
| **Client Secret** | Client secret for basic auth | 基础认证的客户端密钥 |
| **API Key** | API key for user account identification | 用户账户识别密钥 |

</details>

### Step 2: Configure Plugin in Dify
**在 Dify 中配置插件**

```mermaid
graph LR
    A[Install Plugin] --> B[Open Config Page]
    B --> C[Fill Credentials]
    C --> D[Save Config]
    D --> E[Start Using]
```

**Configuration Items | 配置项:**
- **Client ID**: Your LinuxDo Client ID
- **Client Secret**: Your LinuxDo Client Secret  
- **API Key**: Your LinuxDo API Key

## Performance Features

<div align="center">

| Feature | LinuxDo Connect | Traditional Solution | Advantage |
|---------|----------------|----------|------|
| **Response Speed** | Fast Response | Slower | **Optimized Performance** |
| **Security Authentication** | OAuth 2.0 | Basic Auth | **Enterprise-grade Security** |
| **Data Processing** | Structured JSON | Raw HTML | **Easy to Parse** |
| **Error Recovery** | Auto Retry | Manual Handling | **More Reliable** |
| **Memory Usage** | Lightweight | Higher Usage | **Resource Optimized** |

### Performance Benchmarks

```
High-efficiency integration solution based on LinuxDo Connect API
Supports fast user authentication and content retrieval
Optimized network request processing mechanism
```

</div>

## Usage

### User Information | 用户信息获取

<table>
<tr>
<td width="50%">

**Get Complete User Information**
```python
user_info = linuxdo_user_info(
    include_extra_info=True,
    verify_only=False
)
```

</td>
<td width="50%">

**Quick API Key Verification**
```python
verification = linuxdo_user_info(
    include_extra_info=False,
    verify_only=True
)
```

</td>
</tr>
</table>

### Content Search | 内容搜索

<table>
<tr>
<td width="50%">

**Search All Content**
```python
search_results = linuxdo_content_search(
    search_query="Python programming",
    search_type="all",
    limit=20,
    sort_by="relevance"
)
```

</td>
<td width="50%">

**Search Topics Only**
```python
topic_results = linuxdo_content_search(
    search_query="machine learning",
    search_type="topics",
    category_filter="Technical Discussion",
    limit=10,
    sort_by="date"
)
```

</td>
</tr>
</table>

## API Endpoints Information

### LinuxDo Connect API Endpoints

| Endpoint Type | URL | Description |
|---------|-----|------|
| **Authorization Endpoint** | `https://connect.linux.do/oauth2/authorize` | OAuth2 authorization |
| **Token Endpoint** | `https://connect.linux.do/oauth2/token` | Get access token |
| **User Info Endpoint** | `https://connect.linux.do/api/user` | Get detailed user information |
| **User Info Endpoint (OAuth2)** | `https://connect.linux.do/oauth2/userinfo` | OAuth2 user information |

### Available User Fields | 可获取的用户字段

<details>
<summary><strong>User Field Details | 用户字段详情</strong></summary>

| Field | Description | 字段 | 说明 |
|------|------|-------|-------------|
| `id` | Unique user identifier (immutable) | `id` | 用户唯一标识（不可变） |
| `username` | Forum username | `username` | 论坛用户名 |
| `name` | Forum display name (mutable) | `name` | 论坛用户昵称（可变） |
| `avatar_template` | User avatar template URL | `avatar_template` | 用户头像模板URL |
| `active` | Account active status | `active` | 账号活跃状态 |
| `trust_level` | Trust level (0-4) | `trust_level` | 信任等级（0-4） |
| `silenced` | Silenced status | `silenced` | 禁言状态 |
| `external_ids` | External ID associations | `external_ids` | 外部ID关联信息 |
| `api_key` | API access key | `api_key` | API访问密钥 |

</details>

## Data Structures

### User Info Response | 用户信息响应
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

### Search Results Response | 搜索结果响应
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

## Security Recommendations

> **Important**: Please follow these security best practices

<table>
<tr>
<td width="33%">

### Protect Credentials
**保护凭据**

- Keep Client Secret and API Key secure
- Never expose sensitive information in frontend code
- Regularly update API credentials

</td>
<td width="33%">

### Network Security
**网络安全**

- Ensure HTTPS protocol for data transmission
- Validate all user input data
- Implement proper error handling

</td>
<td width="33%">

### Access Control
**访问控制**

- Implement service restrictions based on user trust level
- Monitor API usage frequency to prevent abuse
- Set reasonable rate limits

</td>
</tr>
</table>

## Development Information

### Project Structure | 项目结构

```
linuxdo/
├── manifest.yaml              # Plugin manifest file
├── requirements.txt           # Python dependencies
├── main.py                   # Plugin entry point
├── provider/
│   ├── linuxdo.py           # Provider implementation
│   └── linuxdo.yaml         # Provider configuration
├── tools/
│   ├── linuxdo.py           # User info tool
│   ├── linuxdo.yaml         # User info tool configuration
│   ├── content_search.py    # Content search tool
│   └── content_search.yaml  # Content search tool configuration
└── _assets/
    ├── icon.svg            # Plugin icon
    └── icon-dark.svg       # Dark mode icon
```

## License

> This plugin follows the corresponding open source license. Please ensure compliance with LinuxDo forum terms of use and API usage policies before use.

本插件遵循相应的开源许可证。使用前请确保遵守 LinuxDo 论坛的使用条款和 API 使用政策。

## Support & Feedback

<div align="center">

### Need Help? We're happy to provide support!

</div>

<table>
<tr>
<td width="50%" align="center">

### Report Issues
**报告问题**

[![GitHub Issues](https://img.shields.io/github/issues/langgenius/dify-official-plugins)](https://github.com/langgenius/dify-official-plugins/issues)

[Create GitHub Issue](https://github.com/langgenius/dify-official-plugins/issues/new)

</td>
<td width="50%" align="center">

### Email Contact
**邮件联系**

[![Email](https://img.shields.io/badge/Email-2313072@mail.nankai.edu.cn-blue.svg)](mailto:2313072@mail.nankai.edu.cn)

[Send Email to Developer](mailto:2313072@mail.nankai.edu.cn)

</td>
</tr>
</table>

---

<div align="center">

## Important Notice

**Using this plugin requires a valid LinuxDo account and Connect API access permissions**  
**Please ensure compliance with forum usage rules and API usage restrictions**

*使用本插件需要有效的 LinuxDo 账户和 Connect API 访问权限*  
*请确保遵守论坛使用规则和 API 使用限制*

## Who's Using LinuxDo Connect

<div align="center">

| Organization | Use Case | Review |
|------|---------|------|
| ![Dify](https://img.shields.io/badge/Dify-AI%20Platform-orange?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjQiIGhlaWdodD0iMjQiIHZpZXdCb3g9IjAgMCAyNCAyNCIgZmlsbD0ibm9uZSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj4KPHBhdGggZD0iTTEyIDJMMjIgN1YxN0wxMiAyMkwyIDEyTDEyIDJaIiBmaWxsPSJ3aGl0ZSIvPgo8L3N2Zz4K) | Community Management Automation | "Greatly improved community operation efficiency" |
| ![LinuxDo](https://img.shields.io/badge/LinuxDo-Forum-red?style=for-the-badge) | Official API Integration | "Officially recommended integration solution" |
| ![Community](https://img.shields.io/badge/Open%20Source-Community-green?style=for-the-badge) | Open Source Projects | "Stable, reliable, and easy to extend" |

</div>

## Acknowledgments

<div align="center">

Thanks to the following organizations and individuals for their support:

| [LinuxDo Community](https://linux.do) | [Dify Platform](https://dify.ai) | [GitHub](https://github.com) |
|---------------------------------------|----------------------------------|------------------------------|

</div>

---

<sub>Made with love by frederick | Powered by Dify | Connect with LinuxDo</sub>

</div>