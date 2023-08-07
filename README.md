# Handson for the Conclusion Code Café on Easy web development with Vue 3

These are the suggestions for getting going quickly with an easy introduction to web development with Vue 3. This handson will guide you through the essential elements of Vue applications and allows you to get going rapidly.

The main topics you will work on:
* components
* html and script 
* nested components
* style
* reactive
* developing a Vue application 
* state (reactive session data shared across components)
* UI Component libraries
* i18n

Useful resources:
* [Vue 3 Documentation](https://vuejs.org/guide/essentials/application.html)
* [Vue 3 Playground](https://play.vuejs.org/)

- [Handson for the Conclusion Code Café on Easy web development with Vue 3](#handson-for-the-conclusion-code-café-on-easy-web-development-with-vue-3)
  - [Vue Components](#vue-components)
    - [Child Component](#child-component)
    - [Expressions, Script and Vue Attributes](#expressions-script-and-vue-attributes)
    - [Interaction with Nested Components](#interaction-with-nested-components)
  - [Reactive](#reactive)
    - [Reactive Example - Clock Adjustment](#reactive-example---clock-adjustment)
  - [Software Engineering](#software-engineering)
  - [State (optional)](#state-optional)
  - [UI Libraries](#ui-libraries)
  - [i18n - internationalization](#i18n---internationalization)


## Vue Components

Before looking at applications in their entirety, we will look at the components that make up an application. A component can contain three things: 
* `template` - a mix of HTML and Vue tags and attributes, including JavaScript expressions
* `script` - JavaScript (or TypeScript) providing logic for the component and to import Vue components and other resources
* `style` - CSS style definitions intended for the HTML elements rendered by the component and

Open [this Vue Playground](https://play.vuejs.org/#eNp9kctOwzAQRX9l5HXVCGVXRZF4VAIWgKBLb9xkmrj4JT9Kpar/ztihgQXqzrnnTHwnObFb55aHhGzFmojaKRGx5QagGW/azYhAXMlORGlNU1FWWC8P5ZC1un3AKKQKhOtL6tpH9AidTaqHLYIAk/QWPdgd7KzXgAo1mhgW0wCA1GLAAML0YONIpqNneoGJpDWVmy6uppubau7KFiwG0nZyWO6DNbTIKaucdVY7qdC/ulw+cLaCQjITStmv55JFn/CnBc2M2H3+k+/DMWecvXkM6A/I2cyi8APGCa8/XvBI5xlq2ydF9hX4jsGqlDtO2l0yPdX+45W2T9pZH6UZNmF9pI8SLkvlotk8F58z+pv3V1b/rVsv6zLHzZmdvwGbtqkv) with a minimal application. 

On the left you see the source of the heart of the application, on the right you will find the result of running the application. 

![](images/component-in-playground.png)

The `template` fragment of a Vue component also can contain JavaScript expressions. For example, add this next section under the `<h1>` element in the App.vue component:

`<h3>Current Time {{new Date()}}</h3>`

This should result in the current date time being displayed under the page's main header. The `{{expression}}` or moustache-expression is how you can include an expression to be evaluated to a string to be rendered anywhere there can be plain content. Expresions can also be used to provide values for attributes for HTML (and Vue) tags, as you will see in a moment. 

Add the following snippet below the `<template>`:

``` 
<script setup> 
   const today = `Tuesday`
</script>
```

This adds our first piece of JavaScript to the component. It is rather simple and does nothing more than define a JavaScript constant called `today`.

We can refer to this JavaScript variable - even though it is a const, we still refer to it as a variable - in expressions in the `<template>`. 

Replace the `<h3>` tag you added earlier with the following:
``` 
<h3>Today is {{today}}</h3>
``` 

Of course if you set *today* to a different value, the result of rendering the component will reflect that different value.

``` 
<h3>Today is {{today}}</h3>
``` 

Expressions can contain JavaScript logic; you can for example change the expression `{{today}}` into `today.toUpperCase()`. 

Before you continue, remove the `h3` element.

### Child Component

One key characteristic of Vue - as well as HTML and any other web development framework - is the way components are created and assembled together into larger comoponents and full blown pages and applications. So far you have worked on a single component - App.vue - that contains HTML *components* that can be understood and rendered by the browser. 

Let's add a tag that the browser can not just understand. Replace the `<p>` tag with:
```
  <MyComponent></MyComponent>
```

This will not result in any content being rendered. The browser - nor the Vue transpiler - do not understand *MyComponent*. Let's help them out.

Click on the + icon, right next to the *App.vue* label:
![](images/add-component.png)

Change the proposed name `Comp.vue` into `MyComponent.vue`.

Add the following to the new component:
``` 
<template>
    <p>Here could be a number of form elements,
        images and other page content</p>
</template> 
```

You will notice that the application as rendered on the right hand side of the web page does not show yet this content.

Before the tag `MyComponent` can be interpreted in the context of *App.vue*, we have to make the component known, in an explicit way using the `import` statement.

Under the `<script setup>` tag, add this line:
```
   import MyComponent from "./MyComponent.vue" 
```

As soon as this is included, the tag `MyComponent` in *App.vue* starts to make sense. Where that tag is used, the definition in file *MyComponent.vue* is included and interpreted.

![](images/App-with-mycomponent.png)

Add the following below the occurrence of `MyComponent` in *App.vue*:

```
    <MyComponent></MyComponent>
    <h3>One More</h3>
    <MyComponent/>
```

Not because it makes so much sense contentwise but to get a feel for how the tag `MyComponent`, representing the custom component MyComponent can be used and reused.

### Expressions, Script and Vue Attributes

Vue introduces several predefined attributes that can be added to HTML or custom tags. These are used for example for conditional rendering (v-if, v-else-if, v-else) and for list rendering (v-for). 

Let's try the list rendering first. Replace

```
    <h3>One More</h3>
    <MyComponent/>
```

with

```
    <h3>Four More</h3>
    <MyComponent v-for="i in 4"/>
```
The `v-for` will loop four times and render *MyComponent* in each iteration. Note that `v-for` can also loop over arrays and objects. For example:

```
    <p v-for="color in ['red','green','blue']">
      <p>{{color}}</p>
    </p>
```

Add this to the `<template>` and you will see three colors displayed - well, their names that is. To add little color for real, add the following the style attribute to the inner `<p>` :  ``:style="`background-color:${color}`"``

![](images/v-for-in-color.png)

You may wonder: what happened here all of a sudden? What is attribute *:style* and what is that expression like value for that weird attribute doing?

I have mentioned before that in addition to using *{{}}* expressions inside *<template>* in all the places where content can be rendered, we can also use expressions when providing the values of attributes. These expressions can be simple JavaScript calculations or String manipulations, they can refer to variable defined in the *script* section of a component or to temporary variables created by *v-for*. To indicate that the value of an attribute is to be interpreted as an expression, we prefix the attribute with a colon, hence the *:style*. A normal value for *style* would be something like `background-color:red`. To make this into a dynamic expression, we create a String using the backticks: ``background-color:red`` and then we replace the hardcoded color *red* with dynamic reference `${color}` that is evaluated to whatever value the variable *color* is holding - red, green or blue.


The attribute `v-if` is used to control whether an element is rendered at all. For example, add `v-if="false"` to the `<h3>` element that proclaims *four more*:

```
<h3 v-if="false">Four more</h3>
```
The *h3* is not rendered now. 

Add this *const* definition in the *script* section:

``` 
const toggle = false
```

Change `v-if="false"` to `v-if="toggle"`. The header is still not rendered, this time controlled by the JavaScript *toggle*. Add `v-if="toggle"` to the *MyComponent* tag with the *v-for* attribute. 

The four instances of *MyComponent* are no longer rendered.

Add a new element right below the *MyComponent* tag with the *v-for* attribute.
```
<h3 v-else>Not Four more</h3>
```

The *v-else* is associated with the immediately preceding *v-if*. The *h3* tag with this attribute is only rendered if the tag with the preceding *v-if* is not.

In the *script* section, change the value of *toggle* from `false` to `true`. You will see some content reappearing, and some disappearing.

Vue makes it easy to handle user activity. The easiest example is a click on a button. 

Add a button - as the last element in the *template*:

```
<button @click="console.log('Button was clicked ')">Click Me Please</button>
```
The button appears in the web page. You can click it, as you are kindly invited to do. To see the effect of your click, you need to open the Developer Tools in your browser. Depending on the browser and your operating system, you may require a different key combination. For me it is *Ctrl+Shift+I*. Inside Developer Tools, open the *Console*. You will see the tell tale sign that the button was indeed clicked.

![](images/button-clicked.png)

### Interaction with Nested Components


properties
slots
events


## Reactive


### Reactive Example - Clock Adjustment

Open a [fresh Vue Playground](https://play.vuejs.org/). Replace the content of the *App.vue* file with the following content:

```
<script setup>
  let myClock = new Date()
</script>

<template>
  Current time is {{myClock}}  
</template>
```

You will see the date time presented. It is static the time does not change once the page is loaded. Let's add a function that can adjust the clock. Add this snippet inside the `<script> tag.

```
function adjustClock() {
  myClock = new Date()
  console.log(`new clock setting ${myClock}`)
}
```
Let's also add a button to click and invoke this function. Add this snippet inside the template:
```
  <button @click="adjustClock()">Adjust Clock</button>
```
The button should now be shown. When you click it, the variable *myClock* is assigned a new value. If you look at the *Developer Tools | Console* you should see messages with the latest time. However, the time shown in the webpage does not change. Which is unfortunate.

Here is where the notion of *reactive* is going to help. We are going to turn *myClock* into a reactive variable. We have to do three things:

* import {ref} from 'vue' 
* define *myClock* as a reactive variable - by using `ref(new Date())` instead of just `new Date()` 
* modify function *adjustClock* to make it work correctly with *myClock* as reactive variable (by acting on myClock.value instead of just myClock)

To keep seeing the newly set time in the console, you also need to add `.value` to the `${myClock}` expression in `console.log`.

After making these changes, the component has this content :

```
<script setup>
import { ref } from 'vue'

function adjustClock() {
  myClock.value = new Date()
  console.log(`new clock setting ${myClock.value}`)
}

let myClock = ref(new Date())

</script>

<template>
  Current time is {{myClock}}
  <button @click="adjustClock()">Adjust Clock</button>
</template>
```
The template did not change - only a few small changes in the `script` section. Click on the button to update the time. And again. And again.

To turn this clock into a live clock that does not require a button to be clicked for constant adjustment, you could add the following snippet in the `script` section:

```
setInterval(adjustClock, 1000)
```

Every 1000 miliseconds, function *adjustClock* will be invoked and do its thing.

## Software Engineering

* StackBlitz
* Gitpod


## State (optional)

## UI Libraries



## i18n - internationalization