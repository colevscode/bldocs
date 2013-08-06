{{$ meta }}
title: Retrieve a model
syntax: |
    GET /backlift/data/&lt;collection&gt;/&lt;model_id&gt;<br>
api: data
tag: data_get_model
order: 3
{{$ endmeta }}

Returns a models. See the section on [persistence](persistence.html) for more detail.

Example usage:

    $.ajax({
        type: "GET",
        url: "/backlift/data/todos/8c064fd0-616f-4e18-91e5-959b5475516f",
        success: function(result) { 
            console.log(result); 
        }
    });

    // result: 
    // {
    //    "id":"8c064fd0-616f-4e18-91e5-959b5475516f",
    //    "title":"Do something",
    //    "order":1
    //    ...
    // }

