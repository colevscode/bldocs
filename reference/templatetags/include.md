{{$ meta }}
title: Include
tag: include
syntax: |
    {{$&nbsp;include&nbsp;&lt;path&gt;&nbsp;}}<br>
{{$ endmeta }}

{{$raw}}
The `include` tag lets you embed the contents of a separate file into the current file. You must provide a `path` to that file. The content will be included as-is, so any variables in that file will be evaluated using the context of the file where the include tag is located. For example, if you place an include tag in your index.html file like this:

/index.html:

    {{$ meta }}
    title: "Hello World!"
    {{$ endmeta }}

    <html>
      {{$ include /partials/header.html }}  <!-- include tag -->
      <body>
        <h1>{$ meta.title }<h1>
      </body>
    </html>

...then you could have a file called `header.html` in the partials folder of your project that looks similar to this:

/partials/header.html:
  
    <head>
      <title>{$ meta.title }</title>
    </head>


### Absolute paths only

Currently you should use absolute paths when providing the `path` to the included file. For example, if your included file is called `header.html` and it's in the `partials` folder at the root of your project, write `/partials/header.html` rather than `../partials/header.html` or some other relative path.

{{$endraw}}  
