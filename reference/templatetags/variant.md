{{$ meta }}
title: Variant
tag: variant
syntax: |
    {{$&nbsp;variant&nbsp;&lt;variant name&gt;&nbsp;}}<br>
    &nbsp;&nbsp;&lt;stuff to write for this variant&gt;<br>
    {{$&nbsp;endvariant&nbsp;}}<br>
{{$ endmeta }} 

{{$raw}}
The `variant` tag lets you create HTML that will only be displayed to a portion of your visitors. This tag is useful for split testing, also known as "A/B" testing, where you display variations in your content and track which variant results in a higher conversion rate. Here's an example:

    {{$ variant a }}
      <h1>Our product gets the job done!</h1>
    {{$ endvariant }}

    {{$ variant b }}
      <h1>Our product is magical!</h1>
    {{$ endvariant }}

The variants must be configured before using the variant tag. You can use the `config.yml` file to set up variant groups and specify the probability for each group. Read more about this, and how to track conversions, in our [help guide on split testing??]().

{{$endraw}}





