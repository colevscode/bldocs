{{$ meta }}
title: Each
tag: each
syntax: |
    {{$&nbsp;each&nbsp;&lt;list&gt;&nbsp;as &lt;variable&nbsp;name&gt;&nbsp;}}<br>
    &nbsp;&nbsp;&lt;stuff to write for each item in the list&gt;<br>
    {{$&nbsp;endeach&nbsp;}}<br>
{{$ endmeta }} 

The `each` tag lets you loop over a `list`, writing out some stuff for each item. Here's an example:

    {{$raw}}{{$ each /backlift/files/*.html as file }}
      I found {$ file.filename }!
    {{$ endeach }}{{$endraw}}

The `list` can be anything that generates a list. You can use a variable that contains a list, or the URL for an API that returns a list, or a JSON string containing a list. The above example uses the [Backlift files API??]() to get a list of .html files. 

For example, here's how you can use each with a variable defined in a [meta??]() block:
  
    {{$raw}}{{$ meta }}
    cat_names: ['Bob', 'Frank', 'Suzie']
    {{$ endmeta }}

    {{$ each {$ meta.cat_names } as name }}
      I know a cat named {$ name }.<br>
    {{$ endeach }}{{$endraw}}


