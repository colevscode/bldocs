{{$meta}}
type: guide
title: Overview
order: 1
{{$endmeta}}

{{$layout /index.html as content}}


## Getting started

Check out the [Quickstart guide](/guides/quickstart.html) for a walk-through of creating your first project. This will include a discussion of how to create a website, how to make changes, and how to configure your website.

## Backlift template tags

Backlift provides a template language that you can use to construct dynamic websites. If you've ever created a Tumblr theme, or worked with a server-side templating language, like Django's template language, or Ruby on Rails' ERB templates, you'll have no trouble picking up the Backlift template system. 

Backlift's template language natively understands APIs. With Backlift template tags, you can incorperate data from the Backlift API or 3rd party APIs directly into your HTML. This makes it possible to embed a list of posts from the Tumblr API, or display a list of products, just by adding a few template tags. More information is available in the [template language guide](/guides/templatelang.html).

## Backlift analytics

All backlift projects come with simple analytics out of the box. You can use backlift analytics to see how many users visit your website, track conversions, and set up variations of your website for A/B testing. Take a look at the [analytics guide](/guides/analytics.html) for more details.

## Using Markdown, SASS, LESS or CoffeeScript

Backlift makes it easy to incorporate productivity tools like Markdown and SASS. Whenever you save a file in your Dropbox, Backlift checks the file extension (such as myfile.sass) to determine if it should convert the file into HTML, CSS or JavaScript. If so it will run a *preprocessor* on the file, and add the generated file to your website. You won't see these generated files in your Dropbox, but you can use them in your web pages. For more details, see the [preprocessor guide](/guides/preprocessors.html).

## The Backlift API

Most of the power of Backlift comes from it's API, especially when coupled with the Backlift template language. Backlift provides APIs for user management, data storage and retrieval, and connecting to third party APIs. You can find out more about these APIs with the following guides:

- The [Backlift Data API](/guides/persistence.html) lets you store and retrieve data
- The [Backlift Authorization API](/guides/authorization.html) lets you create users and log in
- The [Backlif Tunnel API](/guides/tunnel.html) lets you connect to third pary APIs easily



<!--
For a list of Backlift variables, please see the [variables reference](variables.html).

For more information about the configuration options available in the config.yml file, see the [configuration reference](configuration.html).
-->

