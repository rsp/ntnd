# Rafał Pocztarski

You may know me from Stack Overflow

[<img alt="rsp on Stack Overflow" src="https://stackexchange.com/users/flair/303952.png" height="116">](https://stackoverflow.com/users/613198/rsp)

# pocztarski.com

Enough about me

---

# Node.js vs ts-node vs Deno

Comparing runtimes for TypeScript applications

---

A secure TypeScript runtime on V8

---

# Timeline

Node started by Ryan Dahl in 2009

Deno started by Ryan Dahl in 2018

---

# Architecture

Node = Server-side JS with V8 + libuv in C++

Deno = Server-side TS with V8 + Tokio in Rust

---

# Numbers

GitHub:
- [nodejs/node](https://github.com/nodejs/node) <img alt="GitHub stars" src="https://img.shields.io/github/stars/nodejs/node.svg?style=social" class="stars" height="40" border="0">
- [denoland/deno](https://github.com/denoland/deno) <img alt="GitHub stars" src="https://img.shields.io/github/stars/denoland/deno.svg?style=social" class="stars" height="40" border="0">

Stack Overflow:
- [Questions tagged 'node.js'](https://stackoverflow.com/questions/tagged/node.js): 270,111
- [Questions tagged 'deno'](https://stackoverflow.com/questions/tagged/deno): 9

---

# Installation

<small>
For the adventurous:<br>
`curl -fsSL https://deno.land/x/install/install.sh | sh`<br>
`iwr https://deno.land/x/install/install.ps1 | iex`

Or get a single file from:<br>
https://github.com/denoland/deno/releases

(The scripts above just scrape the GitHub releases page)
</small>

---

# DENO.LAND

github.com/denoland/deno/releases

---

# Running

`deno script.ts`

`deno https://pocztarski.com/hi.ts`

---

# Security

No network and filesystem write access by default

`deno --allow-write script.ts`

`deno --allow-net script.ts`

---

Deno vs ts-node

See my answer on Stack Overflow for details:<br>
[deno vs ts-node : what's the difference](https://stackoverflow.com/questions/53428120/deno-vs-ts-node-whats-the-difference/55609763#55609763)

For even more details see:<br>
[node-ts-hello adventures](https://gist.github.com/rsp/f7d6aec4f2bbac3de4bc3f88d871cc70)

Conclusion:<br>
Deno is 32x faster on startup for a simple example.<br>
Much easier development.

---

# Started with Go

Porting to Rust was proposed very early

<small>
Deno vs Node.js (Issue #11)<br>
https://github.com/denoland/deno/issues/11

Suggestion: Look into porting to Rust and using Tokio (Issue #205)<br>
https://github.com/denoland/deno/issues/205 <br>
(interesting discussion)
</small>

---

# Example

```
$ cat hi.ts 

import { hello } from 'https://pocztarski.com/hello.ts';

hello();
```

---

# Running

```
$ deno hi.ts

Compiling file:///Users/rsp/talks/deno/git/ntd/hi.ts
Downloading https://pocztarski.com/hello.ts
Uncaught Error: Unknown media type for: "https://pocztarski.com/hello.ts" ...
```

Oops...

---

Netlify - No fix

```
$ curl https://pocztarski.com/hello.ts -I
HTTP/1.1 200 OK
Accept-Ranges: bytes
Cache-Control: public, max-age=0, must-revalidate
Content-Length: 63
Content-Type: text/vnd.trolltech.linguist; charset=UTF-8
Date: Wed, 10 Apr 2019 07:39:40 GMT
Etag: "e23f2644d8d63e564ffcba8baa758bd3-ssl"
Strict-Transport-Security: max-age=31536000
Age: 767
Connection: keep-alive
Server: Netlify
X-NF-Request-ID: 7cb5e5c1-27a3-41ef-a352-8bb94064f514-7650812
```

---

What is text/vnd.trolltech.linguist

https://www.iana.org/assignments/media-types/text/vnd.trolltech.linguist

links to:

http://doc.trolltech.com/4.1/linguist-manual.html

(domain parking page)

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

Netlify - Headers with bad fix

```
$ curl https://pocztarski.com/hello.ts -I
HTTP/1.1 200 OK
Accept-Ranges: bytes
Cache-Control: public, max-age=0, must-revalidate
Content-Length: 63
Content-Type: text/vnd.trolltech.linguist; charset=UTF-8
Content-Type: application/x-typescript
Date: Wed, 10 Apr 2019 09:17:01 GMT
Etag: "f9feb4d50402727c955be9cb95575ab5-ssl"
Strict-Transport-Security: max-age=31536000
Age: 2
Connection: keep-alive
Server: Netlify
X-NF-Request-ID: 7cb5e5c1-27a3-41ef-a352-8bb94064f514-8367887
```

---

Netlify - Headers with good fix

```
$ curl https://pocztarski.com/hello.ts -I
HTTP/1.1 200 OK
Accept-Ranges: bytes
Cache-Control: public, max-age=0, must-revalidate
Content-Length: 63
Content-Type: application/x-typescript
Date: Wed, 10 Apr 2019 09:19:06 GMT
Etag: "59689ad05ef50b0455a56c758821512c-ssl"
Strict-Transport-Security: max-age=31536000
Age: 0
Connection: keep-alive
Server: Netlify
X-NF-Request-ID: 7cb5e5c1-27a3-41ef-a352-8bb94064f514-8384722
```

---

# Libraries

Deno Core

https://github.com/denoland/deno <img alt="GitHub stars" src="https://img.shields.io/github/stars/denoland/deno.svg?style=social" class="stars" height="40" border="0">

Deno Standard Modules

https://github.com/denoland/deno_std <img alt="GitHub stars" src="https://img.shields.io/github/stars/denoland/deno_std.svg?style=social" class="stars" height="40" border="0">

---

Frameworks

- [http](https://github.com/denoland/deno_std/tree/master/http) (std) <img alt="GitHub stars" src="https://img.shields.io/github/stars/denoland/deno_std.svg?style=social" class="stars" height="40" border="0">
- [oak](https://github.com/oakserver/oak) by Kitson Kelly (Australia) <img alt="GitHub stars" src="https://img.shields.io/github/stars/oakserver/oak.svg?style=social" class="stars" height="40" border="0">
- [dinatra](https://github.com/syumai/dinatra) by Syumai (Japan) <img alt="GitHub stars" src="https://img.shields.io/github/stars/syumai/dinatra.svg?style=social" class="stars" height="40" border="0">
- [abc](https://github.com/zhmushan/abc) by Zhmushan (China) <img alt="GitHub stars" src="https://img.shields.io/github/stars/zhmushan/abc.svg?style=social" class="stars" height="40" border="0">
- [expressive](https://github.com/jinjor/deno-playground/tree/master/expressive) by Yosuke Torii (Japan) <img alt="GitHub stars" src="https://img.shields.io/github/stars/jinjor/deno-playground.svg?style=social" class="stars" height="40" border="0">
- [fen](https://github.com/fen-land/deno-fen) by Dominic Ming (China) <img alt="GitHub stars" src="https://img.shields.io/github/stars/fen-land/deno-fen.svg?style=social" class="stars" height="40" border="0">
- [pogo](https://github.com/sholladay/pogo) by Seth Holladay (USA) <img alt="GitHub stars" src="https://img.shields.io/github/stars/sholladay/pogo.svg?style=social" class="stars" height="40" border="0">

---

Databases

- [redis](https://github.com/keroxp/deno-redis) by Yusuke Sakurai (Japan) <img alt="GitHub stars" src="https://img.shields.io/github/stars/keroxp/deno-redis.svg?style=social" class="stars" height="40" border="0">
- [postgres](https://github.com/bartlomieju/deno-postgres) by Bartek Iwańczuk (Poland) <img alt="GitHub stars" src="https://img.shields.io/github/stars/bartlomieju/deno-postgres.svg?style=social" class="stars" height="40" border="0">
- [mysql](https://github.com/manyuanrong/deno_mysql) by EnokMan (China) <img alt="GitHub stars" src="https://img.shields.io/github/stars/manyuanrong/deno_mysql.svg?style=social" class="stars" height="40" border="0">
- [Deno Simple Orm](https://github.com/manyuanrong/dso) by EnokMan (China) <img alt="GitHub stars" src="https://img.shields.io/github/stars/manyuanrong/dso.svg?style=social" class="stars" height="40" border="0">

---

Other Packages

- https://deno.land/x/
- https://denopkg.com/
- https://deno.sh/
- can be used directly from GitHub
- any CDN will work (with correct MIME type)

---

Modules Registry

https://deno.land/x/

<small>
This is a redirection service - you add modules by PRs

E.g. this install script URL:<br>
https://deno.land/x/install/install.sh<br>
redirects to:<br>
https://raw.githubusercontent.com/denoland/deno_install/master/install.sh
</small>

---

Cleaning the cache (on Mac)

```
rm -rvf ~/Library/Caches/deno
```

---

Using local caches

```
DENO_DIR=`pwd`/.deno deno hi.ts
```

---

Bug?

```
DENO_DIR=./.deno deno hi.ts
error TS2691: An import path cannot end with a '.ts' extension.
Consider importing 'https://pocztarski.com/hello' instead.
```

---

# Current state

Not ready for production yet

<small>
(which is the best time to get involved)
</small>

---

Why it *will* get traction

1. Ryan Dahl (known for Node's amazing success)
2. V8 (Google will promote it)
3. TypeScript (Microsoft will promote it)
4. Rust (Mozilla will promote it)

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
</small>

---

Resources

<small>
- https://denoland.org/
- https://deno.land/
- https://deno.land/manual.html
- https://deno.land/typedoc/
- https://deno.land/x/
- https://twitter.com/deno_land
- https://github.com/denoland/deno
- https://github.com/denoland/deno/releases
- https://github.com/denoland/deno/issues
- https://github.com/denoland/deno/pulls

</small>

---

# Questions?

Slides: https://pocztarski.com/ntd

## Rafał Pocztarski

## [pocztarski.com](https://pocztarski.com)

“The only thing that matters in software is the experience of the user.” - Ryan Dahl
