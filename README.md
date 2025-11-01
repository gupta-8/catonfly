# Deploy Catuserbot on fly.io

[fly.io](http://fly.io) is free and perfect alternative to Heroku, but its not easy as that. we have to use terminal for deploy our userbot. Read this guide to deploy bot for yourself.

## Creating Account and adding Credit Card on Fly

first of all, create an account on Fly using GitHub from [fly.io/dashboard](http://fly.io/dashboard) and add credit card on billing section (you won't be charged until upgrading your plan to *Launch Plan*)

Now install its CLI on your Operating System,

- Linux:

`url -L https://fly.io/install.sh | sh`

- Windows (Powershell)

`iwr https://fly.io/install.ps1 -useb | iex`

- Android (Termux)

first do:

`pkg install root-repo`

then run the below command

`pkg install flyctl`

- MacOS

`curl -L https://fly.io/install.sh | sh`

## Authenticating Terminal with Fly

run `flyctl auth login` it will redirect to login page, login with GitHub there.

## Clone and Launch Catuserbot in terminal

Git clone or download Nekopack from GitHub or just copy and paste `git clone [https://](https://tgcatub)github.com/tgcatub/nekopack/`

then do: `cd nekopack`

Now, Launch the Nekopack into [fly.io](http://fly.io) server using `flyctl launch`

(it will ask for overwriting the Procfile, just type `n` there)

![Screenshot_20220922-231828_Termux.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fae42130-47a4-4292-aab3-ca4d57e3250e/Screenshot_20220922-231828_Termux.png)

Now it will ask for Name of the application and server of application

*Tip: choose Miami (mia) server for good ping and fast response*

![Screenshot_20220922-232334_Termux.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/435109c8-97f8-4739-ba07-9f3682ab99db/Screenshot_20220922-232334_Termux.png)

Now it will ask for setting up Postgresql for our app, type `y` there and select Development plan.

![Screenshot_20220922-232455_Termux.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/65aa282b-bbee-4f05-ae20-80067d35ae74/Screenshot_20220922-232455_Termux.png)

It will automatically create postgresql and connect it for our bot.

*Tip: Scale your Database memory using `flyctl scale memory -a your-appname-db 2048`*

*(add -db in end of your app name, like here i am doing with my app: `flyctl scale memory -a harsh-cat-db 2048` it will scale your memory to 2 GB of ram)*

## Adding Secrets and editing fly.toml

add secrets (variables) for your app using `flyctl secrets set VAR_NAME=’value’`

Add the below method to bulk set the secrets using single command

*Tip: paste this on any text editor and add the vars then paste it on your terminal.*

`flyctl secrets set \APP_ID='' \`

`API_HASH='' \`

`ALIVE_NAME='' \`

`ALIVE_PIC='' \`

`STRING_SESSION='' \`

`TG_BOT_TOKEN='' \`

`PRIVATE_GROUP_BOT_API_ID='' \`

`COMMAND_HAND_LER='' \`

`ENV='ANYTHING' \`

`BADCAT='True' \`

`EXTERNAL_REPO='True' \`

`UPSTREAM_REPO='https://github.com/TgCatUB/catuserbot'  \`

`TZ='Asia/Kolkata’`

Now edit the fly.*toml using nano or any text editor* file and replace `paketobuildpacks/builder:base` with `heroku/buildpacks` in `builder` variable

![Screenshot_20220922-234341_Termux~2.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a6a4d1e8-f023-4ec6-b94a-0b79796b0dc5/Screenshot_20220922-234341_Termux2.png)

Now scale the memory of your app also using `flyctl scale memory 2048`

## Deploying The App

type `flyctl deploy` and wait few minutes until it deploy successfully…

![Screenshot_20220922-235013_Termux~2.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/17bf8c88-8fd2-4117-aab8-1e4192b14fb8/Screenshot_20220922-235013_Termux2.png)

![Screenshot_20220922-235144_Termux.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9655bba7-8683-421f-be20-4d2a338a7e8c/Screenshot_20220922-235144_Termux.png)

*Wait for 5-6 Minutes Until it deployed on fly.io*

Meanwhile Logs can be also view from [fly.io/dashboard](http://fly.io/dashboard) or type `flyctl logs` on terminal

![Screenshot_20220922-235616_Termux.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c6e38463-71f4-4314-b32d-7e9556c2b007/Screenshot_20220922-235616_Termux.png)

![Screenshot_20220922-235609_Chrome Beta.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2c093b20-34a0-46a9-be03-20ec3beae24f/Screenshot_20220922-235609_Chrome_Beta.png)
