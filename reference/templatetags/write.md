{{$ meta }}
title: Write
tag: write
syntax: |
    {{$&nbsp;write&nbsp;&lt;thing&gt;&nbsp;}}<br>
{{$ endmeta }} 

{{$raw}}
The `write` tag serves one purpose: to allow you to use filters when writing the contents of a variable into your html file. Here's an example of its use:

    {{$ write {$ meta.created } | dateformat "%B %d, %Y" }}

The above line writes out the current file's created date using a month, date, year format.

{{$endraw}}
