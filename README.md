<!-- ================= BADGES ================= -->
<p align="center">
  <img src="https://img.shields.io/badge/Fly.io-Deploy-blueviolet?style=for-the-badge&logo=fly.io" />
  <img src="https://img.shields.io/badge/Telegram-Userbot-2CA5E0?style=for-the-badge&logo=telegram" />
  <img src="https://img.shields.io/badge/Status-Ready-success?style=for-the-badge" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-3776AB?style=flat-square&logo=python&logoColor=white" />
  <img src="https://img.shields.io/github/license/TgCatUB/catuserbot?style=flat-square" />
  <img src="https://img.shields.io/github/stars/TgCatUB/catuserbot?style=flat-square" />
  <img src="https://img.shields.io/github/forks/TgCatUB/catuserbot?style=flat-square" />
</p>

<h1 align="center">🚀 Deploy Catuserbot on Fly.io (Step-by-Step)</h1>

<p align="center">
  Fly.io is a strong alternative to Heroku, but deployment is terminal-first.<br/>
  This guide deploys <b>Catuserbot / Nekopack</b> on Fly with Postgres + secrets + recommended memory settings.
</p>

<p align="center">
  <a href="https://fly.io/dashboard"><b>Fly Dashboard</b></a> •
  <a href="https://github.com/tgcatub/nekopack/"><b>Nekopack Repo</b></a> •
  <a href="https://github.com/TgCatUB/catuserbot"><b>Upstream Repo</b></a>
</p>

<hr/>

<h2>✅ Before You Start</h2>
<ul>
  <li>GitHub account</li>
  <li>Card added in Fly Billing (no charge unless you upgrade)</li>
  <li>Terminal access (Linux / macOS / Windows / Termux)</li>
</ul>

<hr/>

<h2>1) 🧰 Install Fly CLI (<code>flyctl</code>)</h2>

<h3>🐧 Linux / 🍎 macOS</h3>
<pre><code>curl -L https://fly.io/install.sh | sh</code></pre>

<h3>🪟 Windows (PowerShell)</h3>
<pre><code>iwr https://fly.io/install.ps1 -useb | iex</code></pre>

<h3>🤖 Android (Termux)</h3>
<pre><code>pkg install root-repo
pkg install flyctl</code></pre>

<hr/>

<h2>2) 🔐 Login to Fly</h2>
<pre><code>flyctl auth login</code></pre>
<p>It will open a browser. Login using GitHub.</p>

<hr/>

<h2>3) 📦 Clone Nekopack</h2>
<pre><code>git clone https://github.com/tgcatub/nekopack/
cd nekopack</code></pre>

<hr/>

<h2>4) 🚀 Create the Fly App (<code>flyctl launch</code>)</h2>
<p>
  Run launch inside the project folder. Fly will create your app config (fly.toml) and guide you through setup.
</p>
<pre><code>flyctl launch</code></pre>

<ul>
  <li>If asked to overwrite Procfile → type <code>n</code></li>
  <li>Pick any app name you like</li>
  <li><b>Region tip:</b> choose <code>mia</code> (Miami) for good ping</li>
  <li>When asked for PostgreSQL → choose <b>Yes</b> and select <b>Development</b> plan</li>
</ul>

<p>
  <i>Why Postgres?</i> Catuserbot deployments commonly rely on a database. Fly can create + attach Postgres during launch.
</p>

<hr/>

<h2>5) 🗄️ (Optional) Manage Postgres Later</h2>

<p><b>List your Postgres clusters</b></p>
<pre><code>flyctl postgres list</code></pre>

<p><b>Attach an existing Postgres cluster to your app</b> (if you didn’t attach during launch)</p>
<pre><code>flyctl postgres attach &lt;POSTGRES_APP_NAME&gt; -a &lt;YOUR_APP_NAME&gt;</code></pre>

<p><i>Fly provides a dedicated command to attach Postgres to an app.</i></p>

<hr/>

<h2>6) 🔑 Add Secrets (Environment Variables)</h2>
<p>
  Fly secrets are stored securely and injected as environment variables at runtime.
</p>

<p><b>Bulk set secrets (copy-paste and fill values)</b></p>
<pre><code>flyctl secrets set \
APP_ID='' \
API_HASH='' \
ALIVE_NAME='' \
ALIVE_PIC='' \
STRING_SESSION='' \
TG_BOT_TOKEN='' \
PRIVATE_GROUP_BOT_API_ID='' \
COMMAND_HAND_LER='' \
ENV='ANYTHING' \
BADCAT='True' \
EXTERNAL_REPO='True' \
UPSTREAM_REPO='https://github.com/TgCatUB/catuserbot' \
TZ='Asia/Kolkata'</code></pre>

<p><b>Verify secrets exist</b></p>
<pre><code>flyctl secrets list</code></pre>

<hr/>

<h2>7) 🛠️ Configure Build (Recommended Approach)</h2>

<p>
  <b>Best practice:</b> If your repo already contains a Dockerfile, Fly will use it automatically.
  If it’s buildpack-based, Fly supports builders/buildpacks configuration in <code>fly.toml</code>.
</p>

<p><b>Open fly.toml</b></p>
<pre><code>nano fly.toml</code></pre>

<p>
  If your setup requires a Heroku-style buildpack builder, you can configure the build section.
  (Some projects use this to match Heroku build behavior.)
</p>

<p><b>Example build section</b> (only if your project needs it):</p>
<pre><code>[build]
  builder = "heroku/buildpacks"</code></pre>

<hr/>

<h2>8) 💾 Scale App Memory (Highly Recommended)</h2>
<pre><code>flyctl scale memory 2048</code></pre>

<p><b>(Optional) Scale DB memory too</b> (DB app name usually ends with <code>-db</code>):</p>
<pre><code>flyctl scale memory -a &lt;YOUR_APP_NAME&gt;-db 2048</code></pre>

<hr/>

<h2>9) 🚢 Deploy</h2>
<pre><code>flyctl deploy</code></pre>

<p><b>Watch logs</b></p>
<pre><code>flyctl logs</code></pre>

<hr/>

<h2>✅ Finish</h2>
<p>
  🎉 Your Catuserbot should now be running on Fly.io.<br/>
  If anything fails, the first thing to check is: <code>flyctl logs</code>
</p>

<hr/>

<h2>🧯 Quick Troubleshooting</h2>
<table>
  <tr>
    <th align="left">Issue</th>
    <th align="left">Fix</th>
  </tr>
  <tr>
    <td>Crash / restart loop</td>
    <td>Increase RAM: <code>flyctl scale memory 2048</code></td>
  </tr>
  <tr>
    <td>Secrets not working</td>
    <td>Re-set secrets and redeploy; confirm with <code>flyctl secrets list</code></td>
  </tr>
  <tr>
    <td>DB connection errors</td>
    <td>Ensure Postgres is attached (use <code>flyctl postgres attach</code>)</td>
  </tr>
</table>
