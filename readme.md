# HTML newsletter builder

HTML newsletter builder a command line tool to help you build and preprocess email newsletters. The idea behind HTML newsletter builder is to write clean HTML/CSS markup, and then process it to be more suitable for viewing in email client programs.

It is built using [HTML Email Boilerplate](http://htmlemailboilerplate.com/), [Jade](http://jade-lang.com/) (HTML templates), [Stylus](http://learnboost.github.com/stylus/) (CSS styles) and [Premailer](http://premailer.dialect.ca/) (Inline styles for the newsletter). It uses [Jake](https://github.com/mde/jake) as a build tool.

This tool is still very much work in progress, but hopefully it can become a solid base for building HTML newsletters.

## Installing

### Required software & libraries

To run the builder you need to install:

* [Ruby](http://www.ruby-lang.org/en/downloads/)
* [Node.js](http://nodejs.org/#download)
* [Jake](https://github.com/mde/jake) `npm install jake -g`
* [Jade](https://github.com/visionmedia/jade) `npm install jade -g`
* [Stylus](https://github.com/LearnBoost/stylus) `npm install stylus -g`
* [Nokogiri](http://nokogiri.org/) `sudo gem install nokogiri`
* [Premailer](https://github.com/alexdunae/premailer) `sudo gem install premailer`

### Cloning with git

You can start with cloning this repo from command line:
```
git clone https://github.com/kristerkari/HTML-newsletter-builder.git 'newsletters'
```

...and the move to the `newsletters` folder:
```
cd newsletters
```

### Making changes to the templates and stylesheets

Template(s) for newsletter(s) are written with Jade markup. Inline stylesheet for the newsletter is created from a Stylus stylesheet.

Newsletter template settings are still work in progress, and are most likely going easier to configure in the future. 

Here's how it's done currently:

Setting file(s) can be found in `src/jade/settings/` folder. In the setting file you can setup your doctype and the name of your email template located in `src/jade/email/` folder.

Main newsletter template(s) can be found in `src/jade/email`. This is the file when your newsletter tables and HTML markup should be written. If you change the name of the template file, don't forget to change it in the settings file too.

Stylesheet(s) can be found in the `src/styl` folder. You should make all your CSS to this file. Please notice, that currently your `.styl` files need to be indented in the same way than in examples. Trying to get that fixed. If you change the name of the stylesheet file, don't forget to change it in the newsletter template file too.

### Building

When you have made your changes, you can build your templates with Jake:
```
jake build
```

Rendered HTML templates can be found in the `lib` directory.

## License

This software is released under the [MIT license](http://www.opensource.org/licenses/MIT)