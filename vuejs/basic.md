# Basic
> vue.js version 2

## Declarative Rendering
```
# html:

<div id="app_declarative_rendering">
  {{ message }}
  <span v-bind:title="span_title">
    edit span title
  </span>
</div>
```
```
# js:

var app_declarative_rendering = new Vue({
  el: '#app_declarative_rendering',
  data: {
    message: 'Hello Vue!',
    span_title: 'Hello Xing.'
  }
});
```

## browser Console Update Value
```
app_declarative_rendering.span_title = 'Hello Xing312101';
```

## Conditionals and Loops
```
# html:

<div id="app_conditionals_and_loops">
  <span v-if="seen">Do you really see the man which named xing312101 ?</span>
  <div>
    <ol>
      <li v-for="person in people">
        {{ person.say }}
      </li>
    </ol>
  </div>
</div>
```
# js:

```
var app_conditionals_and_loops = new Vue({
  el: '#app_conditionals_and_loops',
  data: {
    seen: true,
    people: [
      {say: 'No, I didnt'},
      {say: 'No, I didnt'},
      {say: 'No, I didnt'},
      {say: 'No, I didnt'},
      {say: 'No, I didnt'},
      {say: 'No, I didnt'},
      {say: 'Uh, I did..........'}
    ]
  }
});
```

## Handling User Input
```
# html:

<div id="app_handle_user_input">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">See ?</button>
  <p>{{ answer }}</p>
  <input v-model="answer">
</div>
```
```
js:

var app_handle_user_input = new Vue({
  el: '#app_handle_user_input',
  data: {
    message: 'You are not be here!!!!!!',
    answer: 'I am human'
  },
  methods: {
    reverseMessage: function () {
      app_conditionals_and_loops.seen = app_conditionals_and_loops.seen ? false : true;
      this.message = this.message.split('').reverse().join('');
      this.answer = 'I am ghost';
    }
  }
});
```

## Composing with Components
```
# html:

<div id="app_composing_with_componets">
  <div>
      <ol>
        <which-you-go
          v-for="location in locations"
          v-bind:place="location"
          v-bind:key="location.id"
        ></which-you-go>
      </ol>
  </div>
</div>
```
```
# js:

Vue.component('which-you-go', {
  props: ['place'],
  template: '<li>{{place.name}}</li>'
});

var app_composing_with_components = new Vue({
  el: '#app_composing_with_componets',
  data:{
    locations: [
      {name: 'heaven'},
      {name: 'hell'}
    ]
  }
});
```
