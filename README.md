# 👋🏽 Hello, ai2html!

A step-by-step guide to creating a simple, responsive chart.

This tutorial will walk you through the process of building a static — yet responsive — chart with the ai2html tool. ai2html is an open-source tool developed by the New York Times that converts your Illustrator documents into html and css.

This tutorial is based on lessons by Jonathan Soma and uses documentation from the [ai2html](http://ai2html.org/) webpage. The structure of the tutorial draws inspiration from the [First News App](https://first-news-app.readthedocs.io/en/latest/#) tutorial by Ben Welsh.

## ✅ Prelude: Prerequisites
Before you can begin, here is what you will need to finish this walkthrough:
- Abobe Illustrator
- A code editor

## 📚 Act 1: Hello, assets!
This GitHub repository will include all the code files that you will need to walkthrough. Here you find:
- ai2html script (which can also be found [here](https://raw.githubusercontent.com/newsdev/ai2html/master/ai2html.js))
- a .ai file with a graphic that's ready to be exported
- an ai2html-config.json file
- a JavaScript resizer function

## 👀 Act 2: Hello, ai2html script!
Before we get started with out graphic, we need to tell Illustrator what ai2html means, and what we expect it to do. To achieve this, we are going to feed Illustrator the [ai2html](assets/ai2html.js) script, which is developed by the New York Times.

Download [this](assets/ai2html.js) script, and the Times recommends saving it in the Illustrator folder, where other scripts are located.

For instance, if you are running Adobe Illustrator CC 2014, the path would be:
```bash
Adobe Illustrator CC 2014/Presets/en_US/Scripts/ai2html.js
```

💡 Tip: When you're saving the script to your folder, make sure it's saving as JavaScript, `.js`, and not HTML, `.html`.

## 🎨 Act 2: Hello, Illustrator (hey there, artboards)!
Adobe Illustrator allows us to create multiple artboards for an illustrator. This is the property we'll use to ask Illustrator to generate responsive graphics. 

Open Illustrator and get started with an artboard, which you will use to create a graphic for desktop. I'd recommend setting dimensions accordingly, for instance, 800 pixels wide and 500 pixels tall. Name this artboard "desktop."

This is great for desktop, but it may not work very well for handheld. Phones — and tablets, generally — are vertical and a landscape graphic may not work the best. 

Create another artboard, this time, keep in mind that this version of the graphic is going to to be viewed solely on handheld devices. I'd recommend setting dimensions accordingly, perhaps 400 pixels wide and 1000 pixels tall. Let's name this artboard "handheld."


## 🖥 Act 3: Hello, HTML!

Let's export the graphic to see what happens. Click on `File > Scripts > Other Script... > ai2html.js`.

Let Illustrator process this and let's see what message we get. **Do not close out of the message just yet.**

Looks like — for the most part — the graphic was successfully exported. Yay! Let's go back to the file explorer to see what happened. 

Illustrator should have created an `output` folder, with two PNG files and an HTML file. Open the HTML file!

This is not what we wanted. We have a single HTML page with graphics from both artboards. 

🤓 Also, if you're a font nerd like me, yes, this is not Helvetica. 

💪🏽 Don't give up just yet! We'll fix these problems one step at a time.

## 👮🏽 Act 4: Hello, rules!

Let's go back to the Illustrator and see what the error messages are saying. Looks like it gave us a warning about fonts.

When ai2html script turns Illustrator files into HTML, it's converting fonts that live in the Adobe world, so fonts that live on the web. And we need to help ai2html translate fonts.

In the assets folder, we have a `ai2html-config.json` file. Let's bring it to **same directory that your `.ai` file is in.** Let's open it.

This file is a set of rules written in JSON (JavaScript Object Notation). This is where we will feed our rules for fonts.

Let's go back to Illustrator and **copy the name of the font** it's looking to translate: `Helvetica-Bold`.

For the world wide web, this particular font is called `Helvetica Neue`.

Potato Potahto, I know!

In the `ai2html-config.json` — which should be sitting in the same directory as your `.ai` file — let's change the first `ai-font` to `Helvetica-Bold`. For this font, we the family to be `Helvetica Neue`. And since it's bold, let's give it a weight of 600.

In Illustrator, execute the script again. `File > Scripts > Other Script... > ai2html.js`

Open the HTML file, and the font should be fixed!


## 👨‍💻 Act 5: Hello, JavaScript! 
For the most part, things look great, but one problem still stands: We are still seeing both artboards at once. Let's fix that.

Thankfully, the developers at the Times have given us a nifty resizer script that we can simply add to our graphic HTML output, and it will do the rest for us. Pretty neat.

Head over to the [resizer script](assets/resizer_script.html) and copy it to your clipboard.

Open up the graphic HTML output in your code editor, and paste it on top of the graphic that ai2html has output.

Give the HTML file all the necessary attributes, so that your browser knows your rendering HTML. Your HTML file should look like this
```bash
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>

    <!-- Resizer script -->
    <!-- ai2html output content -->
</body>
</html>
```

💡 Tip: If you re-export your graphic, you will have to paste your resizer script again, because it will dissappear. 

Let's see what this looks like in a browser. Yay! We created a graphic that's resizing according to browser width AND the font-family is fixed!

## 🪖 Epilogue: Hello, deployment!
You can publish this graphic on GitHub pages or deploy it on a cloud application platform such as Heroku. Use an IFrame embed code to embed the graphic in your story — and you're good to go!