{{$ meta }}
title: Formerrors
tag: formerrors
syntax: |
    {{$&nbsp;formerrors&nbsp;}}<br>
{{$ endmeta }} 

{{$raw}}
The `formerrors` tag writes out any errors that were generated during the last form submission. For example, formerrors my generate some HTML like this:

    <div class="backlift-form-errors alert alert-error">
    	<span>name required, email invalid<span>
    </div> 

For more information about working with forms in backlift see the [form??](), [formsuccess??](), and [messages??]() tags and the [guide to working with forms??]().

{{$endraw}}





