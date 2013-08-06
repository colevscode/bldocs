{{$ meta }}
title: Login
syntax: |
    POST /backlift/auth/login<br>
api: auth
tag: auth_login
{{$ endmeta }}

Signs in a user. See the section on [authorization](authorization.html) for more detail.

Parameters: (see [validation reference](validation.html#validation-rule-reference))

<pre><code class="javascript">username: {type: 'identifier', required_if_empty: 'email'}
email: {type: 'email', required_if_empty: 'username'}
password: {type: 'password', required: yes}
</code></pre>

Example using AJAX:

    $.ajax({
        type: "POST",
        url: "/backlift/auth/login", 
        data: {
            username: "username",
            password: "password"
        },
        success: function(result) { 
            console.log(result);
        } 
    });

    // result: (same as register)
    // {
    //    "id":"JPwLMxPHmJDkGpwk"
    //    "email": "user@example.com",
    //    "profile": { 
    //        "username": "username",
    //        "_owner": "JPwLMxPHmJDkGpwk",
    //        ...
    //    },
    //    ...
    // }

Example using a form:

    <form method="POST" action="/backlift/auth/login">
        Username: <input type="text" name="username">
        Password: <input type="password" name="password">
        <input type="hidden" name="_next" value="/home">
        <input type="submit">
    </form>
