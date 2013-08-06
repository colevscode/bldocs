{{$meta}}
type: guide
title: Data API
order: 5
{{$endmeta}}

{{$layout /index.html as content}}

{{$raw}}
In Backlift any app can store data on the server and retreive it later. This allows apps to implement complex functionality, such as collecting data from users via forms and visualizing that data in meaningful ways, or cordinating moves in a multiplayer game. You don't need to understand databases or SQL to store and retrieve data, just a basic understanding of javascript and jQuery. If you know how to fetch data jusing jQuery's ajax() methods, you can use the Backlift persistence API.

## Collections and models

Backlift uses just one data structure for persistence, the collection. A collection is just a group of things. Each thing in a collection is referred to as a model, and each model holds a set of related properties that describe the thing. A property has a name and a value. The models in a Backlift collection are not required to have the same properties.

For example, if you were building a library app, you might have a books collection. Each model in the collection would represent a single book, and might have a name, author, status and optional waiting property. Here's what such a collection would look like in Javascript Object Notation (JSON):

	{"books": [
		{"name": "The Corrections",
		 "author": "Jonathan Franzen",
		 "status": "checked-out",
		 "waiting": "Cole Krumbholz"},

		{"name": "Freedom",
		 "author": "Jonathan Franzen",
		 "status": "available"}
	]}

## The persistence API

Data is stored and retrieved using the persistence API. It's not a formal API beacause any URL that matches the pattern below is acceptable:

* GET /backlift/data/&lt;collection&gt;: will retrieve a list of the models in a collection.

* POST /backlift/data/&lt;collection&gt;: will create a new model and add it to a collection.

* GET /backlift/data/&lt;collection&gt;/&lt;item_id&gt;: will retrieve a specific model from a collection.

* PUT /backlift/data/&lt;collection&gt;/&lt;item_id&gt;: will update a model in a collection.

* DELETE /backlift/data/&lt;collection&gt;/&lt;item_id&gt;: will delete a model.

The data for PUT and POST requests should be sent in the request body, and can either be a JSON object or a url-encoded set of key-value pairs. 

Backlift stores the data as JSON documents, and does not need to know what properties a document will have in advance. In addition, collections do not need to be created before they are used. If a POST request is made for a collection the doesn't exist, Backlift will create it. If a GET request is made on a collection that doesn't exist, Backlift will return an empty set.

Later when you want to deploy your app in a production environment, you can setup validation via the config.yml config file. See the section on [data validation](validation.html) for documentation on how to "lock down" a collection.

## Persistence with Backbone.js

When using Backbone.js to communicate with the Backlift server, you just need to prefix your urls with "/backlift/data/". Backbone's default sync mechanism uses the URL scheme listed above. In fact, Backlift was built to allow backbone.js projects to work "out of the box". 

The following example shows how to set the url attribute of your collections and then use backbone's standard save and fetch methods.

	var MyBook = Backbone.Model.extend({});

	var MyBooks = Backbone.Collection.extend({
		model: MyBook,
		url: "/backlift/data/books"
	});

	var books = new MyBooks();
	books.fetch();   // will issue a GET /backlift/data/books

	var book = new MyBook({
		title: "The Corrections"
	});

	books.add(book);
	book.save();   // will issue a POST /backlift/data/books

## Persistence with HTML Forms

It's also possible use regular HTML forms to post data to Backlift API. This doesn't involve any Javascript, but might result to less optimal user experience. To send save data to Backlift with HTML forms, add these attributes to the form: `action="/backlift/data/<collection>"` and `method="POST"`.

As a security measure, you must also include `{{$ csrf}}` template tag somewhere inside the form element. This will add a hidden field to the form that helps the server to validate the origin of the data. If the field is not included, data will be rejected.

As an example, a form persisting data to Backlift might look something like this:

	<form method="POST" action="/backlift/data/mycollection">
		{{$ csrf }}
		
		<input type="text" name="email" />
		<input type="text" name="name" />
		<input type="submit" value="submit" />
	</form>

After the form is submitted, current page is reloaded. You can add template tags {{$ formerrors }} and {{$ formsuccess }} that render errors and success messages that you would normally check with Javascript. If there are no errors or success messages, those template tags don't output anything. If there is, they render something like:

	{{$ formsuccess }} -> <div class="backlift-form-success alert alert-success">
							<span>success</span>
						  </div>

	{{$ formerrors }} ->  <div class="backlift-form-errors alert alert-error">
							<span>Error 1</span>
							<span>Error 2</span>
						  </div>

The reference has more detail about the [csrf](/reference/templatetags#csrf), [formsuccess](/reference/templatetags#formsuccess) and [formerrors](/reference/templatetags#formerrors) tags.


## Special object attributes

Each time the backlift server persists a new object, a few attributes are applied automatically:

* **'id'**: If no id is set, the server will assign a unique uuid to each model and store it in the 'id' attribute. If there is an id, backlift will ensure that it is unique. 

* **'_owner'**: This attribute is automatically assigned to the currently logged-in user's id attribute, if there is a currently logged-in user. This value is read-only.

* **'_created'**: When a new object is created, this attribute is set with the current date and time in ISO standard format. This value is read-only.

* **'_modified'**: Each time an object is updated, this attribute is set with the current date and time in ISO standard format. This value is read-only.

* **'_id'**: Backlift mirrors the id attribute in an '_id' attribute. The '_id' attribute is used by backlift's mongodb database. In the future this attribute may be filtered out, so it's best not to rely on it.

### A note about dates

Backlift returns date/time values using the ISO 8601 format in UTC. These values can be parsed by Javascript's native Date object in all modern browsers. Here is an example of how to parse a date returned by backlift:

	// an example of ISO 8601 UTC time
    var obj = {_created: "2012-12-18T05:36:47.946Z"}; 

    var date = new Date(obj._created);

    console.log(date.toString());   // Mon Dec 17 2012 21:36:47 GMT-0800 (PST)
    console.log(date.toJSON()));    // 2012-12-18T05:36:47.946Z

