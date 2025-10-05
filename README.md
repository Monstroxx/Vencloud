# Vencloud - Self-Hosted Vencord Settings Sync

[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/deploy/uEvlBC?referralCode=JaS_Iy&utm_medium=integration&utm_source=template&utm_campaign=generic)

**Vencloud** is the official cloud settings sync API for Vencord, enabling cross-device synchronization of your Vencord/euidcord settings. This repository provides everything you need to self-host your own Vencloud instance.

## ✨ Features

- **Cross-device sync** - Access your Vencord settings from any device
- **Secure authentication** - Discord OAuth2 integration
- **Easy deployment** - One-click Railway deployment
- **Privacy-focused** - Your data stays on your server
- **Fast & reliable** - Built with Go and Redis
- **Customizable** - Full control over your instance

## 🚀 Quick Start

### Deploy on Railway (Recommended)

1. **Click the Railway button above** or go to [Railway](https://railway.com)
2. **Railway will automatically**:
   - Create a new project
   - Add Redis database
   - Set up all environment variables
3. **Only customize**:
   - Discord Client ID
   - Discord Client Secret
4. **Deploy!**

### Manual Setup

<details>
<summary>Click to expand manual setup instructions</summary>

#### Prerequisites

- Go 1.23+ (for local development)
- Redis server
- Discord Application (for OAuth)

#### Installation

1. **Fork and clone the repository**:
   ```bash
   git clone https://github.com/Monstroxx/Vencloud.git
   cd Vencloud
   ```

2. **Install dependencies**:
   ```bash
   go mod download
   ```

3. **Configure environment**:
   ```bash
   cp .env.example .env
   # Edit .env with your configuration
   ```

4. **Run with Docker**:
   ```bash
   docker-compose up -d
   ```

5. **Or run natively**:
   ```bash
   go run main.go
   ```

</details>

## 🔧 Configuration

### Discord OAuth Setup

1. **Create Discord Application**:
   - Go to [Discord Developer Portal](https://discord.com/developers/applications)
   - Click "New Application"
   - Enter a name (e.g., "My Vencloud")
   - Go to "OAuth2" → "General"

2. **Get credentials**:
   - Copy **Client ID** and **Client Secret**
   - Add Redirect URI: `https://your-domain.railway.app/v1/oauth/callback`

3. **Update Railway variables**:
   ```
   DISCORD_CLIENT_ID=your_client_id
   DISCORD_CLIENT_SECRET=your_client_secret
   ```

### Environment Variables

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| `HOST` | Server host | `0.0.0.0` | No |
| `PORT` | Server port | `8080` | No |
| `REDIS_URI` | Redis connection string | `redis:6379` | Yes |
| `DISCORD_CLIENT_ID` | Discord OAuth Client ID | - | Yes |
| `DISCORD_CLIENT_SECRET` | Discord OAuth Client Secret | - | Yes |
| `DISCORD_REDIRECT_URI` | Discord OAuth Redirect URI | - | Yes |
| `PEPPER_SETTINGS` | Settings encryption pepper | - | Yes |
| `PEPPER_SECRETS` | Secrets encryption pepper | - | Yes |
| `ROOT_REDIRECT` | Root redirect URL | `https://vencord.dev` | No |
| `SIZE_LIMIT` | Max settings size (bytes) | `1048576` | No |
| `ALLOWED_USERS` | Comma-separated Discord User IDs | - | No |
| `PROXY_HEADER` | Reverse proxy header | `X-Forwarded-For` | No |
| `PROMETHEUS` | Enable Prometheus metrics | `false` | No |

### Railway Template

Use our pre-configured template for easy deployment:

```bash
# Copy railway-template.env to Railway Variables
# Only customize Discord credentials, everything else is auto-generated
```

## 🔌 Vencord/euidcord Integration

### Configure Custom Server

1. **Open Vencord** (in Goofcord or browser)
2. **Go to Settings** → **Cloud** → **Custom Server**
3. **Enter your server URL**: `https://your-domain.railway.app`
4. **Save and test**

### Supported Clients

- ✅ **Vencord** (Desktop)
- ✅ **euidcord** (Goofcord)
- ✅ **Vencord Web** (Browser)

## 🛠️ API Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| `GET` | `/v1` | Health check | No |
| `GET` | `/v1/oauth/settings` | OAuth settings page | No |
| `GET` | `/v1/oauth/callback` | OAuth callback | No |
| `GET` | `/v1/settings` | Get user settings | Yes |
| `PUT` | `/v1/settings` | Update user settings | Yes |
| `HEAD` | `/v1/settings` | Check if settings exist | Yes |
| `DELETE` | `/v1/settings` | Delete user settings | Yes |
| `DELETE` | `/v1` | Delete all user data | Yes |

## 🚀 Deployment Options

### Railway (Recommended)

- ✅ **One-click deployment**
- ✅ **Automatic HTTPS**
- ✅ **Built-in Redis**
- ✅ **Auto-scaling**
- ✅ **Free tier available**
## 🔒 Security

### Data Protection

- **Encrypted storage** - All settings are encrypted with your pepper keys
- **OAuth2 authentication** - Secure Discord integration
- **HTTPS only** - All communication encrypted
- **No data collection** - Your data stays on your server

### Best Practices

- Use strong, unique pepper keys
- Regularly update dependencies
- Monitor access logs
- Use environment variables for secrets
- Enable user whitelisting if needed

## 🐛 Troubleshooting

### Common Issues

**Redis Connection Failed**
```
panic: dial tcp: lookup redis: no such host
```
- **Solution**: Add Redis database to your Railway project

**Discord OAuth Error**
```
error: Invalid code
```
- **Solution**: Check Client ID, Secret, and Redirect URI

**Settings Not Syncing**
- **Solution**: Verify server URL in Vencord settings

### Debug Mode

Enable detailed logging by setting:
```
PROMETHEUS=true
```

### Support

- 📖 **Documentation**: [Vencord Wiki](https://vencord.dev)
- 💬 **Discord**: [Vencord Support Server](https://discord.gg/vencord)
- 🐛 **Issues**: [GitHub Issues](https://github.com/Vencord/Vencloud/issues)

## 📊 Monitoring

### Health Check

```bash
curl https://your-domain.railway.app/v1
```

### Metrics (if enabled)

```bash
curl https://your-domain.railway.app/metrics
```

## 💰 Pricing

### Railway

- **Free Tier**: $5 credits/month
- **Pro Plan**: $20/month unlimited
- **Pay-as-you-go**: $0.10/GB RAM/hour


## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📄 License

This project is licensed under the GNU General Public License v3.0 - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [Vencord](https://github.com/Vencord/Vencord) - The amazing Discord client mod
- [Railway](https://railway.app) - Excellent deployment platform
- [Go Fiber](https://gofiber.io) - Fast web framework
- [Redis](https://redis.io) - In-memory data store

---

**Made with ❤️ for the Vencord community**
