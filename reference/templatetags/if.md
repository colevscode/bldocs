{{$ meta }}
title: If
tag: if
syntax: |
    {{$&nbsp;if&nbsp;[&nbsp;not&nbsp;]&nbsp;&lt;thing&gt; [&nbsp;&lt;op&gt; &lt;thing2&gt;&nbsp;]&nbsp;}}<br>
    &nbsp;&nbsp;&lt;stuff to write if the test passes&gt;<br>
    {{$&nbsp;endif&nbsp;}}<br>
{{$ endmeta }} 

{{$raw}}
The `if` tag lets you conditionally write out some HTML if a test passes. If only one `thing` is provided, then the test will pass if that thing is not empty. If two things are provided, then the test is determined by the operator `op`. (one of: is, in, lt or gt) The `not` keyword will invert the criteria, such that the content will only be written if the test fails.

Here's a commonly used example:

    {{$ if not {$ meta.title} }}
      Default title.
    {{$ endwith }}
    {$ meta.title }

Above we first check to see if the title is empty, if so we write out a default title. Then we write out the title. The result is that if a title exists, it will be written out, otherwise we'll see the default.

The `thing` and `thing2` arguments can be any string, variable or object. For example, we can use the `if` tag to check the type of a file, based on some data in the meta tag:

    {{$ meta }}
    type: reference
    {{$ endmeta }}

    {{$ if {$ meta.type } is reference }} 
      This is a reference file
    {{$ endif }}

### operators

Here are the various operators you can use:

- `is`: checks for equality
- `in`: checks that the first thing is a member of a list. This means the second thing must be a list! For example: `{{$ if {$ item } in '["box", "bag"]' }}`
- `gt`: checks that the first thing is greater than the second thing
- `lt`: checks that the first thing is less than the second thing

You can test to see if a thing is greater than or equal to the second thing by inverting the operation and using `not`. For example `{{$ if not {$ var } lt 4 }}` will test if `var` is greater than or equal to 4.


{{$endraw}}





