{{$meta}}
type: guide
title: Quick Start
order: 0
{{$endmeta}}

{{$layout /index.html as content}}

<div class="videocontainer">
<div class="video" style="padding: 10px;">
    <iframe width="100%" height="100%" src="http://www.youtube.com/embed/ScMzIvxBSi4?feature=player_detailpage" frameborder="0" allowfullscreen></iframe>
</div>
</div>

Welcome to Backlift. This guide will quickly walk you through the basics of creating a Backlift website, making some changes, adding dynamic data with template tags, and deploying your site to production. Let's get started!

## Creating a website

You can create a new website in just a few steps. First visit the [Backlift home page](backlift.com), and click on the starter kits section, and select a starter kit. Then choose a name for your new website and click create. In a few seconds you'll be redirected to your website's URL. Your files will be placed in the <code>/Apps/Backlift</code> folder of your Dropbox. While you are online, any changes you make will automatically be synchronized to your Backlift website via Dropbox. 

If you need to visit your website later, visit [backlift.com](https://www.backlift.com), log in if you're not already, and click the 'my websites' link.

### Your website's URL

Backlift websites are assigned a unique URL based on the name you provide when creating it. The format of the URL is:

	<name>-<random_string>.backliftapp.com

This URL is not easy to guess, so you won't have unexpected visitors to your website while it's still in development. However it's publicly accessible, so you can share your work with others by sending them the URL. 

Backlift also supports custom URLs using your own domain. You must have already purchased the domain from a third party service like [Name Cheap](http://namecheap.com) or [DNSimple](http://dnsimple.com). You can find instructions on how to enable your purchased domain name by visiting the [custom urls](http://backlift.com/dashboard/urls) section of the dashboard. (Note you need an upgraded account in order to use your custom DNS. See the [Upgrade](http://backlift.com/dashboard/upgrade) section of the dashboard)

### Project layout

Files and folders within the Dropbox folder for your website can be layed out any way you like. Any files you add to your website folder will be accessible via the same path from your app's URL. For example if you create an "about.html" file in the /pages folder of your website in Dropbox, that file will be available by browsing to:

    <your-app>.backliftapp.com/pages/about.html


## The admin site

Each app gets a unique admin page that can be used for debugging and, in the future, managing security features like validation and authorization. You can view your app's admin page by clicking on the small gear icon under your app in the [apps](https://www.backlift.com/dashboard/apps) section of your Backlift dashboard.

As you develop your app, the admin page will change to reflect your app's collections and request history. This makes it a valuable debugging tool.

