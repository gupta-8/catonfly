<!-- ========================================== -->
<!--       CATUSERBOT × FLY.IO DEPLOY           -->
<!-- ========================================== -->

<div align="center">

<!-- BADGES ROW 1 -->
<p>
  <a href="https://fly.io">
    <img src="https://img.shields.io/badge/Fly.io-Deploy%20Ready-8B5CF6?style=for-the-badge&logo=fly.io&logoColor=white" alt="Fly.io"/>
  </a>
  <a href="https://telegram.org">
    <img src="https://img.shields.io/badge/Telegram-Userbot-26A5E4?style=for-the-badge&logo=telegram&logoColor=white" alt="Telegram"/>
  </a>
  <a href="https://www.python.org/">
    <img src="https://img.shields.io/badge/Python-3.9+-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
  </a>
  <a href="https://www.postgresql.org/">
    <img src="https://img.shields.io/badge/PostgreSQL-Database-336791?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL"/>
  </a>
</p>

<!-- QUICK LINKS -->
<p>
  <a href="https://fly.io/dashboard"><kbd> Fly Dashboard </kbd></a>&nbsp;&nbsp;
  <a href="https://github.com/tgcatub/nekopack/"><kbd> Nekopack Repo </kbd></a>&nbsp;&nbsp;
  <a href="https://github.com/TgCatUB/catuserbot"><kbd> Upstream Repo </kbd></a>&nbsp;&nbsp;
  <a href="#-quick-start"><kbd> Quick Start </kbd></a>
</p>

</div>

---

## Why Fly.io?

<div align="center">

| Feature | Heroku | Fly.io |
|:-------:|:------:|:------:|
| **Free Tier** | Discontinued | Available |
| **Global Edge** | Limited | 30+ Regions |
| **PostgreSQL** | Paid Add-on | Free Dev Plan |
| **Performance** | Fast | Blazing Fast |
| **Modern Stack** | Legacy | Container-native |

</div>

<br/>

> [!TIP]
> **Fly.io** offers better performance, global deployment, and a generous free tier — making it the perfect home for your Catuserbot!
<br/>

## Prerequisites

<div align="center">

```
┌──────────────────────────────────────────────────────────────────┐
│                     BEFORE YOU START                                         │
├──────────────────────────────────────────────────────────────────┤
│  GitHub Account (for authentication)                                         │
│  Fly.io Account with billing enabled (no charge for free)                    │
│  Terminal Access (Linux / macOS / Windows / Termux)                          │
│  Your Telegram API credentials (API_ID, API_HASH, etc.)                      │
└──────────────────────────────────────────────────────────────────┘
```

</div>

> [!NOTE]
> Adding a card to Fly Billing is required but you **won't be charged** unless you exceed free tier limits or manually upgrade.

<br/>

## Installation

### Step 1: Install Fly CLI (`flyctl`)

<details>
<summary><b>Linux / macOS</b></summary>

```bash
curl -L https://fly.io/install.sh | sh
```

After installation, add to your PATH:
```bash
export FLYCTL_INSTALL="/home/$USER/.fly"
export PATH="$FLYCTL_INSTALL/bin:$PATH"
```

</details>

<details>
<summary><b>Windows (PowerShell)</b></summary>

```powershell
iwr https://fly.io/install.ps1 -useb | iex
```

</details>

<details>
<summary><b>Android (Termux)</b></summary>

```bash
pkg install root-repo
pkg install flyctl
```

</details>

<br/>

### Step 2: Authenticate with Fly.io

```bash
flyctl auth login
```

<div align="center">
  <kbd>A browser window will open — login with your GitHub account</kbd>
</div>

<br/>

## Quick Start

<div align="center">

```
     ┌─────────────────────────────────────────────────────┐
     │                         DEPLOYMENT FLOW                       │
     └─────────────────────────────────────────────────────┘
                                  │
          ┌───────────────────┼───────────────────┐
          ▼                   ▼                   ▼
     ┌─────────┐        ┌──────────┐        ┌──────────┐
     │  Clone    │        │   Launch   │        │  Deploy    │
     │  Repo     │        │   App      │        │            │
     └─────────┘        └──────────┘        └──────────┘
           │                    │                     │
           ▼                   ▼                    ▼
      git clone          flyctl launch       flyctl deploy
```

</div>

<br/>

### Clone the Repository

```bash
git clone https://github.com/tgcatub/nekopack/
cd nekopack
```

<br/>

### Create Your Fly App

```bash
flyctl launch
```

<div align="center">

| Prompt | Recommended Answer |
|:-------|:-------------------|
| Overwrite Procfile? | Type `n` (No) |
| App name | Choose any unique name |
| Region | `mia` (Miami) for best ping |
| PostgreSQL | **Yes** → Development plan |

</div>

> [!IMPORTANT]
> When prompted for **PostgreSQL**, select **Yes** and choose the **Development** plan. Catuserbot requires a database to function properly.

<br/>

### PostgreSQL Management (Optional)

