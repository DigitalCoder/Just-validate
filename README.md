# Just-validate
Lightweight form validation in Javascript Vanilla, without dependencies, with custom rules (including remote validation) and custom messages.

Demo: https://horprogs.github.io/Just-validate/

## How to use
### npm
```shell
npm install just-validate --save
```

### bower
```shell
bower install just-validate --save
```

Include the script of the Just-validate on your page
```html
<script src="./path/to/just-validate.min.js"></script>
...
</body>
```

## Create your form
```html
<form action="#" class="js-form form">
    <div class="row">
      <div class="form-group col-md-6">
        <label for="name">Enter your name</label>
        <input type="text" class="form__input form-control" placeholder="Enter your name" autocomplete="off" data-validate-field="name" name="name" id="name">
      </div>
      <div class="form-group col-md-6">
        <label for="email">Enter your email</label>
        <input type="email" class="form__input form-control" placeholder="Enter your email" autocomplete="off" data-validate-field="email" name="email" id="email">
      </div>
    </div>
    <div class="form-group">
      <label for="password">Enter your password</label>
      <input type="password" class="form__input form-control" placeholder="Enter your password" autocomplete="off" data-validate-field="password" name="password" id="password">
    </div>
    <div class="form-group">
      <label for="password">Enter your text</label>
      <textarea name="msg" cols="30" rows="10" class="form__textarea form-control" data-validate-field="text" id="text"></textarea>
    </div>
    <div class="form-group">
      <input type="checkbox" id="checkbox" class="form__checkbox" data-validate-field="checkbox" checked><label for="checkbox">I agree</label>
    </div>
    <div class="form-group">
      <label><input type="checkbox" class="form__checkbox" data-validate-field="checkbox2" checked>I agree</label>
    </div>

    <button class="form__btn btn btn-primary">SUBMIT</button>
  </form>
```

## Fields
`` data-validate-field `` : Name of field to which the rule will be applied

Plugin has default fields, which already have rules.

* **Field: email** 
    * required
    * email
    * remote
* **Field: name** 
    * required
    * minLength: 3
    * maxLength: 15
* **Field: text** 
    * required
    * minLength: 5
    * maxLength: 300
* **Field: password** 
    * required
    * password (at least 1 digit and 1 letter)
    * minLength: 4
    * maxLength: 8
* **Field: zip** 
    * required
    * zip (4-5 digits)
* **Field: phone** 
    * phone (format 111-222-3333)
    
You can create your own fields, e.g. ``data-validate-field="myField"``.

## Rules
* required -  Required field, not empty
* email - Check a valid email address
* minLength - Limit the minimum value
* maxLength - Limit the maximum value
* password - At least 1 letter and 1 digit
* zip - 4-5 digits
* phone - Format 111-222-3333
* remote
 
More about ``remote`` rule: <br>
Rule check remote server api for correct answer. For example:
```js
remote: {
    url: '/check-correct',
    successAnswer: 'OK',
    sendParam: 'email',
    method: 'GET'
}
```
* url - remote server api url
* successAnswer - expected response from server, if value is correct
* sendParam - parameter to be sent to server
* method - GET or POST

## Settings
```js
new window.JustValidate(element, options);
```

* element - string, selector of DOM element
* options - object
 
Initiate plugin:

First argument - selector of DOM element.
```js
new window.JustValidate('.js-form');
```

In this case default rules and messages will be applied.

Also, you can customize validation:
```js
new JustValidate('.js-form', {
    rules: {
      checkbox: {
        required: true
      },
      myField: {
        required: true
      },
      email: {
        required: false,
        email: true
      }
    },
    messages: {
      name: {
        minLength: 'My custom message about only minLength rule'
      },
      email: 'My custom message about error (one error message for all rules)' 
    },

    submitHandler: function (form, values, ajax) {

      ajax({
        url: 'https://just-validate-api.herokuapp.com/submit',
        method: 'POST',
        data: values,
        async: true,
        callback: function(response)  {
          console.log(response)
        }
      });
    },
  });
```

You can override custom message for once rule or for all at once rules.

### Styling

You can customize style color of error, using property ``colorWrong``, for example: <br>
```js
new window.JustValidate('.js-form', {
    colorWrong: 'red'
});
```

Error fields and messages have classes: ``js-validate-error-label`` and  ``js-validate-error-field``

### Submit form
You can override standard submit form, using method ``submitHandler``. It has 3 arguments:
* form - DOM link to form
* values - object of fields values
* ajax - function of XMLHttpRequest

## Current version stable
**V1.0.0**

## Contributing
- Check the open issues or open a new issue to start a discussion around your feature idea or the bug you found.
- Fork repository, make changes, add your name and link in the authors session readme.md
- Send a pull request

**Thank you**


