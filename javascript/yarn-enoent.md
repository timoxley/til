# Inexplicable yarn ENOENT error

Yesterday's issue of [corrupt global packages](https://github.com/timoxley/til/blob/master/javascript/yarn-global-packagejson.md) reoccurred intermittently for me with yarn 0.21.3.

Example error caused by running any `yarn add` command:

```
ENOENT: no such file or directory, open '/usr/local/lib/node_modules/yarn/node_modules/har-validator/lib/index.js'
```

Note it's trying to access `har-validator/lib/index.js`, which sure enough doesn't exist, but why the hell is it trying to read that in the first place?

#### tl;dr

I have no idea wtf was wrong with my computer yesterday. Rolling back yarn to 0.20.4 seemed to fix the problem, but I have no idea why it was broken or what was going on and I hope the problem doesn't come back because nothing made any sense.

## Nothing makes any sense & I hate computers

Trying to read `har-validator/lib/index.js` is super strange because it doesn't add up with the either the requiring code or the `"main"` field in `package.json`.

The package requiring this file when the error occurred was `request` and it's requiring `har-validator` directly, rather than `har-validator/lib` or anything:

```js
var validate = require('har-validator')
```
[Source](https://github.com/request/request/blob/f422111e0bc44e065a7b15e243748b59d5e99e33/lib/har.js#L5)

And the `"main"` entry in `har-validator/package.json` points at `lib/node4/promise.js`:

```js
{
  // …
  "name": "har-validator",
  "description": "Extremely fast HTTP Archive (HAR) validator using JSON Schema",
  "main": "lib/node4/promise.js",
   // …
}
```
[Source](https://github.com/ahmadnassri/har-validator/blob/b38c2d7d1286fb17788cac6447bcafa6b2cf72e1/package.json#L12)

#### Why is it trying to read `har-validator/lib/index.js`? 

I tried messing with the "main" entry in the `har-validator/package.json` to point at anything else, but my edits were ignored. I thought perhaps it was resolving to a different package (??), but `console.log(require.resolve('har-validator'))` gave me the path to the same package I was editing, and `console.log` calls in the source would appear correctly. Requiring the package from a node repl inside the `request` package directory worked perfectly fine. 

I note there's entries for `node4   node6   node7` in the `har-validator/lib` dir. I'm running node v6, is there some (broken) magic that switches the `"main"` based on the node version? Not that I could find.

At this point I tried rolling back to an older version of `yarn` ( .20.4), and that seemed to fix the problem. Upgrading back to `yarn` 0.21.3 worked for a time, but then problem came back, manifesting itself as the same error from yesterday:

```
/Users/timoxley/.config/yarn/global/node_modules/npm/node_modules/npmlog/log.js:57
log.progressEnabled = log.gauge.isEnabled()
                                ^

TypeError: log.gauge.isEnabled is not a function
    at Object.<anonymous> (/Users/timoxley/.config/yarn/global/node_modules/npm/node_modules/npmlog/log.js:57:33)
    at Module._compile (module.js:570:32)
    at Object.Module._extensions..js (module.js:579:10)
    at Module.load (module.js:487:32)
    at tryModuleLoad (module.js:446:12)
    at Function.Module._load (module.js:438:3)
    at Module.require (module.js:497:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/Users/timoxley/.config/yarn/global/node_modules/npm/lib/utils/umask.js:2:14)
    at Module._compile (module.js:570:32)
    at Object.Module._extensions..js (module.js:579:10)
    at Module.load (module.js:487:32)
    at tryModuleLoad (module.js:446:12)
    at Function.Module._load (module.js:438:3)
    at Module.require (module.js:497:17)
    at require (internal/module.js:20:19)
```

The `log.gauge` bit makes me think `yarn` has loaded an old version of `npm`, before the progress bar was added? Maybe? Why would it be doing that? Huh? I give up. Just roll back.

Overall, I have no idea wtf was going on or what to even blame to open a bug report. Maybe my SSD is dying and doing weird stuff to my files? Rolling back to the older version of `yarn` seemed to work though, so probably not. Super weird.
