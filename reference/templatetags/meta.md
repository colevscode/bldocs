{{$ meta }}
title: Meta
tag: meta
syntax: |
    {{$&nbsp;meta&nbsp;}}<br>
    &lt;properties&gt;<br>
    {{$&nbsp;endmeta&nbsp;}}<br>
{{$ endmeta }} 

The `meta` tag allows you to add metadata to an HTML file. The content of the `meta` block should be a list of properties. Generally a meta tag should look like this:

    {{$raw}}{{$ meta }}
    property1: value1
    property2: value2
    {{$ endmeta }}{{$endraw}}

For most common use cases, if you follow the example above you should be fine. If you want to do more complicated things, like use lists or hashes as property values, you can do so by following the [yaml]() syntax.

### Accessing meta properties

Meta properties can be accessed within an HTML file by using a variable tag. For example, if your `meta` block contains a `title` property, you can access the property later in that file with the {{$raw}}`{$ meta.title }`{{$endraw}} variable.

Meta properties are also accessible using the [Backlift files API](). A common pattern is to use an `each` tag to get a list of files using the files API. 

### Default meta properties

Backlift adds a few meta properties to all files, including the `created`, `modified`, `filename`, and `url` properties, to name a few. You can override these defaults by creating a property with the same name in the `meta` tag. 

### Further reading

See the section on metadata in the [Backlift template guide]() for further discussion of how to access properties you've defined in a meta block, and a full list of the default meta properties defined by Backlift.