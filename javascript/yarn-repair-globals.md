# Yarn repair global installation

### tl;dr

If your yarn global packages get corrupted somehow, running any `yarn global` command appears to repair them, e.g.

````
> yarn global ls
```

### Backstory

For some unknown reason, today my globally installed yarn packages were corrupted, including yarn itself. This manifest itself when I tried running the `npm-check-updates` (`ncu`) tool:

```
> ncu -ua
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

Weird. :/

I tried updating `ncu`, which reported a missing file in my global `node_modules`??

```
> yarn global add npm-check-updates
yarn global v0.21.3
warning No license field
[1/4] 🔍  Resolving packages...
error An unexpected error occurred: "ENOENT: no such file or directory, open '/usr/local/lib/node_modules/yarn/node_modules/har-validator/lib/index.js'".
info If you think this is a bug, please open a bug report with the information provided in "/Users/timoxley/.config/yarn/global/yarn-error.log".
info Visit https://yarnpkg.com/en/docs/cli/global for documentation about this command.
```

I know that `yarn` is pretty insistant on keeping your `node_modules` healthy so I guessed that after reinstalling `yarn` running any `yarn global` command could have the side-effect of repairing the global packages. This turned out to be accurate and after running `yarn global ls` `ncu` worked as expected. Nice one `yarn`.
