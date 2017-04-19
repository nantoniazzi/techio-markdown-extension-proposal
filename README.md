# Tech.io interactive code section new proposal

The current tech.io markdown is not standard and break the rendering compatibility with other markdown platforms.
This document is a proposal to make it more standard.

## Hidden interactive code

Sometime, we just want to insert in the middle of existig course a run command, that should be hidden for every platform that do not accept interactive section.

### Current syntax

Our current syntax looks to somethink like this:
```
@[This is the label of my run command]({"command":"run.sh", stubs:["src/hello.js"]})
```
And on github, it is rendered as:

@[This is the label of my run command]({"command":"run.sh", stubs:["src/hello.js"]})

which is quite ugly :)

### New proposal

I propose to use the label syntax to hide this:
```
[TECHIO-RUN]: # (cmd:run.sh, stub:src/hello.js, title:Execute this program)
```
which is render as:

[TECHIO-RUN]: # (command:run.sh, stub:src/hello.js, title:Execute this program)

_Nothing... but in the source code, the previous line has been inserted_

With this syntax `[TECHIO-RUN]` is a reserved link label used to define an interactive code section. The title is moved into an attribute of the token. We can also rely on a simplified syntax (not a json with all the heavy quotes) for the attributes name and values.

## Displayed interactive code section

Most of the time, existing learning content also contains source code sample that should be displayed to the user. There is the triple backquote syntax for this. It is rendered like this:

```
function hello() {
  console.log("hello world!");
}
```

Sometime, we want to make this code section also runnable.
I propose to surroud this code section with the tokens `TECHIO-RUN:BEGIN]` and `[TECHIO-RUN:END]`.

It could be something like this:

````
[RUN-BEGIN]: # (cmd:run.sh, stubs:[src/index.htm:html, src/style.css], title:Execute this program)

```javascript,/project/target/src/hello.js
function hello() {
  console.log("hello world!");
}
```

[RUN-END]: #
````
