<div align="center">

<img src="https://i.imgur.com/QCxOSK5.png" alt="Logo" width="500"/>

#### SquadStatsJS PRO

[![GitHub contributors](https://img.shields.io/github/contributors/11TStudio/SquadStatsJSPRO.svg?style=flat-square)](https://github.com/11TStudio/SquadStatsJSPRO/graphs/contributors)
[![GitHub release](https://img.shields.io/github/license/11TStudio/SquadStatsJSPRO.svg?style=flat-square)](https://github.com/11TStudio/SquadStatsJSPRO/blob/master/LICENSE)

<br>

[![GitHub issues](https://img.shields.io/github/issues/11TStudio/SquadStatsJSPRO.svg?style=flat-square)](https://github.com/11TStudio/SquadStatsJSPRO/issues)
[![GitHub pull requests](https://img.shields.io/github/issues-pr-raw/11TStudio/SquadStatsJSPRO.svg?style=flat-square)](https://github.com/11TStudio/SquadStatsJSPRO/pulls)
[![GitHub issues](https://img.shields.io/github/stars/11TStudio/SquadStatsJSPRO.svg?style=flat-square)](https://github.com/11TStudio/SquadStatsJSPRO/stargazers)

<br>

[![](https://img.shields.io/badge/discord.js-v13.0.0--dev-blue.svg?logo=npm)](https://github.com/discordjs)

<br>
<br>

</div>

## About

All-in-one advanced discord bot and website combo.<br>
Manage your Squad server from the new dashboard/panel using already existing RCON connection of your SquadJS application, no redundant RCON connections!<br>
Use in-game map voting ability and squad stats track to entertain your players.<br>
Make custom suggestions and event registrations from Discord.<br>

<br>
For squad usage you NEED to have `SquadJS/socket.io` and `SquadJS/dblog` configured.

## Using SquadStatsJS PRO

The general usage can be found on the help command.
Soon there will be a written usage guide and/or a video example.

### Prerequisites

- Git
- MongoDB ([Windows](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#download-the-installer) || [Linux](https://docs.mongodb.com/manual/administration/install-on-linux/))
  - Just download and install it, or use the the free service of MongoDB -> Mongo Atlas Cloud.
- [Node.js](https://nodejs.org/en/) (^16.2) - [Download](https://nodejs.org/en/)
  - This will be used for DiscordJSv13
- NPM
  - Recommended version: 7.20.x
- SquadJS
  - MySQL server configured. If you want to use mysql 8.x than I recommend you to use the <code>mysql_native_password</code> authentication plugin. More can be found here <a>https://stackoverflow.com/a/50131831/12628648 </a>
  - <code>SquadJS/socket.io</code> and <code>SquadJS/dblog</code> configured.

### Updating from v2.0 to v2.1

Unfortunately there is no script to upgrade your old version to the latest and the reason for that is because there was an whole rewrite of the bot. Therefor major code changes and db schema changes were made that it makes it very hard to me to write a script to update everything without losing data.

If you want to update you should **remove** everything that you already have from SquadStatsJSPRO v2 and clone this instead.

What is changed:

- Website hosted at the IP of your bot's machine.
- Panel for players and admins to manage the server and see profile stats.
- No more useless discord commands. Just commands about squad.
- An API that you can build up on.
- Major RAM usage stays between **30-100MB**!
- Again there is no need for yet another RCON connection, SquadStatsJSPRO uses the **already** existing RCON connection from SquadJS.

### Installation

1. Clone the repository via your terminal/cmd: `git clone https://github.com/11TStudio/SquadStatsJSPRO`
2. Configure the `config.example.js` file. And when done SAVE and delete the .example. (At the end the file should look like: `config.js`)
   - Once you have completed stap 3 (below) run also <code>npm run testcfg</code> to see if everything is configured fine.
3. Run `npm install` via the terminal.
4. Start your bot: `node index.js&`. (**I recommend you to use [pm2](https://pm2.keymetrics.io)**)
5. Star this repo if you liked!

### Configuring - SquadStatsJS PRO

SquadStatsJS PRO can be configured via .js file which by default is called `config.example.js`

The config file needs to be called `config.js` at the end and a example can be found below:

PS: Configure this file as first thing before you do anything :)

```js
module.exports = {
	/* The token of your Discord Bot */
	token: "Discord_Bot_Token",
	/* The main Discord server ID */
	serverID: "Discord_Server_ID",
	/* The Battle Metrics Server ID of your squad server */
	squadBattleMetricsID: "BattleMetrics_ServerID",
	/* For the support server */
	support: {
		logs: "827885263438217226", // And the ID of the logs channel of your server (new servers for example)
		debug: false, // Will activate debug mode.
	},
	/* SocketIO details */
	socketIO: {
		enabled: true, // whether the squad map voting is enabled or nothing
		ip: "194.26.183.182", // The IP address where SquadJS is installed.
		port: "7777", // The port for socket.IO
		token: "MyPasswordForSocketIOFromSquadJS", // Password for socket.IO
	},
	/* Dashboard/Website configuration */
	dashboard: {
		enabled: true, // whether the dashboard is enabled or not
		secret: "MyDiscordBotSecret", // Your discord client secret
		/* don't forget to add "<baseURL>/api/callback" at the discord bot whitelisted url's/OAuth2 */
		baseURL: "http://my-domain.com", // The base URl of the dashboard without "/" at the end
		port: 80, // Dashboard port
		expressSessionPassword: "UcPT5Enzmhk_ARFVrGyDZ3WjJvSe!9", // Change this to something else!!! (Use: https://passwordsgenerator.net/plus/ to generate a new one)
		failureURL: "http://my-domain.com", // url on which users will be redirected if they click the cancel button (discord authentication) or logout
	},
	/* The URl of the mongodb database (SECURE YOUR CONNECTION IF YOU WILL USE IT REMOTELY) */
	/* 	More info on:	https://docs.mongodb.com/manual/reference/connection-string/ */
	mongoDB: "mongodb://localhost:27017/V3", // if remote hosted: "mongodb://username:password@host:port/database"
	/* The default prefix for using the bot, you can also change this from dashboard or discord command (setprefix) */
	prefix: "v3!",
	/* For the embeds (embeded messages) */
	embed: {
		color: "#0091fc", // The default color for the embeds
		footer: "LeventHAN | l-event.studio", // And the default footer for the embeds
	},
	/* Bot's owner informations */
	/* Change this to your own ID (and name?), as this will be used to give you permission at the dashboard when configuring it! */
	owner: {
		id: "152644814146371584", // The ID of the bot's owner (for the dashboard to give access to configurations)
		name: "LeventHAN#0001", // And the name of the bot's owner (just for statistics)
	},
	/* The API keys that are required for certain commands */
	apiKeys: {
		steam: "MySteamKeyToken", // Will be used for logging (Obtain by filling your domain or IP here: https://steamcommunity.com/dev/apikey)
		battleMetrics: "MyBattleMetricsToken", // Will be used to sync with your Battle Metrics server (Obtain from: https://www.battlemetrics.com/developers)
	},
	/* The others utils links */
	others: {
		github: "https://github.com/11TStudio", // Founder's github account
		donate: "https://github.com/sponsors/11TStudio", // Sponsor Link (donate if you liked this project <3)
	},
	/* The Bot status */
	status: [
		{
			name: "👀 looking for your stats",
			type: "LISTENING",
		},
		{
			name: "SquadStatsJS PRO™",
			type: "PLAYING",
		},
	],
};
```

## Commands and Examples

Soon there will be more examples and screenshots!

<details>
      <summary>help</summary>
      <h2>Help Embed</h2>
      <p>Shows all commands with more info when used as following: `!help <command-name>`</p>
      <h3>Example image</h3>
       <div align="center">
       <img src="https://i.imgur.com/ZCCJV5H.png" alt="Example !profile"/>
       </div>
</details>

<details>
      <summary>profile</summary>
      <h2>Search for players statistics</h2>
      <p>The <code>profile</code> command will show the player stats.</p>
      <h3>Example after linking your steamUID</h3>
       <div align="center">
       <img src="https://i.imgur.com/pSxuO8G.png" alt="Example !profile"/>
       </div>
</details>

## Credits

- [SquadJS](https://github.com/Thomas-Smyth/SquadJS) - The reason this bot is made.
- The [Contributors](https://github.com/11TStudio/SquadStatsJSPRO/graphs/contributors), for helping me build this amazing multi-purpose bot.
- My [Sponsors](https://github.com/sponsors/11TStudio?preview=true), for supporting me and giving me the possibility to make this project.

## License

```
MIT License

Copyright (c) 2021 11T Studio

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

```
