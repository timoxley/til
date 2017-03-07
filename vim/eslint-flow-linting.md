# Linting a JavaScript project with `flow` + `eslint` in vim

This is way harder than it should be. 

#### tl;dr

Just use [w0rp/ale](https://github.com/w0rp/ale). It's simple, async, fast, and most importantly: **`ale` runs the local version of the linting package by default**.

Setting up `ale` was as simple as adding this to my vim config:

```js
Plugin 'w0rp/ale' # if using Vundle

let g:ale_linters = {
\   'javascript': ['eslint', 'flow']
\}
```

----

## Why not `x` ?

I had the most difficulty getting these other solutions to use the locally installed `eslint`/`flow` executable rather than a globally installed one. **Linters should never rely on globally installed executables or config files**, they should only ever use the current package's dependencies and configuration. Global packages cannot be version managed by the project's `package.json`, so two developers could be using totally different versions of `eslint`/`flow`. Additionally, using global eslint means all the project's eslint plugins need to be installed globally, but is a massive hassle if you need to use different versions of any of these tools simultaneously on different projects. Hats off to `ale` for getting this right from the start.

FYI: if you need to run locally installed excutables from the commandline you can use [timoxley/npm-run](https://github.com/timoxley/npm-run).

### Why not [syntastic](https://github.com/vim-syntastic/syntastic)?

I was already using this for linting, so I would have liked to continue using it, but:

* Hard to configure to load local eslint config.
* `flow` solutions all seemed untenably slow.
* Not async. Blocking.

### Why not [flowtype/vim-flow](https://github.com/flowtype/vim-flow)?

Official vim plugin for flow, but I couldn't get this working easily. Maybe needed additional config.

* Very slow at start up. 20s+ to open a JS file & gives an error.
* Not async. Makes the above problem worse.
* Seemed to lint entire project at once?
* Doesn't use local `flow` executable.
* Needs to work alongside something else that does `eslint` linting.
* Uses a quickfix window open at the bottom showing lint issues across whole project. I only want current file's errors to appear as signs in the margin.

### Why not [neomake](https://github.com/neomake/neomake)?

Neomake is newish and is async which is nice, however I couldn't get it configured nicely:

* Hard to configure to use local `eslint`/`flow` executables.
* Required messing around with more config to get decent looking signs.
* Lint errors seemed to appear at random times. Sometimes I'd have just `eslint` errors, other times just `flow` errors.
