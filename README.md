The current tech.io markdown is not standard and break the rendering compatibility with other markdown platform
This document is a proposal to make it more standard.

The current syntax looks to somethink like this:
```
@[This is the label of my run command]({"command":"run.sh", stubs:["src/hello.js"]})
```
And on github, it is rendered as:
> @[This is the label of my run command]({"command":"run.sh", stubs:["src/hello.js"]})
which is quite ugly :)

I propose to use the label syntax to hide this:
```
[TECHIO-RUN]: # (cmd:run.sh, stub:src/hello.js, title:Execute this program)
```
which is render as:
[TECHIO-RUN]: # (cmd:run.sh, stub:src/hello.js, title:Execute this program)

_Nothing... but in the source code, the previous line as been inserted_


In this syntax `[TECHIO-RUN]` is a reserved link label used to define an interactive code section. The title is moved into an attribute of the token. We can also rely on a simplified syntax (not a json with all the heavy quotes.

Most of the time, existing learning content also contains source code sample that should be displayed to the user. There is the triple backquote for this.

```
function hello() {
  console.log("hello world!");
}
```

Some contributors contains source code that should be displayed to the use. Sometime, we also want this source code to be runnable.

The markdown syntax could be more standard like:

[RUN-BEGIN]: # (cmd:run.sh, stubs:[src/index.htm:html, src/style.css])

###### Execute this program

```javascript,/project/target/src/hello.js
function hello() {
  console.log("hello world!");
}
```

[RUN-END]: #

Or for content where everything is hidden:

[RUN]: # (cmd:run.sh, stub:src/hello.js, title:Execute this program)

_you will actually need to go to the source code to actually see this_
