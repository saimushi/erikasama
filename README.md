# Eris Discord Bot Example

An very simple example/tutorial on how to make a Discord Bot with the library Eris by murf#4142

### Requirements

 - [Discord Account](https://discordapp.com)
 - A server with the right permissions to add your bot to.
 ![Permission](https://cdn.glitch.com/dae81fe2-1fdf-4980-805e-76c7fa26dfef%2FCA0906CC-4EDA-401E-8440-56E10595B36D.jpeg?1527422600325)

### Steps

* Create a Discord Bot account on: [https://discordapp.com/developers/applications/me](https://discordapp.com/developers/applications/me)

* Click this button:
![New App](https://cdn.glitch.com/dae81fe2-1fdf-4980-805e-76c7fa26dfef%2F356CAEAD-E000-4A50-AFF8-F44FA28BCD23.jpeg?1527422848543)

* Then fill out the forms you want but make sure you don't do the Redirect URI(s) form. Then, click `Create App` button and it will redirect you to the new bot's account page.

* Create a Bot User by pressing the button further down the page like below.
![Create a Bot User](https://cdn.glitch.com/dae81fe2-1fdf-4980-805e-76c7fa26dfef%2FCD437C75-7818-4D4D-8A81-57D6E5B82CD6.jpeg?1527423089823)

* Then this will show up:
![Bot User](https://cdn.glitch.com/dae81fe2-1fdf-4980-805e-76c7fa26dfef%2F5386D4DB-9582-444B-8116-613EFDFA9C6D.jpeg?1527424952690)

* You can make public only if you want other people to be able to add your bot.

* Get the bot's token:
![Token](https://cdn.glitch.com/dae81fe2-1fdf-4980-805e-76c7fa26dfef%2F436140A7-107C-49C3-A8F1-CCBC34A0D86F.jpeg?1527424952990)

* **MAKE SURE YOU NEVER SHOW ANYBODY THIS TOKEN!**

* Open up the `.env` file in your [https://glitch.com](https://glitch.com) and place your token next to the `=` sign and make sure there is no spaces at all

* Add the App Bot User to your Discord server using this link: `https://discordapp.com/oauth2/authorize?&client_id=<CLIENT ID>&scope=bot&permissions=0`

* Replace`<CLIENT_ID>` with the Client ID found on the page of your Application Page.

### Code

* Open up the `server.js` file to see all of the code.

* To interact with Discord's API (To make your bot), we are using the [Eris](https://abal.moe/Eris) library.

* Once everything in place is done, open up `Logs` and you would be able to see  that it said `Eris Bot is Online`.

### Example

Whenever you type `!example` it will send you a message in that Discord channel.
![Example](https://cdn.glitch.com/dae81fe2-1fdf-4980-805e-76c7fa26dfef%2FB0E4CDE6-BD36-4EB2-B713-1206D474392E.jpeg?1527425129428)

### Keeping your Bot Online

* You need to go into the package.json file and click `Add Package` button and search for `express` package unless `express` is already in the package.json file, no need to add the package.

* Add this code on the bottom lines of `server.js`:

```js
const http = require('http');
const express = require('express');
const app = express();
app.get("/", (request, response) => {
  console.log(Date.now() + " Ping Received");
  response.sendStatus(200);
});
app.listen(process.env.PORT);
setInterval(() => {
  http.get(`http://${process.env.PROJECT_DOMAIN}.glitch.me/`);
}, 280000);
```

### Make the bot don't auto restart on change

* Make a file by clicking the `+ New File` button above assets and name it `watch.json`

* Add this code inside that file:

```json
{
  "install": {
    "include": [
      "^package\\.json$",
      "^\\.env$"
    ]
  },
  "restart": {
    "exclude": [
      "^public/",
      "^dist/"
    ],
    "include": [
      "\\.js$",
      "\\.json"
    ]
  },
  "throttle": 900000
}
```

This is very helpful since Discord disconnects your bot and forces you to reset your token after 1000 logins. This means, when type up to 1000 characters, it is  quite an issue.