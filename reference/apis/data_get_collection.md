{{$ meta }}
title: Retrieve all models
syntax: |
    GET /backlift/data/&lt;collection&gt;<br>
api: data
tag: data_get_col
order: 1
{{$ endmeta }}

Returns a list of models in a collection. See the section on [persistence](persistence.html) for more detail.

Example usage:

    $.ajax({
        type: "GET",
        url: "/backlift/data/todos",
        success: function(result) { 
            console.log(result); 
        }
    });

    // result: 
    // [{
    //    "id":"8c064fd0-616f-4e18-91e5-959b5475516f",
    //    "title":"Do something",
    //    "order":1
    //    ...
    // },{
    //    "id":"4928bcd1-56f7-40e4-ba78-212bae096b5c",
    //    "title":"Something else",
    //    "order":2
    //    ...
    // }]

