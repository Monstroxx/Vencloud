# Vencloud Railway Deployment Guide

## Prerequisites

1. **Railway Account**: Create an account at [railway.app](https://railway.app)
2. **Discord Application**: Create a Discord Application for OAuth

## Discord Application Setup

1. Go to [Discord Developer Portal](https://discord.com/developers/applications)
2. Click "New Application"
3. Enter a name (e.g. "My Vencloud")
4. Go to "OAuth2" → "General"
5. Copy the **Client ID** and **Client Secret**
6. Add a Redirect URI: `https://your-domain.railway.app/auth/callback`

## Railway Deployment

### Option 1: GitHub Integration (Recommended)

1. **Push repository to GitHub**:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin https://github.com/your-username/vencloud-railway.git
   git push -u origin main
   ```

2. **Create Railway project**:
   - Go to [railway.app](https://railway.app)
   - Click "New Project"
   - Select "Deploy from GitHub repo"
   - Connect your GitHub repository

3. **Set environment variables**:
   - Go to your Railway project
   - Click "Variables"
   - Add the following variables:

   ```
   DISCORD_CLIENT_ID=your_discord_client_id
   DISCORD_CLIENT_SECRET=your_discord_client_secret
   DISCORD_REDIRECT_URI=https://your-domain.railway.app/auth/callback
   ROOT_REDIRECT=https://vencord.dev
   PEPPER_SETTINGS=generate_a_random_string
   PEPPER_SECRETS=generate_a_random_string
   SIZE_LIMIT=1048576
   ALLOWED_USERS=
   PROXY_HEADER=X-Forwarded-For
   PROMETHEUS=false
   ```

### Option 2: Railway CLI

1. **Install Railway CLI**:
   ```bash
   npm install -g @railway/cli
   railway login
   ```

2. **Deploy project**:
   ```bash
   cd /path/to/vencloud
   railway init
   railway up
   ```

3. **Set environment variables**:
   ```bash
   railway variables set DISCORD_CLIENT_ID=your_client_id
   railway variables set DISCORD_CLIENT_SECRET=your_client_secret
   # ... additional variables
   ```

## After Deployment

1. **Note the domain**: Railway gives you a domain like `https://your-project.railway.app`
2. **Update Discord Redirect URI**: 
   - Go back to your Discord Application
   - Change the Redirect URI to: `https://your-project.railway.app/auth/callback`

## Vencord/euidcord Configuration

1. **Open Vencord** (in Goofcord)
2. **Settings** → **Cloud** → **Custom Server**
3. **Enter Server URL**: `https://your-project.railway.app`
4. **Save and test**

## Security Notes

- **PEPPER_SETTINGS** and **PEPPER_SECRETS** should be random, long strings
- **ALLOWED_USERS** can be left empty for public access or add Discord User IDs
- Make sure your Railway domain supports HTTPS

## Troubleshooting

- **Check logs**: Railway Dashboard → Your Service → Logs
- **Redis Connection**: Make sure Redis is running
- **Discord OAuth**: Check Client ID, Secret and Redirect URI
- **HTTPS**: Railway should automatically provide HTTPS

## Pricing

Railway offers:
- **Free Tier**: $5 Credits per month
- **Pro Plan**: $20/month for unlimited usage
- **Pay-as-you-go**: $0.10 per GB RAM/hour

The Free Tier should be sufficient for Vencloud as it's a relatively lightweight service.