<details>
<summary><b>List your Postgres clusters</b></summary>

```bash
flyctl postgres list
```

</details>

<details>
<summary><b>Attach Postgres to your app (if not done during launch)</b></summary>

```bash
flyctl postgres attach <POSTGRES_APP_NAME> -a <YOUR_APP_NAME>
```

</details>

<br/>

## Environment Variables

Configure your secrets securely with Fly. These are injected as environment variables at runtime.

### Set All Secrets at Once

```bash
flyctl secrets set \
  APP_ID='YOUR_APP_ID' \
  API_HASH='YOUR_API_HASH' \
  ALIVE_NAME='YOUR_BOT_NAME' \
  ALIVE_PIC='YOUR_ALIVE_PIC_URL' \
  STRING_SESSION='YOUR_STRING_SESSION' \
  TG_BOT_TOKEN='YOUR_BOT_TOKEN' \
  PRIVATE_GROUP_BOT_API_ID='YOUR_GROUP_ID' \
  COMMAND_HAND_LER='.' \
  ENV='ANYTHING' \
  BADCAT='True' \
  EXTERNAL_REPO='True' \
  UPSTREAM_REPO='https://github.com/TgCatUB/catuserbot' \
  TZ='Asia/Kolkata'
```

<br/>

### Secrets Reference

<div align="center">

| Variable | Description | Required |
|:---------|:------------|:--------:|
| `APP_ID` | Telegram API ID from [my.telegram.org](https://my.telegram.org) | ✅ |
| `API_HASH` | Telegram API Hash from [my.telegram.org](https://my.telegram.org) | ✅ |
| `STRING_SESSION` | Pyrogram/Telethon session string | ✅ |
| `TG_BOT_TOKEN` | Bot token from [@BotFather](https://t.me/BotFather) | ✅ |
| `ALIVE_NAME` | Display name for alive message | ❌ |
| `ALIVE_PIC` | Image URL for alive command | ❌ |
| `PRIVATE_GROUP_BOT_API_ID` | Your private log group ID | ❌ |
| `COMMAND_HAND_LER` | Command prefix (default: `.`) | ❌ |
| `TZ` | Timezone (e.g., `Asia/Kolkata`) | ❌ |

</div>

<br/>

### Verify Secrets

```bash
flyctl secrets list
```

<br/>

## Configuration

### Build Configuration

Edit `fly.toml` to customize your build:

```bash
nano fly.toml
```

If your project requires Heroku-style buildpacks:

```toml
[build]
  builder = "heroku/buildpacks"
```

> [!NOTE]
> If your repo contains a `Dockerfile`, Fly will automatically use it for building.

<br/>

## Scaling

### Scale App Memory (Highly Recommended)

```bash
flyctl scale memory 2048
```

### Scale Database Memory (Optional)

```bash
flyctl scale memory -a <YOUR_APP_NAME>-db 2048
```

<div align="center">

| Memory | Use Case |
|:------:|:---------|
| `512MB` | Minimal testing |
| `1024MB` | Light usage |
| `2048MB` | **Recommended** for stable operation |
| `4096MB` | Heavy usage / multiple plugins |

</div>

<br/>

## Deploy!

```bash
flyctl deploy
```

### Watch Logs

```bash
flyctl logs
```

<br/>

<div align="center">

```
╔══════════════════════════════════════════════════════════════╗
║                                                                         ║
║   🎉  CONGRATULATIONS!  Your Catuserbot is now LIVE!  🎉                ║
║                                                                         ║
╚══════════════════════════════════════════════════════════════╝
```

</div>

<br/>

## Troubleshooting

<details>
<summary><b>Crash / Restart Loop</b></summary>

**Cause:** Insufficient memory

**Solution:**
```bash
flyctl scale memory 2048
```

</details>

<details>
<summary><b>Secrets Not Working</b></summary>

**Cause:** Secrets not properly set or app not redeployed

**Solution:**
```bash
# Re-set secrets
flyctl secrets set KEY='value'

# Verify
flyctl secrets list

# Redeploy
flyctl deploy
```

</details>

<details>
<summary><b>Database Connection Errors</b></summary>

**Cause:** PostgreSQL not attached to your app

**Solution:**
```bash
# List available postgres clusters
flyctl postgres list

# Attach to your app
flyctl postgres attach <POSTGRES_APP_NAME> -a <YOUR_APP_NAME>
```

</details>

<details>
<summary><b>Region Latency Issues</b></summary>

**Cause:** Deployed in a far region

**Solution:**
```bash
# List available regions
flyctl platform regions

# Scale to a closer region
flyctl regions set <REGION_CODE>
```

</details>

<br/>

## Useful Commands

<div align="center">

| Command | Description |
|:--------|:------------|
| `flyctl status` | Check app status |
| `flyctl logs` | View live logs |
| `flyctl ssh console` | SSH into your app |
| `flyctl scale show` | View current scaling |
| `flyctl releases` | List deployment history |
| `flyctl restart` | Restart your app |
| `flyctl destroy` | Delete your app |

</div>
