{{$ meta }}
title: Delete a model
syntax: |
    DELETE /backlift/data/&lt;collection&gt;/&lt;model_id&gt;<br>
api: data
tag: data_del_model
order: 5
{{$ endmeta }}

Removes a model from it's collection. See the section on [persistence](persistence.html) for more detail.

Example:

    $.ajax({
        type: "DELETE",
        url: "/backlift/data/todos/4928bcd1-56f7-40e4-ba78-212bae096b5c", 
        success: function(result) { 
            console.log("Deleted!");
        } 
    });

Errors:

* **403 Not Authorized**: This error occurs if the currently signed-in user doesn't have permission to perform this operation. This can occur if the model to be updated is owned by another user, and the _public_permissions property excludes delete permission. See [permissions and access control](authorization.html#permissions-and-access-control) or more information.


