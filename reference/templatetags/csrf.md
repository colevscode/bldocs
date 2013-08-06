{{$ meta }}
title: CSRF
tag: csrf
syntax: |
    {{$&nbsp;csrf&nbsp;}}<br>
{{$ endmeta }} 

{{$raw}}
The `csrf` tag writes out a hidden input field necessary for submitting forms to Backlift. This is a security measure used to prevent [Cross Site Request Forgery??](). You can add the csrf tag to your forms like this:

    <form action="/backlift/data/signups" method="POST">
      {{$ csrf }}
      <input type="text" name="email">
      <input type="submit">
    </form>

The csrf tag will generate HTML that looks something like this:

    <input type="hidden" name="_csrf" value="csrf_token_generated_by_backlift"/>

*The "csrf_token_generated_by_backlift" above will be replaced by a generated token.*

For more information about working with forms in backlift see the [form??](), [formsuccess??](), and [formerrors??]() tags and the [guide to working with forms??]().

{{$endraw}}





