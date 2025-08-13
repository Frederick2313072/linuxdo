# LinuxDo Connect Plugin for Dify

**Author:** frederick  
**Version:** 0.0.1  
**Type:** tool  

## 项目概述

LinuxDo Connect Plugin 是一个专为 Dify 平台设计的插件，通过 LinuxDo Connect API 连接 LinuxDo 论坛。该插件提供全面的论坛集成功能，包括身份验证、用户信息获取、内容搜索、个性化推荐和自动签到等功能。

### 主要功能

- **身份验证**: 支持 OAuth2 和 API Key 认证方式
- **用户信息管理**: 获取和验证用户信息，包括信任等级、活跃状态等
- **内容搜索**: 在论坛中搜索主题、帖子和讨论，支持高级过滤选项
- **个性化推荐**: 基于用户兴趣和活动历史提供内容推荐
- **自动签到**: 自动执行每日签到，维持账户活跃状态
- **活动跟踪**: 监控用户活动，提供详细的统计信息

## 分步设置说明

### 第1步：前期准备

1. **Python 环境要求**
   - Python 3.11 或更高版本
   - 确保已安装 pip 包管理器

2. **获取 LinuxDo Connect 认证信息**
   - 访问 [LinuxDo Connect](https://connect.linux.do)
   - 注册或登录您的 LinuxDo 账户
   - 申请应用接入：点击"我的应用接入" -> "申请新接入"
   - 填写应用信息，包括应用名称、描述和回调地址
   - 获取以下认证信息：
     - **Client ID**: 应用客户端ID
     - **Client Secret**: 应用客户端密钥
     - **API Key**: 用户API访问密钥

### 第2步：安装依赖

1. **克隆或下载项目**
   ```bash
   git clone <repository_url>
   cd linuxdo
   ```

2. **安装Python依赖包**
   ```bash
   pip install -r requirements.txt
   ```

3. **依赖包说明**
   - `dify_plugin>=0.2.0,<0.3.0`: Dify插件SDK
   - `requests>=2.31.0`: HTTP请求库

### 第3步：配置环境变量

1. **创建环境配置文件**
   ```bash
   cp .env.example .env
   ```

2. **编辑.env文件，添加以下配置**
   ```env
   # Dify插件调试配置
   INSTALL_METHOD=remote
   REMOTE_INSTALL_URL=debug.dify.ai:5003
   REMOTE_INSTALL_KEY=<your_debugging_key>

   # LinuxDo Connect API配置（可选，用于测试）
   LINUXDO_CLIENT_ID=<your_client_id>
   LINUXDO_CLIENT_SECRET=<your_client_secret>
   LINUXDO_API_KEY=<your_api_key>
   ```

### 第4步：配置插件认证

在 Dify 平台中安装插件后，需要配置以下认证信息：

1. **Client ID**
   - 在插件设置中输入从 LinuxDo Connect 获取的 Client ID
   - 用于基础认证和API访问

2. **Client Secret**
   - 输入对应的 Client Secret
   - 与 Client ID 配合使用进行身份验证

3. **API Key**
   - 输入您的个人 API Key
   - 用于识别和验证用户身份

### 第5步：测试连接

1. **本地调试测试**
   ```bash
   python -m main
   ```

2. **验证连接状态**
   - 检查 Dify 插件列表中是否显示 "LinuxDo Connect"
   - 插件状态应显示为 "debugging" 或 "active"
   - 尝试使用任一工具功能验证API连接

## 详细使用说明

### 工具功能详解

#### 1. 用户信息工具 (LinuxDo User Info)

**功能**: 获取和验证用户信息

**参数**:
- `action_type`: 操作类型
  - `info`: 获取用户基本信息
  - `verify`: 验证用户身份
  - `profile`: 获取详细档案
  - `activity`: 查看活动状态

**使用示例**:
```
获取我的LinuxDo用户信息
验证当前用户的信任等级
查看我的论坛活动状态
```

#### 2. 内容搜索工具 (LinuxDo Content Search)

**功能**: 在论坛中搜索内容

**参数**:
- `search_query` (必需): 搜索关键词
- `search_type`: 搜索类型 (all/topics/posts/categories)
- `category_filter`: 分类筛选
- `limit`: 结果数量限制 (1-100)
- `sort_by`: 排序方式 (relevance/date/views/replies)

**使用示例**:
```
搜索关于"Linux内核"的主题
在技术分享分类中搜索"Docker"相关内容
查找最近热门的讨论话题
```

#### 3. 个性化推荐工具 (LinuxDo Recommendations)

**功能**: 基于用户兴趣提供内容推荐

**参数**:
- `recommendation_type`: 推荐类型
- `category_preference`: 偏好分类
- `limit`: 推荐数量
- `time_range`: 时间范围

**使用示例**:
```
为我推荐感兴趣的技术话题
推荐本周热门讨论
基于我的浏览历史推荐相关内容
```

#### 4. 自动签到工具 (LinuxDo Check-in)

**功能**: 自动签到和活动跟踪

**参数**:
- `action_type`: 操作类型 (checkin/status/history/streak)
- `auto_activity`: 是否执行额外活动
- `notification_enabled`: 是否启用通知
- `days_to_check`: 历史查询天数

**使用示例**:
```
执行今日签到
查看我的签到状态
检查连续签到记录
查看最近7天的签到历史
```

### 高级功能

#### OAuth2 集成

插件支持标准的 OAuth2 授权流程：

1. **授权端点**: `https://connect.linux.do/oauth2/authorize`
2. **令牌端点**: `https://connect.linux.do/oauth2/token`
3. **用户信息端点**: `https://connect.linux.do/api/user`

#### API 限制和配额

- **请求频率**: 建议每分钟不超过60个请求
- **数据量限制**: 单次搜索最多返回100条结果
- **缓存策略**: 用户信息缓存5分钟，内容搜索缓存1分钟

## 必需的 APIs 和认证信息

### LinuxDo Connect API

#### 认证方式
1. **Basic Authorization**
   - 使用 Client ID 和 Client Secret
   - 格式: `Authorization: Basic base64(client_id:client_secret)`

2. **API Key Authentication**
   - 用于用户身份识别
   - 格式: `?api_key={your_api_key}`

#### 必需的认证信息

| 参数 | 类型 | 必需 | 描述 | 获取方式 |
|------|------|------|------|----------|
| Client ID | string | 是 | 应用客户端标识符 | 从 LinuxDo Connect 应用管理页面获取 |
| Client Secret | string | 是 | 应用客户端密钥 | 从 LinuxDo Connect 应用管理页面获取 |
| API Key | string | 是 | 用户个人访问密钥 | 从 LinuxDo Connect 用户设置页面获取 |

#### API 端点列表

| 端点 | 方法 | 功能 | 认证要求 |
|------|------|------|----------|
| `/api/key` | GET | 验证API Key | Basic Auth + API Key |
| `/api/user` | GET | 获取用户信息 | Basic Auth + API Key |
| `/api/search` | GET | 搜索论坛内容 | Basic Auth + API Key |
| `/api/recommendations` | GET | 获取个性化推荐 | Basic Auth + API Key |
| `/api/checkin` | POST | 执行签到操作 | Basic Auth + API Key |
| `/oauth2/authorize` | GET | OAuth2 授权 | Client ID |
| `/oauth2/token` | POST | 获取访问令牌 | Client ID + Secret |

### 可获取的用户数据字段

| 字段 | 类型 | 描述 |
|------|------|------|
| id | integer | 用户唯一标识符（不可变） |
| username | string | 论坛用户名 |
| name | string | 用户昵称（可变） |
| avatar_template | string | 头像模板URL |
| active | boolean | 账号活跃状态 |
| trust_level | integer | 信任等级（0-4） |
| silenced | boolean | 禁言状态 |
| external_ids | object | 外部ID关联信息 |
| api_key | string | API访问密钥 |

## 连接要求和配置详情

### 网络要求

1. **域名访问**
   - 确保可以访问 `connect.linux.do`
   - 确保可以访问 `linux.do` (用于内容链接)

2. **端口要求**
   - HTTPS (443): 用于API通信
   - HTTP (80): 用于重定向处理

3. **代理配置**
   - 如果使用代理，请确保支持HTTPS
   - 配置代理白名单包含 LinuxDo 相关域名

### 安全配置

1. **HTTPS 要求**
   - 所有API通信必须使用HTTPS
   - 确保SSL证书验证开启

2. **认证信息保护**
   - Client Secret 必须保密，不可在客户端暴露
   - API Key 应定期轮换
   - 使用环境变量存储敏感信息

3. **请求头配置**
   ```
   User-Agent: Dify LinuxDo Plugin/1.0
   Content-Type: application/json
   Authorization: Basic {base64_credentials}
   ```

### 错误处理

常见错误码和处理方式：

| 状态码 | 错误类型 | 处理方式 |
|--------|----------|----------|
| 401 | 认证失败 | 检查 Client ID/Secret |
| 403 | API Key 无效 | 重新获取 API Key |
| 429 | 请求过频 | 实施请求限制 |
| 500 | 服务器错误 | 重试或联系支持 |

## 项目源代码

### 仓库信息

- **源代码仓库**: [GitHub Repository](https://github.com/frederick/linuxdo-dify-plugin)
- **主分支**: main
- **许可证**: MIT License

### 项目结构

```
linuxdo/
├── _assets/                 # 资源文件
│   ├── icon-dark.svg       # 深色图标
│   └── icon.svg            # 浅色图标
├── provider/               # 插件提供者
│   ├── linuxdo.py          # 主要提供者类
│   └── linuxdo.yaml        # 提供者配置
├── tools/                  # 工具实现
│   ├── checkin.py          # 签到工具
│   ├── checkin.yaml        # 签到工具配置
│   ├── content_search.py   # 内容搜索工具
│   ├── content_search.yaml # 搜索工具配置
│   ├── linuxdo.py          # 用户信息工具
│   ├── linuxdo.yaml        # 用户工具配置
│   ├── recommendations.py  # 推荐工具
│   └── recommendations.yaml# 推荐工具配置
├── main.py                 # 插件入口
├── manifest.yaml           # 插件清单
├── requirements.txt        # Python依赖
├── api.md                  # API文档
├── GUIDE.md               # 开发指南
├── PRIVACY.md             # 隐私政策
└── README.md              # 项目说明
```

### 贡献指南

1. Fork 项目仓库
2. 创建功能分支: `git checkout -b feature/new-feature`
3. 提交更改: `git commit -am 'Add new feature'`
4. 推送分支: `git push origin feature/new-feature`
5. 创建 Pull Request

### 问题反馈

如果您遇到任何问题或有改进建议，请通过以下方式联系：

- **GitHub Issues**: [Report Issues](https://github.com/frederick/linuxdo-dify-plugin/issues)
- **邮箱**: frederick@example.com
- **LinuxDo 论坛**: @frederick

---

**注意**: 请确保遵守 LinuxDo 论坛的使用条款和 API 使用政策。本插件仅供学习和个人使用，请勿用于商业用途或恶意行为。
