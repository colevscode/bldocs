{{$ meta }}
title: Displaying a list of recent blog posts
tags: [meta, nav, layout]
difficulty: 3
{{$ endmeta }}

{{$ layout /partials/recipe.html as content }}

{{$raw}}
in /posts/blogpost.html:

    {{$ meta }}
    title: Chickens are not Turkeys
    created: 2012-09-23
    author: Cole Krumbholz
    {{$ endmeta }}

    {{$ layout /layouts/base.html as content }}

    <h1> {$ meta.title } </h1>

    What a week. Today I learned an important distinction between two similar varieties of fowl...


in /index.html:

    {{$ layout /layouts/base.html as content }}

    <h1>Welcome to my blog!</h1>
    This is a blog about the things I learn every day.
    <h3>Recent posts:</h3>
    {{$ nav /posts/*.html | sort {$ page.created } | reversed }}


in /layouts/base.html:

    <html>
      <head>
        <title>My blog</title>
      </head>
      <body>
        {$ content }
      </body>
    </html>
    
        
Here we first create a blog post and place the `meta` tag at the top where we add some properties to the post, like a post title, created date and author. We layout the blog post using the `index.html` file as a template. We then fill out the rest of the post like a normal HTML page. (As a convenience we use the `{$ meta.title }` variable in the header tag so that if we change the title later, we only have to change it in one place.)

Then in the `index.html` we create a list of posts by using the `nav` tag. The `nav` tag gets a list of files that match the pattern `/posts/*.html`. It then uses the `title` meta property along with the built-in `url` property for each file to construct a list of links. We can also refer to those meta properties, like the page's `created` date to apply filters, like the `sort` filter.

Finally in the `/layouts/base.html` file we provide a template that for all the pages on our site.

{{$endraw}}
