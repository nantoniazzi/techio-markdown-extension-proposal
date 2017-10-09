# Tech.io interactive code section new proposal

The current tech.io markdown is not standard and break the rendering compatibility with other markdown platforms.
This document is a proposal to make it more standard.

## Hidden interactive code

Sometime, we just want to insert in the middle of an existig documentation an interactive code content which should be hidden for every platform that do not accept interactive code section.

### Current syntax

Our current interactive code section syntax looks like this:
```
@[This is the label of my run command]({"command":"run.sh", "stubs":["src/hello.js"]})
```
And on github, it is rendered as:

@[This is the label of my run command]({"command":"run.sh", "stubs":["src/hello.js"]})

which is quite ugly and not understandable.

### New proposal

I propose to use the label syntax to hide this:
```
[RUN]: # (cmd:run.sh, stub:src/hello.js, title:Execute this program)
```
which is rendered as:

[RUN]: # (command:run.sh, stub:src/hello.js, title:Execute this program)

_Nothing... but in the source code, the previous line has really been inserted_

With this new syntax `[RUN]` is a reserved link label used to define an interactive code section. The title is moved into an attribute of the token. We can also rely on a simplified syntax (not a big json with all the heavy quotes) for the attributes name and values. You can also notice the use of the singular `stub` parameter to avoid the use of brackets to declare an array when only one stub file is necessary.

## Displayed interactive code section

Most of the time, existing learning content contains source code sample that should be displayed to the user. There is the triple backtick syntax for this:

````
```javascript
function hello() {
  console.log("hello world!");
}
```
````

It is rendered like this:

```javascript
function hello() {
  console.log("hello world!");
}
```

Sometimes, we want to make this code section also runnable.

I propose to surround this code section with the tokens `[RUN]` and `[\RUN]`.

It could be something like this:

````
[RUN]: # (cmd:run.sh, stubs:[src/index.htm:html, src/style.css], title:Execute this program)

```javascript,/project/target/src/hello.js
function hello() {
  console.log("hello world!");
}
```

```css,/project/target/src/hello.css
body { background-color: red; }
```

[\RUN]: #
````

And the displayed result would be:

[RUN]: # (cmd:run.sh, stubs:[src/index.htm:html, src/style.css], title:Execute this program)

```javascript,/project/target/src/hello.js
function hello() {
  console.log("hello world!");
}
```

```css,/project/target/src/hello.css
body { background-color: red; }
```

[\RUN]: #

You can also notice the path of the file next to the three backtick. It gives the target path where the file should be written once the `RUN` button is clicked. It is also a way to have a **working and compiling code in the docker image** and **display a non compiling content (a content to fix) to the user**. We can also include some extra stubs, using the `stub` or `stubs` attribute, which will not be displayed in the markdown.



### Other very good proposal by Max

All code blocks that have a command 

````

```javascript,path:/project/target/src/hello.js, cmd:run.sh, title:Execute this program
function hello() {
  console.log("hello world!");
}
```
```css,/project/target/src/hello.css
body { background-color: red; }
```

````

It would display this:

```javascript, dest:/project/target/src/hello.js, cmd:run.sh, title:Execute this program, stubs:[index.html, style.css]
function hello() {
  console.log("hello world!");
}
```
```css, dest:/project/target/src/hello.css
body { background-color: red; }
```

## Final proposal

````
[RUN]: # cmd:run.sh, title:Execute this program
```javascript src/hello.js
function hello() {
  console.log("hello world!");
}
```
```html index.htm
```
```css style.css
```
```css src/hello.css
body { background-color: red; }
```
````

It displays this:

[RUN]: # cmd:run.sh, title:Execute this program
```javascript src/hello.js
function hello() {
  console.log("hello world!");
}
```
```html index.htm
```
```css style.css
```
```css 
body { background-color: red; }
```

## New proposal to match the snippet syntax (oct. 9th, 2017)

````
```javascript file:src/hello.js title:'Execute this program' cmd:run.sh 
function hello() {
  console.log("hello world!");
}
```
```html index.htm
```
```css style.css
```
```css src/hello.css
body { background-color: red; }
```
````

It displays this:

```javascript file:src/hello.js title:'Execute this program' cmd:run.sh image:'node:8.6'
function hello() {
  console.log("hello world!");
}
```
```html index.htm
```
```css style.css
```
```css 
body { background-color: red; }
```
