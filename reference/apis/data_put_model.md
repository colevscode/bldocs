{{$ meta }}
title: Update a model
syntax: |
    PUT /backlift/data/&lt;collection&gt;/&lt;model_id&gt;<br>
api: data
tag: data_put_model
order: 4
{{$ endmeta }}

Updates a model. See the section on [persistence](persistence.html) for more detail.

Parameters:

* **id**: the id of the new object. If no id is supplied, the object will be assigned a random id. 
* ... any additional parameters passed will become properties of the new model

Returns: The updated model.

Example:

    $.ajax({
        type: "PUT",
        url: "/backlift/data/todos/4928bcd1-56f7-40e4-ba78-212bae096b5c", 
        data: {
            title: "Write MORE Code",
            order: 1
        },
        success: function(result) { 
            console.log(result);
        } 
    });

    // result: 
    // {
    //    "id":"4928bcd1-56f7-40e4-ba78-212bae096b5c",
    //    "title":"Write MORE Code",
    //    "order":"1",
    //    ...
    // }

Errors:

* **400 Bad Request**: If the data submitted doesn't pass one of the validation tests, the response will be a 400 error. The result will be a JSON object with a 'form_errors' property that contains a dictionary where the keys are names of the property for which a validation error was raised, and the values are lists of the validation errors for each property. For example:

      {"form_errors":
          "title": ["must be 25 characters or less"]
      } 

* **403 Not Authorized**: This error occurs if the currently signed-in user doesn't have permission to perform this operation. This can occur if the model to be updated is owned by another user, and the _public_permissions property excludes write permission. See [permissions and access control](authorization.html#permissions-and-access-control) or more information.
