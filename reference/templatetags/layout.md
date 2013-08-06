{{$ meta }}
title: Layout
tag: layout
syntax: |
    {{$&nbsp;layout&nbsp;&lt;path&gt;&nbsp;as &lt;variable&nbsp;name&gt;&nbsp;}}<br>
    &nbsp;&nbsp;&lt;content to layout&gt;<br>
    [ {{$&nbsp;endlayout&nbsp;}} ]<br>
{{$ endmeta }}

The `layout` tag lets you select a separate file to use as the layout for your content. You must provide a `path` to that file, and a `variable name` that will will be used to inject the content into the layout file. If no `endlayout` tag is provided, the rest of the file will be used as the content to layout. 

For example, if you place a layout tag in your index.html file like this:

/index.html:

    {{$raw}}{{$ layout /layouts/base.html as content }}
    Hello world!{{$endraw}}

...then you should have a file called `base.html` in the layouts folder of your project that looks similar to this:

/layouts/base.html:
  
    <h1>{{$raw}}{$ content }{{$endraw}}</h1>

When you visit the `/index.html` file you'll see the following result in your browser:

result:

    <h1>Hello world!</h1>

### Optional block syntax

You can optionally provide an end tag for the layout which would allow you to layout just a portion of your file. For example if you had the following index file:

/index.html:

    {{$raw}}{{$ layout /layouts/base.html as content }}
    Hello world!
    {{$ endlayout }}
    <hr>
    Some footer data{{$endraw}}   

Using the same `/layouts/base.html` file you'd see the following result when you visited `index.html` in your browser:

result:

    <h1>Hello world!</h1>
    <hr>
    Some footer data


### Absolute paths only

Currently you should use absolute paths when providing the `path` to the layout file. For example, if your layout file is called `base.html` and it's in the `layouts` folder at the root of your project, write `/layouts/base.html` rather than `../layouts/base.html` or some other relative path.

