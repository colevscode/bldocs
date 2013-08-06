{{$ meta }}
title: Using the same layout for several pages
tags: [layout]
difficulty: 1
{{$ endmeta }}

{{$ layout /partials/recipe.html as content }}

{{$raw}}
in /index.html:

    {{$ layout /layouts/base.html as content }}

    <h1>Welcome to my cat website</h1>

    Here you will find photos of cats!

in /about.html:

    {{$ layout /layouts/base.html as content }}

    <h1>About this website</h1>

    I'm Rick and I like to photograph cats. I live in Massachusetts. 

in /layouts/base.html:

    <html>
      <head>
        <title>Rick's photos of cats!</title>
      </head>
      <body>
        {$ content }
      </body>
    </html>

{{$endraw}}

In this recipe, we've created a layout file at `/layouts/base.html` with all the boilerplate HTML that must go in all the pages of our website. Then when we create new pages, like the `index.html` or `about.html` pages, we can just specify the layout file and the name of the variable that will be used to inject the file content into the layout.