The choice to go with ISO 8601 was somewhat arbitrary. There are several date time formats, and no particular format is prescribed in the JSON specification. We chose this format partly because it's what Date.toJSON() generates.

## Backlift collections and schemas

Collections are like tables in a database and are defined by a set of attributes, or fields. In backlift individual models in a collection don't need to contain all the attributes of their sibling models. However, if any of the models in a collection contain an attribute, it will be considered a part of that collection's schema.

By default there are no validation rules on any models in backlift. Anything can be stored in a collection, and new collections can be created on the fly. This is useful during development when the data model of an application is changing regularly. Later, when the application is ready for production, schema validation rules may be applied to "lock down" the kinds of data that backlift accepts.

## Defining schemas

Currently backlift validation rules must be created using the config.yml configuration file. Here is an example section of the config.yml file that sets up a validation rule:

    collections:
      tweets:
        message: {type: 'string', max: 140, required: yes}
        (other rules...)
      (other collections...)

Each sub group under 'collections' defines a new collection. When an AJAX request is sent to a /backlift/data/collection URL, backlift searches for the collection in this list. When found, the data attributes are matched against the rule names in order to select validation tests. If the data passes the tests for all attributes, the operation is permitted. 

For a discussion of the permissions attributes used during authorization, see the [authorization](authorization.html) section.

The syntax for defining a new rule is:

    <field name>: {[type: '<rule type>',] <parameter name>: <value> [...]}

If the rule 'type' is omitted, it will be assumed to be a 'string'.

## Validation errors

If one or more validation tests fail, backlift will return a 400 response along with a JSON object containing error data. The error data structure will look like this:

    {"form_errors": {
    	"message": ["exceeds 140 character limit"],
    	"otherfield": ["required"],
    	"": ["other problems"],
    }}

Each attribute of the 'form_errors' hash is a field name, and the value is a list of error messages. The empty string attribute indicates form-wide errors.

## Validation rule reference

The following is a list of validation rule types, and their type specific parameters.

*   '**string**' (min, max):
    A string with an optional minimum and maximum length. This is the default validation type for all rules.

*   '**regex**' (regex):
    A string that must match a regular expression. 

*   '**identifier**':
    A strictly alpha-numeric string at least 2 characters long and no more than 30 characters long. (It must match the regular expression '^[a-zA-Z0-9]{2,30}$') In addition identifiers are forced to lower-case when validated. Identifiers are used primarily for things like usernames and app IDs.

*   '**password**': 
    A string at least 8 characters long and no longer than 30 characters.

*   '**email**':
    Must be a valid email address.

*   '**list**':
    Must be a strig of the form '["item", "item", ...]'. Allows string representations of lists to be stored and retreived without requiring json deserialization.

*   '**auto:uuid**':
    A string that matches the regex pattern '^[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$'. A random uuid matching this pattern will be substituted for this attribute's value when the object is initially created.

*   '**auto:unique_uuid**':
    A string that matches the regex pattern '^[a-f0-9]{8}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{4}-[a-f0-9]{12}$'. A random uuid will be substituted for this attribute's value when the object is initially created. This value will be unique amongst values for this attribute on this collection.

*   '**auto:random_16_a0**':
    see below

*   '**auto:random_16_aA0**':
    see below

*   '**auto:unique_16_a0**':
    see below

*   '**auto:unique_16_aA0**':
    A string that matches the regex pattern '^[a-zA-Z0-9]{16}$' or '^[a-z0-9]{16}$'. A random string containing 16 alphanumeric characters (just lowercase, or upper and lowercase), will be substituted for this attribute's value when the object is initially created. If unique is specified the value will be unique amongst values for this attribute on this collection.

This list is incomplete at this time. We will update this list as new validation rules are created.

We realize that it is impossible to perform all server side data validation using a predetermined finite set of validation rules. Our goal is not to cover all possibilities. We are currently working to define a reasonable set that covers as much territory as possible. We are also evaluating alternatives for how to handle more custom validation needs.

## Common validation rule parameters

All validation rules accept the generic parameters 'default', 'required' and 'readonly'. 

* The 'default' parameter sets the value if no value is specified for an attribute.

* The 'required' parameter will ensure that a value is supplied for an attribute if set. (The value cannot be the empty string, nor can the attribute be absent entirely.)

* The 'readonly' parameter will cause the server to quietly reject any changes made to that attribute if set.

A common pattern is to set a value for the 'default' parameter, and set 'readonly' to 'yes'. This has the same effect of setting a fixed value for an attribute. All new objects created with these parameters will have the default value set for this attribute, which cannot be changed. This technique is effective for setting permissions on objects. See the [authorization](authorization.html) section for further discussion.

{{$endraw}}
