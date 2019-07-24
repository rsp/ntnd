# Rafał Pocztarski

You may know me from Stack Overflow

[<img alt="rsp on Stack Overflow" src="https://stackexchange.com/users/flair/303952.png" height="116">](https://stackoverflow.com/users/613198/rsp)

# pocztarski.com

<small>(and also from Medium, Quora, etc.)</small>

---

# <small>Node.js<br>vs<br>ts-node<br>vs<br>Deno</small>

Comparing runtimes for TypeScript applications

---

# <small>Node.js + TypeScript<br>vs<br>ts-node<br>vs<br>Deno</small>

Comparing runtimes for TypeScript applications

---

# Timeline

2009 Node.js

2012 TypeScript

2015 ts-node

2018 Deno

---

# Architecture

Node = Server-side JS with V8 + libuv in C++

Node + TypeScript = explicit transpilation to JavaScript

ts-node = Node + TypeScript with implicit transpilation

Deno = Server-side TS with V8 + Tokio in Rust

---

# Overview

---

# Node + TypeScript

explicit transpilation<br>
TypeScript compiler installed as dev dependency<br>
transpiler run manually<br>
dualism of src vs dist/build<br>
editing src, running dist<br>
committing src to GitHub and gitignoring dist<br>
publishing dist to npm and NOT npmignoring dist<br>

---

# ts-node

implicit transpilation<br>
ts-node is a Node.js module<br>
it is written in Node.js<br>
it's installed with npm<br>
it uses the TypeScript compiler as a peer dependency<br>
it installs its own dependencies<br>
as a runtime it uses Node which is written in C++ using libuv

---

# Deno

deno is a standalone executable<br>
it doesn't use Node.js<br>
it is distributed as a single binary<br>
it contains the TypeScript compiler as a V8 snapshot<br>
it has no dependencies<br>
it is a runtime written in Rust using Tokio

---

# Installation

Node + TS:<br>
install Node, npm install typescript

ts-node:<br>
install Node, npm install typescript and ts-node

Deno:<br>
get a single binary (not even a tarball)

---

# Running

Node + TS:<br>
work on TS files, transpile TS to JS with tsc, run JS files with node

ts-node:<br>
work on TS files, run TS files with tsc

Deno:<br>
work on TS files, run TS files with deno

---

# Dependencies

Node + TS:<br>
install dependencies with npm<br>
import locally installed libraries

ts-node:<br>
install dependencies with npm<br>
import locally installed libraries

Deno:<br>
import URLs directly

---

# Security

Node + TS:<br>
all programs run with node have access to all your files

ts-node:<br>
all programs run with ts-node have access to all your files

Deno:<br>
no access to files or network by default

---

# Running

`deno run script.ts`

`deno run https://pocztarski.com/hi.ts`

---

# Security

No network and filesystem access by default

`deno --allow-write script.ts`

`deno --allow-net script.ts`

---

# Deno vs ts-node

See my answer on Stack Overflow for details:<br>
[deno vs ts-node : what's the difference](https://stackoverflow.com/questions/53428120/deno-vs-ts-node-whats-the-difference/55609763#55609763)

For even more details see:<br>
[node-ts-hello adventures](https://gist.github.com/rsp/f7d6aec4f2bbac3de4bc3f88d871cc70)

Conclusion:<br>
Deno was 32x faster on startup for a simple example.<br>
Much easier development.

---

# Example

```
$ cat hi.ts 

import { hello } from 'https://pocztarski.com/hello.ts';

hello('Warsaw TypeScript');
```

---

# Running

```
$ deno run hi.ts 
Compile file:///Users/rsp/talks/ts-runtimes/hi.ts
Download https://pocztarski.com/hello.ts
Hello, Warsaw TypeScript!

$ deno run hi.ts 
Hello, Warsaw TypeScript!
```

(make sure to have correct Content-Type for ts files
e.g. Netlify serves ts files with Content-Type: text/vnd.trolltech.linguist by default)

---

# Netlify - Bad Fix

(Not working!)

```yaml
$ cat _headers

/*.ts
  Content-type: application/x-typescript
```

---

# Netlify - Good Fix

(Working!)

```yaml
$ cat _headers 

/*.ts
  Content-Type: application/x-typescript
```

---

# Libraries

Node + TypeScript: https://www.npmjs.com/

ts-node: https://www.npmjs.com/

Deno: https://deno.land/x/

---

Deno downloads and caches all the files globally by default

Cleaning the cache (on Mac)

```
rm -rvf ~/Library/Caches/deno
```

---

Using local caches

```
DENO_DIR=`pwd`/.deno deno run hi.ts
```

---

Interesting 

1. Ryan Dahl (known for Node's amazing success)
2. V8 (engine by Google)
3. TypeScript (language by Microsoft)
4. Rust (language by Mozilla)

---

My prediction

The industry will ignore it until it is "ready" and then:

1. startups who provide infrastructure and tooling will get business
2. people who used it "before it was cool" will get more job offers that they can read

(like it is now with Node.js)

---

Recommended talks

<small>
- [Ryan Dahl: Original Node.js presentation (2009)](https://www.youtube.com/watch?v=ztspvPYybIY)
- [History of Node.js by Ryan Dahl (2011)](https://www.youtube.com/watch?v=SAc0vQCC6UQ)
- [10 Things I Regret About Node.js by Ryan Dahl (2018)](https://www.youtube.com/watch?v=M3BM9TB-8yA)
- [Deno, A New Server-Side Runtime by Ryan Dahl (2018)](https://www.youtube.com/watch?v=FlTG0UXRAkE)
- [From Node.js to Deno - JavaScript/TypeScript runtime built with V8 and Rust by Rafał Pocztarski (2019)](https://www.youtube.com/watch?v=Aib1OZLy0_c&t=5s)
</small>

---

Resources

<small>
- https://deno.land/
- https://denoland.org/
- https://deno.land/manual.html
- https://deno.land/typedoc/
- https://deno.land/x/
- https://www.typescriptlang.org/
- https://github.com/TypeStrong/ts-node
- https://nodejs.org/en/
</small>

---

# Questions?

Slides: https://pocztarski.com/ntd

## Rafał Pocztarski

## [pocztarski.com](https://pocztarski.com)

“The only thing that matters in software is the experience of the user.” - Ryan Dahl
