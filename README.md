repository: bots/discord/03-discordjs

variations:
  - name: "With Env"
    lang: "Nodejs"
    folder: with-env

links:
  - title: "discord.js"
@@ -15,6 +21,10 @@ links:
    url: https://www.disstreamchat.com/
  - title: "The Coding Train Discord"
    url: /discord
  - title: "Choo choo bot on Glitch"
    url: https://glitch.com/~choo-choo-bot-discord
  - title: "Discord Bot Choo Choo GitHub Repository"
    url: https://github.com/CodingTrain/Discord-Bot-Choo-Choo

videos:
  - title: "Server Side with Node.js"
 6  learning/bots/discord/03-discordjs/Nodejs/bot.js 
@@ -1,3 +1,9 @@
// Coding a Bot with discord.js
// Discord Bots
// The Coding Train / Daniel Shiffman
// https://thecodingtrain.com/learning/bots/discord/03-discordjs.html
// https://youtu.be/8k-zyUyuvlM

console.log('Beep beep! 🤖');

const Discord = require('discord.js');
 3  learning/bots/discord/03-discordjs/with-env/.env-sample 
@@ -0,0 +1,3 @@
SERVERID=123456789
CHANNELID=123456789
TOKEN=123456789 
 3  learning/bots/discord/03-discordjs/with-env/.gitignore 
@@ -0,0 +1,3 @@
node_modules
.env
.DS_Store 
 21  learning/bots/discord/03-discordjs/with-env/LICENSE 
@@ -0,0 +1,21 @@
MIT License

Copyright (c) 2020 Daniel Shiffman

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
 98  learning/bots/discord/03-discordjs/with-env/README.md 
@@ -0,0 +1,98 @@
# Choo Choo Discord Bot!

[<img src="https://i.ytimg.com/vi/7A-bnPlxj4k/maxresdefault.jpg" alt="Discord Bot Tutorial" width="320">](https://www.youtube.com/playlist?list=PLRqwX-V7Uu6avBYxeBSwF48YhAnSn_sA4)

🚂🌈💖🤖 All aboard! [Coding Train Tutorial Videos](https://www.youtube.com/playlist?list=PLRqwX-V7Uu6avBYxeBSwF48YhAnSn_sA4) 🚂🌈💖🤖

## Steps to create new bot 

1. Create node project and install discord.js module.

```
$ npm init
$ npm install discord.js
```

2. [Create an application](https://discord.com/developers/applications/) - optionally set name, description, avatar.

3. Select Bot from left navigation and "Add Bot" - set name and icon.

4. Add bot to the A2Z server with the url: `https://discord.com/oauth2/authorize?client_id=YOUR_CLIENT_ID&scope=bot`

5. Write the code!

Login to bot account:
```javascript
const Discord = require('discord.js');
const client = new Discord.Client();
client.login('YOUR BOT TOKEN');
```

Callback for when the bot is connected and ready:
```javascript
client.once('ready', () => {
  console.log('Ready!');
});
```

Callback for when a message is posted:
```javascript
client.on('message', gotMessage);
function gotMessage(msg) {
  console.log(msg.content);
}
```

9. Run the bot!

```
$ node index.js
```

## Limit to one server and one channel

1. Enable developer mode in Discord (Settings->Appearance->Enable Developer Mode).
2. Copy server ID.
3. Copy channel ID.

```javascript
const serverID = 'SERVER ID';
const channelID = 'CHANNEL ID';
client.on('message', gotMessage);
function gotMessage(msg) {
  // Only for this server and this channel
  if (msg.guild.id === serverID && msg.channel.id === channelID) {
    // Reply to the message ping!
    if (msg.content === 'ping') {
      msg.channel.send('pong');
    }
  }
}
```

## Store token and other secrets in .env file.

1. Install [dotenv package](https://www.npmjs.com/package/dotenv).
```
$ npm install dotenv
```

2. Create `.env` file:

```
SERVERID=123456789
CHANNELID=123456789
TOKEN=123456789
```

3. Load environment variables using `dotenv` and `.env`:

```javascript
require('dotenv').config();
const serverID = process.env.SERVERID;
const channelID = process.env.CHANNELID;
const TOKEN = process.env.TOKEN;
```
 46  learning/bots/discord/03-discordjs/with-env/index.js 
@@ -0,0 +1,46 @@
// Coding a Bot with discord.js (With Env)
// Discord Bots
// The Coding Train / Daniel Shiffman
// https://thecodingtrain.com/learning/bots/discord/03-discordjs.html
// https://youtu.be/8k-zyUyuvlM

const Discord = require('discord.js');
const client = new Discord.Client();

require('dotenv').config();

const serverID = process.env.SERVERID;
const channelID = process.env.CHANNELID;

console.log('Beep beep! 🤖');

const Discord = require('discord.js');
const client = new Discord.Client();
// I recommend using dotenv, you can see how the project is setup here: 
// https://github.com/CodingTrain/Discord-Bot-Choo-Choo
// dotenv will be covered in a future video
client.login(process.env.TOKEN);

client.on('ready', readyDiscord);

function readyDiscord() {
  console.log('💖');
}

const replies = [
  '🚂🌈💖',
  'Choo choo!',
  'Ding! 🛎',
  'Never forget this dot!'
]

client.on('message', gotMessage);

function gotMessage(msg) {
  if (msg.guild.id === serverID && msg.channel.id === channelID) {
    if (msg.content === '!choochoo') {
      const index = Math.floor(Math.random() * replies.length);
      msg.channel.send(replies[index]);
    }
  }
}
 112  learning/bots/discord/03-discordjs/with-env/package-lock.json 
Some generated files are not rendered by default. Learn more.

 23  learning/bots/discord/03-discordjs/with-env/package.json 
@@ -0,0 +1,23 @@
{
  "name": "discord-bot-a2z",
  "version": "1.0.0",
  "description": "A discord bot example for A2Z",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/shiffman/Discord-Bot-A2Z.git"
  },
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/shiffman/Discord-Bot-A2Z/issues"
  },
  "homepage": "https://github.com/shiffman/Discord-Bot-A2Z#readme",
  "dependencies": {
    "discord.js": "^12.3.1",
    "dotenv": "^8.2.0"
  }
}
