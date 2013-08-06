{{$ meta }}
title: Nav
tag: nav
syntax: |
    {{$&nbsp;nav&nbsp;&lt;file&nbsp;pattern&gt; [&nbsp;&lt;list&nbsp;class&gt;&nbsp;] [&nbsp;&lt;item&nbsp;class&gt;&nbsp;]&nbsp;}}<br>
{{$ endmeta }} 

{{$ raw }}
The `nav` tag creates a list of links to all the files that match a `file pattern`. For example, if you placed this tag in your `index.html` file:

    {{$ nav /posts/*.html }}


... and you had these files in your posts folder:

    posts/
      firstpost.html
      secondpost.html


... it would generate the following HTML:

    <ul>
      <li><a href="/posts/firstpost.html">firstpost.html</a></li>
      <li><a href="/posts/secondpost.html">secondpost.html</a></li>
    </ul>


### Controlling the link text

When generating the links, for each file the `nav` tag first looks to see if there is a [meta??]() tag with a `title` property. If so, it will place the title in the link text. If not, then the filename will be used instead.

So for example in order to change the link text for a blog post, add a `meta` tag at the top like this:

in /posts/mypost.html:

    {{$ meta }}
    title: My first post
    {{$ endmeta }}

    Post body...


### Controlling the navigation styles

The `nav` tag has two optional arguments for specifying CSS classes: one for the list class and one for the list items class. Here is an example of specifying both:

    {{$ nav /posts/*.html 'nav' 'nav-item' }}

... which generates this:

    <ul class="nav">
      <li class="nav-item"><a href="/posts/firstpost.html">firstpost.html</a></li>
      <li class="nav-item"><a href="/posts/secondpost.html">secondpost.html</a></li>
    </ul>



### The nav tag is just a shortcut

You can generate exactly the same HTML output by using an [each??]() tag and the [files API??](). It's just a bit more verbose. Here's what it would look like:

    <ul>
      {{$ each /backlift/files/posts/*.html as page }}
        <li>
          <a href="{$ page.path }">
            {$ page.title }
            {{$ if not {$ page.title} }}
              {$ page.filename }
            {{$ endif }}
          </a>
        </li>
      {{$ endeach }}
    </ul>

{{$ endraw }}