{{$ meta }}
title: Create a new model
syntax: |
    POST /backlift/data//&lt;collection&gt;<br>
api: data
tag: data_post_col
order: 2
{{$ endmeta }}

Creates a new model for a collection. See the section on [persistence](persistence.html) for more detail.

Parameters:

* **id**: the id of the new object. If no id is supplied, the object will be assigned a random id. 
* ... any additional parameters passed will become properties of the new model

Returns: A copy of the new model that will include a new id property if one has been assigned.

Example:

    $.ajax({
        type: "POST",
        url: "/backlift/data/todos", 
        data: {
            title: "Write Code",
            order: 3
        },
        success: function(result) { 
            console.log(result);
        } 
    });

    // result: 
    // {
    //    "id":"4928bcd1-56f7-40e4-ba78-212bae096b5c",
    //    "title":"Write Code",
    //    "order":"3",
    //    ...
    // }

Errors:

* **400 Bad Request**: If the data submitted doesn't pass one of the validation tests, the response will be a 400 error. The result will be a JSON object with a 'form_errors' property that contains a dictionary where the keys are names of the property for which a validation error was raised, and the values are lists of the validation errors for each property. For example:

      {"form_errors":
          "title": ["must be 25 characters or less"]
      } 

* **403 Not Authorized**: This error occurs if the currently signed-in user doesn't have permission to perform this operation. This can occur if the model has an id that matches an existing model in the collection owned by another user. It can also occur if the collection's schema has an _owner_permissions attribute with a default that lacks create permissions. See [permissions and access control](authorization.html#permissions-and-access-control) or more information.
