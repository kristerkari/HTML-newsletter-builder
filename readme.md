# HTML newsletter builder

HTML newsletter builder a command line tool to help you build and preprocess email newsletters. The idea behind HTML newsletter builder is to write clean HTML/CSS markup, and then process it to be more suitable for viewing in email client programs.

It is built using [HTML Email Boilerplate](http://htmlemailboilerplate.com/), [Jade](http://jade-lang.com/) (HTML templates), [Stylus](http://learnboost.github.com/stylus/) (CSS styles) and [Premailer](http://premailer.dialect.ca/) (Inline styles for the newsletter). It uses [Jake](https://github.com/mde/jake) as a build tool.

This tool is still very much work in progress, but hopefully it can become a solid base for building HTML newsletters.

## Installing

### Required software & libraries

To run the builder you need to install:

* [Ruby](http://www.ruby-lang.org/en/downloads/)  (you can also use [RVM](https://rvm.io/rvm/install/))
* [Node.js](http://nodejs.org/#download)
* [Jake](https://github.com/mde/jake) `npm install jake -g` *
* [Jade](https://github.com/visionmedia/jade) `npm install jade -g` *
* [Stylus](https://github.com/LearnBoost/stylus) `npm install stylus -g` *
* [Nokogiri](http://nokogiri.org/tutorials/installing_nokogiri.html) `gem install nokogiri` *
* [Premailer](https://github.com/alexdunae/premailer) `gem install premailer` *

\* add `sudo` in front of the command if needed

### Cloning with git | [git cloning guide](http://git-scm.com/book/en/Git-Basics-Getting-a-Git-Repository#Cloning-an-Existing-Repository)

You can start with cloning this repo from command line:
```
git clone https://github.com/kristerkari/HTML-newsletter-builder.git 'newsletters'
```

...and the move to the `newsletters` folder:
```
cd newsletters
```

## Making changes to the templates and stylesheets

### [jade guide](https://github.com/visionmedia/jade#syntax) | [stylus guide](http://learnboost.github.com/stylus/)

Templates for newsletters are written with Jade markup. Inline stylesheet for the newsletter is created from a Stylus stylesheet.

Newsletter template settings are still work in progress, and are most likely going to be easier to configure in the future. 

Here's how it's done currently:

**Setting files** can be found in `src/jade/settings/` folder. In the setting file you can setup your doctype and the name of your email template located in `src/jade/email/` folder.

**Newsletter templates** can be found in `src/jade/email`. This is the file when your newsletter tables and HTML markup should be written. If you change the name of the template file, don't forget to change it in the settings file too.

**Stylesheets** can be found in the `src/styl` folder. You should make all your CSS to this file. Please notice, that currently your `.styl` files need to be indented in the same way than in examples. I'm trying to get that fixed. If you change the name of the stylesheet file, don't forget to change it in the newsletter template file too.

## Building your newsletter

When you have made your changes, you can build your templates with Jake:
```
jake build
```

Rendered HTML templates can be found in the `lib` directory.

## Example template (HTML Email Boilerplate)

```jade
//- ===============================
//- HTML EMAIL BOILERPLATE
//- ===============================

head
  meta(http-equiv="Content-Type", content="text/html; charset=utf-8")
  meta(name="viewport", content="width=device-width, initial-scale=1.0")
  title Newsletter
  include boilerplate-styles
  //- Conditional comment targeting Windows Mobile
  // if IEMobile 7
    style(type="text/css")

  //- Conditional comment target Outlook 2007 and 2010
  // if gte mso 9
    style(type="text/css")

body
  //- Wrapper/Container Table: Use a wrapper table to control the width and the background color consistently of your email.
  //- Use this approach instead of setting attributes on the body tag.
  table(cellpadding="0", cellspacing="0", border="0", id="backgroundTable")
    tr
      td
        //- Tables are the most common way to format your email consistently. 
        //- Set your table widths inside cells and in most cases reset cellpadding, cellspacing, and border to zero. 
        //- Use nested tables as a way to space effectively in your message.
        table(cellpadding="0", cellspacing="0", border="0", align="center")
          tr
            td(width="200", valign="top")
            td(width="200", valign="top")
            td(width="200", valign="top")
        //- End example table

        //- Yahoo Link color fix updated: Simply bring your link styling inline.
        a(href="http://htmlemailboilerplate.com", target="_blank", title="Styling Links", style="color: orange; text-decoration: none;") Coloring Links appropriately

        //- Gmail/Hotmail image display fix: Gmail and Hotmail unwantedly adds in an extra space below images when using non IE browsers.
        //- This can be especially painful when you putting images on top of each other or putting back together an image you spliced for formatting reasons.
        //- Either way, you can add the 'image_fix' class to remove that space below the image.
        //- Make sure to set alignment (don't use float) on your images if you are placing them inline with text.
        img.image_fix(src="full path to image", alt="Your alt text", title="Your title text", width="x", height="x")

        //- Step 2: Working with telephone numbers (including sms prompts).
        //- Use the "mobile-link" class with a span tag to control what number links and what doesn't in mobile clients.
        span.mobile_link 123-456-7890

  //- End of wrapper table
```

## License

This software is released under the [MIT license](http://www.opensource.org/licenses/MIT)