{{$ meta }}
title: With
tag: with
syntax: |
    {{$&nbsp;with&nbsp;&lt;object&gt;&nbsp;as &lt;variable&nbsp;name&gt;&nbsp;}}<br>
    &nbsp;&nbsp;&lt;stuff to write using the object&gt;<br>
    {{$&nbsp;endwith&nbsp;}}<br>
{{$ endmeta }} 

{{$raw}}
The `with` tag lets you write out some HTML using the data contained in an `object`. Here's an example:

    {{$ with /backlift/data/addresses/home as address }}
      I live at {$ address.street } in {$ address.city }.
    {{$ endwith }}

The `object` can be anything that represents an object, such as a variable that contains an object, or the URL for an API that returns an object, or a JSON string containing an object. The above example uses the [Backlift data API??]() to get an address. 

Alternatively, here's how you can use with send some data to a seperately included file:
  
    {{$ with '["Bob", "Suzie", "Garth"]' as cat_names }}
      {{$ import /catlist.html }}
    {{$ endwith }}

... then in /catlist.html you can write out the cat names with an [each??]() tag:

    {{$ each {$ cat_names } as name }}
      I know a cat named {$ name }.<br>
    {{$ endeach }}

{{$endraw}}





