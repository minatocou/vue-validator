# vue-validator

[![CircleCI Status](https://circleci.com/gh/vuejs/vue-validator/tree/dev.svg?style=shield&circle-token=36fad1862fbb44da91a28217df8fba769d6d1ce7)](https://circleci.com/gh/vuejs/vue-validator/tree/dev)
[![Coverage Status](https://coveralls.io/repos/vuejs/vue-validator/badge.svg?branch=dev&service=github)](https://coveralls.io/github/vuejs/vue-validator?branch=dev)
[![Sauce Test Status](https://saucelabs.com/buildstatus/vuejs-validator)](https://saucelabs.com/u/vuejs-validator)
[![Commitizen friendly](https://img.shields.io/badge/commitizen-friendly-brightgreen.svg)](http://commitizen.github.io/cz-cli/)


Validator component for Vue.js


# Requirements
- Vue.js `1.0.14`+

## NOTE
vue-validator is still in its alpha verison. There may be some breaking changes. 
If you have some feedback, you're welcome in [Vue.js Discussion](http://forum.vuejs.org) :smiley_cat:


# Installation

## npm

### stable version
```shell
$ npm install vue-validator
```

### development version
```shell
git clone https://github.com/vuejs/vue-validator.git node_modules/vue-validator
cd node_modules/vue-validator
npm install
npm run build
```

When used in CommonJS, you must explicitly install the router via `Vue.use()`:
```javascript
var Vue = require('vue')
var VueValidator = require('vue-validator')

Vue.use(VueValidator)
```

You don't need to do this when using the standalone build, as it installs itself automatically.

## CDN
jsdelivr
```html
<script src="https://cdn.jsdelivr.net/vue.validator/2.0.0-alpha.16/vue-validator.min.js"></script>
```


# Usage

```javascript
new Vue({
  el: '#app'
})
```

We can use the `validator` element directive and `v-validate` directive, as follows:

```html
<div id="app">
  <validator name="validation1">
    <form novalidate>
      username: <input type="text" v-validate:username="['required']"><br />
      comment: <input type="text" v-validate:comment="{ maxlength: 256 }"><br />
      <div>
        <span v-show="$validation1.username.required">Required your name.</span>
        <span v-show="$validation1.comment.maxlength">Your comment is too long.</span>
      </div>
      <input type="submit" value="send" v-if="$validation1.valid">
    </form>
  </validator>
</div>
```

The validation results are scoped to the validator element. In above case, the validation results keep to `$validation1` scope (prefixed with `$`), specified by the `name` attribute of the `validator` element.


# Validation result structure

Validation results can be accessed in this structure:

```
  $validation.valid
             .invalid
             .touched
             .untouched
             .dirty
             .pristine
             .modified
             .messages.field1.validator1
                             ...
                             .validatorX
                      .field2.validator1
                             ...
                             .validatorX
             .field1.validator1
                    ...
                    .validatorX
                    .valid
                    .invalid
                    .touched
                    .untouched
                    .dirty
                    .pristine
                    .modified
                    .messages.validator1
                             ...
                             .validatorX
             ...
             .fieldX.validator1
                    ...
                    .validatorX
                    .valid
                    .invalid
                    .touched
                    .untouched
                    .dirty
                    .pristine
                    .modified
                    .messages.validator1
                             ...
                             .validatorX
```

The various top-level properties are in the validation scope, and each field validation result in its own respective scopes.

## Field validation properties
- `valid`: whether field is valid; if it's valid, then return `true`, else return `false`.
- `invalid`: reverse of `valid`.
- `touched`: whether field is touched. if field was focused, return `true`, else return `false`.
- `untouched`: reverse of `touched`.
- `modified`: whether field value is modified; if field value was changed from **initial** value, return `true`, else return `false`.
- `dirty`: whether field value was changed at least **once**; if so, return `true`, else return `false`.
- `pristine`: reverse of `dirty`.
- `messages`: if invalid field exist, return error message wrapped with object, else `undefined`.

## Top level validation properties
- `valid`: whether **all** fields is valid. if so, then return `true`, else return `false`.
- `invalid`: if invalid field exist even **one** in validate fields, return `true`, else `false`.
- `touched`: whether **all** fields is touched, if so, return `true`, else `false`.
- `untouched`: if untouched field exist even **one** in validate fields, return `true`, else `false`.
- `modified`: if modified field exist even **one** in validate fields, return `true`, else `false`.
- `dirty`: if dirty field exist even **one** in validate fields, return `true`, else `false`.
- `pristine`: whether **all** fields is pristine, if so, return `true`, else `false`.
- `messages`: if invalid even one exist, return all field error message wrapped with object, else `undefined`.


# Validator syntax
`v-validate` directive syntax the below:

```
    v-validate[:field]="array literal | object literal | binding"
```

## Field
In vue-validator version 2.0-alpha or earlier, validation relied on `v-model`. In 2.0-alpha and later, use the `v-validate` directive instead.

~v1.4.4:
```html
<form novalidate>
  <input type="text" v-model="comment" v-validate="minLength: 16, maxLength: 128">
  <div>
    <span v-show="validation.comment.minLength">Your comment is too short.</span>
    <span v-show="validation.comment.maxLength">Your comment is too long.</span>
  </div>
  <input type="submit" value="send" v-if="valid">
</form>
```

v2.0-alpha later:
```html
<validator name="validation">
  <form novalidate>
    <input type="text" v-validate:comment="{ minlength: 16, maxlength: 128 }">
    <div>
      <span v-show="$validation.comment.minlength">Your comment is too short.</span>
      <span v-show="$validation.comment.maxlength">Your comment is too long.</span>
    </div>
    <input type="submit" value="send" v-if="valid">
  </form>
</validator>
```

### Caml-case property
As well as [Vue.js](http://vuejs.org/guide/components.html#camelCase_vs-_kebab-case), you can use the kebab-case for `v-validate` models:

```html
<validator name="validation">
  <form novalidate>
    <input type="text" v-validate:user-name="{ minlength: 16 }">
    <div>
      <span v-if="$validation.userName.minlength">Your user name is too short.</span>
    </div>
  </form>
</validator>
```

### Attribute
You can specify the field name to `field` params attribute. This is useful when you need to define the validatable form elements dynamically:

> NOTE: the field part of `v-validate` is optional, when you use `field` params attribute

```html
<div id="app">
  <validator name="validation">
    <form novalidate>
      <p class="validate-field" v-for="field in fields">
      <label :for="field.id">{{field.label}}</label>
      <input type="text" :id="field.id" :placeholder="field.placeholder" field="{{field.name}}" v-validate="field.validate">
      </p>
      <pre>{{ $validation | json }}</pre>
    </form>
  </validator>
</div>
```

```javascript
new Vue({
  el: '#app',
  data: {
    fields: [{
      id: 'username',
      label: 'username',
      name: 'username',
      placeholder: 'input your username',
      validate: { required: true, maxlength: 16 }
    }, {
      id: 'message',
      label: 'message',
      name: 'message',
      placeholder: 'input your message',
      validate: { required: true, minlength: 8 }
    }]
  }
})
```


## Literal

### Array
The below example uses an array literal:

```html
<validator name="validation">
  <form novalidate>
    Zip: <input type="text" v-validate:zip="['required']"><br />
    <div>
      <span v-if="$validation.zip.required">Zip code is required.</span>
    </div>
  </form>
</validator>
```

Since `requred` doesn't need to specify any additional rules, this syntax is preferred.


### Object
The below example uses an object literal:

```html
<validator name="validation">
  <form novalidate>
    ID: <input type="text" v-validate:id="{ required: true, minlength: 3, maxlength: 16 }"><br />
    <div>
      <span v-if="$validation.id.required">ID is requred.</span>
      <span v-if="$validation.id.minlength">Your ID is too short.</span>
      <span v-if="$validation.id.maxlength">Your ID is too long.</span>
    </div>
  </form>
</validator>
```

Object literals allow you to provide rule values. For `requred`, as it doesn't need a rule value, you can specily a **dummy rule** instead, as shown.

Alternatively, you can specify a strict object as follows:

```html
<validator name="validation">
  <form novalidate>
    ID: <input type="text" v-validate:id="{ minlength: { rule: 3 }, maxlength: { rule: 16 } }"><br />
    <div>
      <span v-if="$validation.id.minlength">Your ID is too short.</span>
      <span v-if="$validation.id.maxlength">Your ID is too long.</span>
    </div>
  </form>
```

## Binding
The below example uses live binding:

```javascript
new Vue({
  el: '#app',
  data: {
    rules: {
      minlength: 3,
      maxlength: 16
    }
  }
})
```
```html
<div id="app">
  <validator name="validation">
    <form novalidate>
      ID: <input type="text" v-validate:id="rules"><br />
      <div>
        <span v-if="$validation.id.minlength">Your ID is too short.</span>
        <span v-if="$validation.id.maxlength">Your ID is too long.</span>
      </div>
    </form>
  </validator>
</div>
```

You can also use computed properties or methods to retrieve rule sets, instead of a set data property.


# v-model 
You can validate the field that updated with v-model:

```html
<div id="app">
  <validator name="validation1">
    <form novalidate>
      message: <input type="text" v-model="msg" v-validate:message="{ required: true, minlength: 8 }"><br />
      <div>
        <p v-if="$validation1.message.required">Required your message.</p>
        <p v-if="$validation1.message.minlength">Too short message.</p>
      </div>
    </form>
  </validator>
</div>
```

```javascript
var vm = new Vue({
  el: '#app',
  data: {
    msg: ''
  }
})

setTimeout(function () {
  vm.msg = 'hello world!!'
}, 2000)
```


# Checkbox

Checkbox validation supports lengths:

```html
<div id="app">
  <validator name="validation1">
    <form novalidate>
      <h1>Survey</h1>
      <fieldset>
        <legend>Which do you like fruit ?</legend>
        <input id="apple" type="checkbox" value="apple" v-validate:fruits="{
          required: { rule: true, message: requiredErrorMsg },
          minlength: { rule: 1, message: minlengthErrorMsg },
          maxlength: { rule: 2, message: maxlengthErrorMsg }
        }">
        <label for="apple">Apple</label>
        <input id="orange" type="checkbox" value="orange" v-validate:fruits>
        <label for="orange">Orage</label>
        <input id="grape" type="checkbox" value="grage" v-validate:fruits>
        <label for="grape">Grape</label>
        <input id="banana" type="checkbox" value="banana" v-validate:fruits>
        <label for="banana">Banana</label>
        <ul class="errors">
          <li v-for="msg in $validation1.fruits.messages">
            <p>{{msg}}</p>
          </li>
        </ul>
      </fieldset>
    </form>
  </validator>
</div>
```

```javascript
new Vue({
  el: '#app',
  computed: {
    requiredErrorMsg: function () {
      return 'Required fruit !!'
    },
    minlengthErrorMsg: function () {
      return 'Please chose at least 1 fruit !!'
    },
    maxlengthErrorMsg: function () {
      return 'Please chose at most 2 fruits !!'
    }
  }
})
```


# Radio Button

```html
<div id="app">
  <validator name="validation1">
    <form novalidate>
      <h1>Survey</h1>
      <fieldset>
        <legend>Which do you like fruit ?</legend>
        <input id="apple" type="radio" name="fruit" value="apple" v-validate:fruits="{
          required: { rule: true, message: requiredErrorMsg }
        }">
        <label for="apple">Apple</label>
        <input id="orange" type="radio" name="fruit" value="orange" v-validate:fruits>
        <label for="orange">Orage</label>
        <input id="grape" type="radio" name="fruit" value="grage" v-validate:fruits>
        <label for="grape">Grape</label>
        <input id="banana" type="radio" name="fruit" value="banana" v-validate:fruits>
        <label for="banana">Banana</label>
        <ul class="errors">
          <li v-for="msg in $validation1.fruits.messages">
            <p>{{msg}}</p>
          </li>
        </ul>
      </fieldset>
    </form>
  </validator>
</div>
```

```javascript
new Vue({
  el: '#app',
  computed: {
    requiredErrorMsg: function () {
      return 'Required fruit !!'
    }
  }
})
```


# Selectbox

```html
<div id="app">
  <validator name="validation1">
    <form novalidate>
      <select v-validate:lang="{ required: true }">
        <option value="">----- select your favorite programming language -----</option>
        <option value="javascript">JavaScript</option>
        <option value="ruby">Ruby</option>
        <option value="python">Python</option>
        <option value="perl">Perl</option>
        <option value="lua">Lua</option>
        <option value="go">Go</option>
        <option value="rust">Rust</option>
        <option value="elixir">Elixir</option>
        <option value="c">C</option>
        <option value="none">Not a nothing here</option>
      </select>
      <div class="errors">
        <p v-if="$validation1.lang.required">Required !!</p>
      </div>
    </form>
  </validator>
</div>
```

```javascript
new Vue({ el: '#app' })
```


# Grouping

The vue binding syntax can group inputs together:

```html
<validator name="validation1" :groups="['user', 'password']">
  username: <input type="text" group="user" v-validate:username="['required']"><br />
  password: <input type="text" group="password" v-validate:password1="{ minlength: 8, required: true }"/><br />
  password (confirm): <input type="text" group="password" v-validate:password2="{ minlength: 8, required: true }"/>
  <div class="user">
    <span v-if="$validation1.user.invalid">Invalid yourname !!</span>
  </div>
  <div class="password">
    <span v-if="$validation1.password.invalid">Invalid password input !!</span>
  </div>
</validator>
```


# Message

Error messages can be stored directly in the validation rules, rather than relying on `v-show` or `v-if`:

```html
<validator name="validation1">
  username: <input type="text" v-validate:username="{
    required: { rule: true, message: 'required you name !!' }
  }"><br />
  password: <input type="text" v-validate:password="{
    required: { rule: true, message: 'required you password !!' },
    minlength: { rule: 8, message: 'your password short too !!' }
  }"/><br />
  <div class="errors">
    <ul>
      <li v-for="obj in $validation1.messages">
        <div class="{{$key}}" v-for="msg in obj">
          <p>{{$key}}: {{msg}}</p>
        </div>
      </li>
    </ul>
  </div>
</validator>
```

Data property or computed properties can help reduce clutter, rather than using inline rule sets.

# Event

The new `valid` and `invalid` events can be bound using regular vue event bindings:

```javascript
new Vue({
    el: '#app',
    data: {
      occuredValid: '',
      occuredInvalid: ''
    },
    methods: {
      onValid: function () {
        this.occuredValid = 'occured valid event'
        this.occuredInvalid = ''
      },
      onInvalid: function () {
        this.occuredInvalid = 'occured invalid event'
        this.occuredValid = ''
      }
    }
  }
})
```
```html
<div id="app">
  <validator name="validation1">
    comment: <input type="text" @valid="onValid" @invalid="onInvalid" v-validate:comment="[required]"/>
    <div>
      <p>{{occuredValid}}</p>
      <p>{{occuredInvalid}}</p>
    </div>
  </validator>
</div>
```


# Lazy initialization

The `lazy` attribute on the `validator` element will delay initialization of the validator until `$activateValidator()` is called. This is useful for data that must first be loaded in asynchronously, preventing the validator from reporting invalid data until ready.

The following example waits for the comment contents to be loaded before evaluating; without `lazy`, the component would show errors until the data loads in.

```html
<!-- comment component -->
<div>
  <h1>Preview</h1>
  <p>{{comment}}</p>
  <validator lazy name="validation1">
    <input type="text" :value="comment" v-validate:comment="{ required: true, maxlength: 256 }"/>
    <span v-if="$validation1.comment.required">Required your comment</span>
    <span v-if="$validation1.comment.maxlength">Too long comment !!</span>
    <button type="button" value="save" @click="onSave" v-if="valid">
  </validator>
</div>
```

```javascript
Vue.component('comment', {
  props: {
    id: Number,
  },
  data: function () {
    return { comment: '' }
  },
  activate: function (done) {
    var resource = this.$resource('/comments/:id');
    resource.get({ id: this.id }, function (comment, stat, req) {
      this.commont =  comment.body

      // activate validator
      this.$activateValidator()
      done()

    }.bind(this)).error(function (data, stat, req) {
      // handle error ...
      done()
    })
  },
  methods: {
    onSave: function () {
      var resource = this.$resource('/comments/:id');
      resource.save({ id: this.id }, { body: this.comment }, function (data, stat, req) {
        // handle success
      }).error(function (data, sta, req) {
        // handle error
      })
    }
  }
})
```

# Custom validator

## Global registration
You can register your custom validator with using `Vue.validator`. the below the exmpale:

Cursom validators are registered to `Vue.validator` using a callback function; return true upon passing.

> **NOTE:** `Vue.validator` asset is extended from Vue.js' asset managment system.

```javascript
// register custom validator
Vue.validator('email', function (val) {
  return /^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(val)
})

new Vue({
  el: '#app'
  data: {
    email: ''
  }
})
```
```html
<div id="app">
  <validator name="validation1">
    address: <input type="text" v-validate:address="['email']"><br />
    <div>
      <p v-show="$validation1.address.email">Invalid your mail address format.</p>
    </div>
  <validator>
</div>
```

## Local registration
You can register your custom validator for component. the below the exmpale:

Cursom validators are registered to Vue constructor `validators` option using a callback function; return true upon passing.

```javascript
// `email` custom validator is global registration
Vue.validator('email', function (val) {
  return /^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(val)
})

new Vue({
  el: '#app',
  validators: { // `numeric` and `url` custom validator is local registration
    numeric: function (val) {
      return /^[-+]?[0-9]+$/.test(val)
    },
    url: function (val) {
      return /^(http\:\/\/|https\:\/\/)(.{4,})$/.test(val)
    }
  },
  data: {
    email: ''
  }
})
```

```html
<div id="app">
  <validator name="validation1">
    username: <input type="text" v-validate:username="['required']"><br />
    email: <input type="text" v-validate:address="['email']"><br />
    age: <input type="text" v-validate:age="['numeric']"><br />
    site: <input type="text" v-validate:site="['url']"><br />
    <div>
      <p v-if="$validation1.username.required">required username</p>
      <p v-if="$validation1.address.email">invalid email address</p>
      <p v-if="$validation1.age.numeric">invalid age value</p>
      <p v-if="$validation1.site.url">invalid site uril format</p>
    </div>
  <validator>
</div>
```

## Error message

Custom validators may have default error messages attached:

```javascript
// `email` custom validator global registration
Vue.validator('email', {
  message: 'invalid email address', // error message with plain string
  check: function (val) { // define validator
    return /^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/.test(val)
  }
})

// build-in `required` validator customization
Vue.validator('required', {
  message: function (field) { // error message with function
    return 'required "' + field + '" field'
  },
  check: Vue.validator('required') // re-use validator logic
})

new Vue({
  el: '#app',
  validators: {
    numeric: { // `numeric` custom validator local registration
      message: 'invalid numeric value',
      check: function (val) {
        return /^[-+]?[0-9]+$/.test(val)
      }
    },
    url: { // `url` custom validator local registration
      message: function (field) {
        return 'invalid "' + field + '" url format field'
      },
      check: function (val) {
        return /^(http\:\/\/|https\:\/\/)(.{4,})$/.test(val)
      }
    }
  },
  data: {
    email: ''
  }
})
```

```html
<div id="app">
  <validator name="validation1">
    username: <input type="text" v-validate:username="['required']"><br />
    email: <input type="text" v-validate:address="['email']"><br />
    age: <input type="text" v-validate:age="['numeric']"><br />
    site: <input type="text" v-validate:site="['url']"><br />
    <div>
      <p v-if="$validation1.username.required">{{ $validation1.username.messages.required }}</p>
      <p v-if="$validation1.address.email">{{ $validation1.address.messages.email }}</p>
      <p v-if="$validation1.age.numeric">{{ $validation1.age.messages.numeric }}</p>
      <p v-if="$validation1.site.url">{{ $validation1.site.messages.url }}</p>
    </div>
  <validator>
</div>
```


# TODO
- async validation
- validate timing customize with options
- server-side validation error applying
- more tests !!
- [and other issues...](https://github.com/vuejs/vue-validator/labels/2.0)


# Contributing
- Fork it !
- Create your top branch from `dev`: `git branch my-new-topic origin/dev`
- Commit your changes: `git commit -am 'Add some topic'`
- Push to the branch: `git push origin my-new-topic`
- Submit a pull request to `dev` branch of `vuejs/vue-validator` repository !


# Testing

```shell
$ npm test
```


# License

[MIT](http://opensource.org/licenses/MIT)
