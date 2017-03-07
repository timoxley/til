# zsh – report execution statistics after command completed

A neat zsh feature that comes out-of-the-box: If the `REPORTTIME` environment variable is set to a non-negative value, whenever a command takes more than `REPORTTIME` seconds, `zsh` will print execution statistics upon completion, e.g.

```
> export REPORTTIME=3
> npm install
npm ls  3.09s user 0.50s system 105% cpu 3.401 total
```

#### REPORTTIME=0

Note if you set the value to `0`, you may end up with multiple lines, as [it will also track processes executed by your shell prompt](https://github.com/robbyrussell/oh-my-zsh/issues/5331#issuecomment-247822990) e.g. `git` 

```
> export REPORTTIME=0
> ls
…
ls -G  0.00s user 0.00s system 41% cpu 0.008 total
0.01s user 0.01s system 95% cpu 0.023 total
0.00s user 0.00s system 42% cpu 0.016 total
0.00s user 0.00s system 34% cpu 0.007 total
0.00s user 0.00s system 53% cpu 0.004 total
```

#### Customizing the output format with `TIMEFMT`

You can customize the output using the `TIMEFMT` environment variable, e.g. [adding colours](https://github.com/chr4/shellrc/blob/7d57cc1747a3b1594f73e66e66e0b6df5e51bdfe/zshrc.d/reporttime.zsh)

```
autoload -Uz colors && colors

TIMEFMT="'$fg[green]%J$reset_color' time: $fg[blue]%*Es$reset_color, cpu: $fg[blue]%P$reset_color"
```

Note the `TIMEFMT` variable will affect **all** use of the zsh `time` built-in:

```
> run-help time
…
  time [ pipeline ]
              The pipeline is executed, and timing statistics are reported on the standard error in the
              form specified by the TIMEFMT parameter.  If pipeline is omitted, print statistics about 
              the shell process and its children.
…              
```

----

I'm not actually using this, instead I've started using the [sindresorhus/pure](https://github.com/sindresorhus/pure) zsh prompt, which has a [similar feature](https://github.com/sindresorhus/pure/blob/291574e652c18f3513524be88913a96038e93e19/readme.md#pure_cmd_max_exec_time) built in.
