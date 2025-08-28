# LinuxDo Connect Plugin for Dify

English | [中文](README.md)

**Author:** frederick  
**Version:** 0.0.1  
**Type:** tool  

## Project Overview

LinuxDo Connect Plugin is a plugin designed specifically for the Dify platform, connecting to the LinuxDo forum through the LinuxDo Connect API. This plugin provides comprehensive forum integration features, including authentication, user information retrieval, content search, personalized recommendations, and automatic check-in.

### Key Features

- **Authentication**: Supports OAuth2 and API Key authentication methods
- **User Information Management**: Retrieve and verify user information, including trust level, activity status, etc.
- **Content Search**: Search for topics, posts, and discussions in the forum with advanced filtering options
- **Personalized Recommendations**: Provide customized recommendations based on user interests and activity history
- **Auto Check-in**: Automatically perform daily check-ins to maintain account activity
- **Activity Tracking**: Monitor user activities and provide detailed statistics

## Step-by-Step Setup Instructions

### Step 1: Prerequisites

1. **Python Environment Requirements**
   - Python 3.11 or higher
   - Ensure pip package manager is installed

2. **Obtain LinuxDo Connect Authentication Information**
   - Visit [LinuxDo Connect](https://connect.linux.do)
   - Register or log in to your LinuxDo account
   - Apply for application access: Click "My Application Access" -> "Apply for New Access"
   - Fill in application information, including application name, description, and callback URL
   - Obtain the following authentication information:
     - **Client ID**: Application client identifier
     - **Client Secret**: Application client secret
     - **API Key**: User API access key

### Step 2: Install Dependencies

1. **Clone or Download the Project**
   ```bash
   git clone https://github.com/Frederick2313072/linuxdo
   cd linuxdo
   ```

2. **Install Python Dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Dependency Description**
   - `dify_plugin>=0.3.0,<0.5.0`: Dify Plugin SDK
   - `requests>=2.31.0,<3.0.0`: HTTP request library

### Step 3: Configure Environment Variables

1. **Create Environment Configuration File**
   ```bash
   cp .env.example .env
   ```

2. **Edit .env File and Add the Following Configuration**
   ```env
   # Dify plugin debugging configuration
   INSTALL_METHOD=remote
   REMOTE_INSTALL_URL=debug.dify.ai:5003
   REMOTE_INSTALL_KEY=<your_debugging_key>

   # LinuxDo Connect API configuration (optional, for testing)
   LINUXDO_CLIENT_ID=<your_client_id>
   LINUXDO_CLIENT_SECRET=<your_client_secret>
   LINUXDO_API_KEY=<your_api_key>
   ```

### Step 4: Configure Plugin Authentication

After installing the plugin in the Dify platform, you need to configure the following authentication information:

1. **Client ID**
   - Enter the Client ID obtained from LinuxDo Connect in the plugin settings
   - Used for basic authentication and API access

2. **Client Secret**
   - Enter the corresponding Client Secret
   - Used together with Client ID for identity verification

3. **API Key**
   - Enter your personal API Key
   - Used to identify and verify user identity

### Step 5: Test Connection

1. **Local Debug Testing**
   ```bash
   python -m main
   ```

2. **Verify Connection Status**
   - Check if "LinuxDo Connect" appears in the Dify plugin list
   - Plugin status should show as "debugging" or "active"
   - Try using any tool function to verify API connection

## Detailed Usage Instructions

### Tool Features Overview

#### 1. User Information Tool (LinuxDo User Info)

**Function**: Retrieve and verify user information

**Parameters**:
- `action_type`: Action type
  - `info`: Get basic user information
  - `verify`: Verify user identity
  - `profile`: Get detailed profile
  - `activity`: View activity status

**Usage Examples**:
```
Get my LinuxDo user information
Verify current user's trust level
View my forum activity status
```

#### 2. Content Search Tool (LinuxDo Content Search)

**Function**: Search content in the forum

**Parameters**:
- `search_query` (required): Search keywords
- `search_type`: Search type (all/topics/posts/categories)
- `category_filter`: Category filter
- `limit`: Result limit (1-100)
- `sort_by`: Sort method (relevance/date/views/replies)

**Usage Examples**:
```
Search for topics about "Linux kernel"
Search for "Docker" related content in the technical sharing category
Find recent popular discussion topics
```

#### 3. Personalized Recommendations Tool (LinuxDo Recommendations)

**Function**: Provide content recommendations based on user interests

**Parameters**:
- `recommendation_type`: Recommendation type
- `category_preference`: Preferred category
- `limit`: Number of recommendations
- `time_range`: Time range

**Usage Examples**:
```
Recommend technical topics I might be interested in
Recommend this week's popular discussions
Recommend related content based on my browsing history
```

#### 4. Auto Check-in Tool (LinuxDo Check-in)

**Function**: Auto check-in and activity tracking

**Parameters**:
- `action_type`: Action type (checkin/status/history/streak)
- `auto_activity`: Whether to perform additional activities
- `notification_enabled`: Whether to enable notifications
- `days_to_check`: Number of days for history query

**Usage Examples**:
```
Perform today's check-in
View my check-in status
Check consecutive check-in records
View check-in history for the last 7 days
```

### Advanced Features

#### OAuth2 Integration

The plugin supports standard OAuth2 authorization flow:

1. **Authorization Endpoint**: `https://connect.linux.do/oauth2/authorize`
2. **Token Endpoint**: `https://connect.linux.do/oauth2/token`
3. **User Info Endpoint**: `https://connect.linux.do/api/user`

#### API Limits and Quotas

- **Request Frequency**: Recommended not to exceed 60 requests per minute
- **Data Volume Limit**: Maximum 100 results per search
- **Cache Strategy**: User information cached for 5 minutes, search results cached for 1 minute

## Required APIs and Credentials

### LinuxDo Connect API

#### Authentication Methods
1. **Basic Authorization**
   - Uses Client ID and Client Secret
   - Format: `Authorization: Basic base64(client_id:client_secret)`

2. **API Key Authentication**
   - Used for user identity identification
   - Format: `?api_key={your_api_key}`

#### Required Authentication Information

| Parameter | Type | Required | Description | How to Obtain |
|-----------|------|----------|-------------|---------------|
| Client ID | string | Yes | Application client identifier | Obtain from LinuxDo Connect application management page |
| Client Secret | string | Yes | Application client secret | Obtain from LinuxDo Connect application management page |
| API Key | string | Yes | User personal access key | Obtain from LinuxDo Connect user settings page |

#### API Endpoint List

| Endpoint | Method | Function | Authentication Requirements |
|----------|--------|----------|----------------------------|
| `/api/key` | GET | Verify API Key | Basic Auth + API Key |
| `/api/user` | GET | Get user information | Basic Auth + API Key |
| `/api/search` | GET | Search forum content | Basic Auth + API Key |
| `/api/recommendations` | GET | Get personalized recommendations | Basic Auth + API Key |
| `/api/checkin` | POST | Perform check-in operation | Basic Auth + API Key |
| `/oauth2/authorize` | GET | OAuth2 authorization | Client ID |
| `/oauth2/token` | POST | Get access token | Client ID + Secret |

### Available User Data Fields

| Field | Type | Description |
|-------|------|-------------|
| id | integer | User unique identifier (immutable) |
| username | string | Forum username |
| name | string | User display name (changeable) |
| avatar_template | string | Avatar template URL |
| active | boolean | Account active status |
| trust_level | integer | Trust level (0-4) |
| silenced | boolean | Silenced status |
| external_ids | object | External ID association information |
| api_key | string | API access key |

## Connection Requirements and Configuration Details

### Network Requirements

1. **Domain Access**
   - Ensure access to `connect.linux.do`
   - Ensure access to `linux.do` (for content links)

2. **Port Requirements**
   - HTTPS (443): For API communication
   - HTTP (80): For redirect handling

3. **Proxy Configuration**
   - If using a proxy, ensure HTTPS support
   - Configure proxy whitelist to include LinuxDo related domains

### Security Configuration

1. **HTTPS Requirements**
   - All API communications must use HTTPS
   - Ensure SSL certificate verification is enabled

2. **Authentication Information Protection**
   - Client Secret must be kept confidential and not exposed on the client side
   - API Key should be rotated regularly
   - Use environment variables to store sensitive information

3. **Request Header Configuration**
   ```
   User-Agent: Dify LinuxDo Plugin/1.0
   Content-Type: application/json
   Authorization: Basic {base64_credentials}
   ```

### Error Handling

Common error codes and handling methods:

| Status Code | Error Type | Handling Method |
|-------------|------------|-----------------|
| 401 | Authentication failed | Check Client ID/Secret |
| 403 | Invalid API Key | Re-obtain API Key |
| 429 | Too many requests | Implement request limiting |
| 500 | Server error | Retry or contact support |

## Project Source Code

### Repository Information

- **Source Code Repository**: [GitHub Repository](https://github.com/Frederick2313072/linuxdo)
- **Main Branch**: main
- **License**: MIT License

### Project Structure

```
linuxdo/
├── _assets/                 # Asset files
│   └── icon.svg            # Plugin icon
├── provider/               # Plugin provider
│   ├── linuxdo.py          # Main provider class
│   └── linuxdo.yaml        # Provider configuration
├── tools/                  # Tool implementations
│   ├── checkin.py          # Check-in tool
│   ├── checkin.yaml        # Check-in tool configuration
│   ├── content_search.py   # Content search tool
│   ├── content_search.yaml # Search tool configuration
│   ├── linuxdo.py          # User info tool
│   ├── linuxdo.yaml        # User tool configuration
│   ├── recommendations.py  # Recommendation tool
│   └── recommendations.yaml# Recommendation tool configuration
├── main.py                 # Plugin entry point
├── manifest.yaml           # Plugin manifest
├── requirements.txt        # Python dependencies
├── api.md                  # API documentation
├── GUIDE.md               # Development guide
├── PRIVACY.md             # Privacy policy
├── README.md              # Project documentation (Chinese)
└── README_EN.md           # Project documentation (English)
```

### Contribution Guidelines

1. Fork the project repository
2. Create a feature branch: `git checkout -b feature/new-feature`
3. Commit changes: `git commit -am 'Add new feature'`
4. Push to branch: `git push origin feature/new-feature`
5. Create a Pull Request

### Issue Reporting

If you encounter any issues or have suggestions for improvement, please contact us through:

- **GitHub Issues**: [Report Issues](https://github.com/Frederick2313072/linuxdo/issues)
- **Email**: frederick@example.com
- **LinuxDo Forum**: @frederick

## Development and Testing

### Local Development

1. **Set up development environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   ```

2. **Configure debugging**
   - Create `.env` file with your debugging credentials
   - Set `INSTALL_METHOD=remote` for remote debugging
   - Set `REMOTE_INSTALL_URL` and `REMOTE_INSTALL_KEY`

3. **Run the plugin**
   ```bash
   python -m main
   ```

### Plugin Packaging

To package the plugin for distribution:

```bash
dify-plugin plugin package ./
```

This will create a `plugin.difypkg` file ready for submission to the Dify Marketplace.

## Support and Community

### Getting Help

- **Documentation**: Check this README and the GUIDE.md file
- **Issues**: Report bugs or request features on GitHub Issues
- **Community**: Join discussions on the LinuxDo forum

### Contributing

We welcome contributions! Please read our contribution guidelines and submit pull requests for any improvements.

---

**Note**: Please ensure compliance with LinuxDo forum terms of service and API usage policies. This plugin is for educational and personal use only. Please do not use it for commercial purposes or malicious activities.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Changelog

### Version 0.0.1 (Initial Release)
- Basic authentication with LinuxDo Connect API
- User information retrieval and verification
- Content search functionality
- Personalized recommendations
- Auto check-in feature
- Comprehensive documentation and privacy policy
