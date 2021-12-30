# Discord.js Guide

## Creating your bot

The recommended bot hosting platform is [Replit](https://replit.com).

- Create a Discord Application on your [Discord Developer Dashboard](https://discord.com/developers/applications).
- Fork [this repl](https://replit.com/@akhilpil0308/Discordjs-Template).
- Add your bot's command prefix in `config.js` (i.e. `prefix: '!'`). The example prefix used here is `!`.
- Add your bot token (select your application, click "Bot", and click "Copy" under the "Token" category) as an environment variable (click the lock in the Replit sidebar.)
- Create an invite link in the following format: `https://discord.com/api/oauth2/authorize?client_id=${a}&permissions=${p}&scope=bot%20applications.commands` where `${a}` is your Application ID from the [Discord Developer Dashboard](https://discord.com/developers/applications), and `${p}` is the permissions integer you generate at the bottom of your application's "General Information" page.
- Open that link in a new tab to invite your bot to a server.
- Run the repl (click "Run" at the top).
- Open Discord and type `!help`. A help menu should be sent by the bot. Also run `!ping`, which will send a message saying how long the transmission between Replit and Discord takes.

## Setting up UptimeRobot

If you have the [Replit Hacker Plan](https://replit.com/site/pricing), you can just turn on "Always on repl". However, if you don't want to pay, you can use a free service called [UptimeRobot](https://uptimerobot.com). After you create an account, click "Add New Monitor". Choose "HTTPS", and enter a name and the URL of your web server (`https://replprojectname.username.repl.co`). UptimeRobot's computers will keep pinging the URL every 5 minutes so that the repl doesn't "fall asleep".

## Customizing your bot (a.k.a. writing your own code)

This is inevitable. A help menu and a ping command don't fit your needs. You will have to write your own commands. This section will help get you started.

```JAVASCRIPT
switch(command) {
  case 'sayhello':
    message.channel.send('Hello!'); // "Hello!" Just sends your message.
    message.reply('Hello!'); // "@userwhocalled, Hello!" Mentions the user, then adds your message.
    break;
  case 'embed':
    let thisArg = args[1]
    let thisEmbed = new MessageEmbed()
      .setTitle('ThisEmbed')  // Important: Note that there is no semicolon at the end of the line.
      .setDescription('A MessageEmbed')
      .addField('fieldname', 'fielddescription')
      .addFields(
        { name: 'fieldname', value: 'fieldvalue', inline: 'false' } // inline is optional, default is false
        { name: 'Argument 1', value: `${thisArg}` }  // `${variable}` returns the value of the variable, so `The first argument is ${thisArg}` would return "The rist argument is " and then the value of thisArg.
      )
      .setColor('#3D8E6A')  // Hexadecimal, RGB array (i.e. [255, 13, 183]), or one of the colors listed at https://discord.js.org/#/docs/main/stable/typedef/ColorResolvable.
      .setTimestamp() // Not really necessary
      .setImage('https://images.com/someimage')  // Any URL that leads to an image
      .setFooter('The footer') // The footer of the embed
      .setThumbnail('https://images.com/randomimage');  // Any image URL. The semicolon at the end of this line is necessary!
      message.channel.send(thisEmbed);
    break;
}
```

Another thing that will eventually happen: You won't know how to get or do something. Let's say you can't make a message that says "The potato called *mention the message author* is a potato." Look at [the documentation](https://discord.js.org/#/docs/main/stable/general/welcome) or [the guide](https://discordjs.guide). You know that `message` is of type `Message`, so you search for that. `Message` turns out to have the property `author`. And `Message.author` is of type `User`. And `User` has the property `id`, which returns the user's Discord ID. Put together, you get `Message.author.id`. But in our code, the `Message` is `message`. But what do you do with the user's ID? After searching for this on [StackExchange](https://stackexchange.com), you learn that the syntax for mentioning user with an ID  of `1234567890` is as follows: `<@!1234567890>`. So your code would look like this: ```message.channel.send(`The potato called <@!${message.author.id}> is a potato.`);```

If people have posted their code, and the license allows you to use it, and you need it, use it! Don't spend an hour reinventing the wheel. On the occasion that you cannot find what you are looking for, write it yourself! One trick: Use python3's `sys.argv[]` (command-line arguments) and `print()` to model your function first, then modify it for JavaScript and Discord.js.
