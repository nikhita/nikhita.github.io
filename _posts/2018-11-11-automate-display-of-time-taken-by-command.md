---
layout: post
title: Automate display of time taken by a command
description: How to automate displaying the last execution time of a command in your terminal.
comments: true
---

Having the need to find the time taken by a command to run from launch to finish is pretty common when you are working with computers. One handy way of accomplishing this is using the `time` command.

The following output shows the time taken (among other things) by the command `sleep 10s`.

```sh
$ time sleep 10s
sleep 10s  0.00s user 0.00s system 0% cpu 10.002 total
```

While this is pretty easy to use and solves most of the cases where we need to find the execution time, I find it annoying when the command is expected to take a long time _and_ I forget to add the `time` prefix to the command. :/

I solved this by taking a step towards the lazier axis - displaying time taken to run _each_ command after it's done executing! I did this by adding the following bit of code to my `.zshrc`.

```sh
function preexec() {
  timer=${timer:-$SECONDS}
}

function precmd() {
  if [ $timer ]; then
    timer_show=$(($SECONDS - $timer))
    export RPROMPT="%F{cyan}${timer_show}s %{$reset_color%}"
    unset timer
  fi
}
```

Here is an explanation for how this works:

- zsh has in-built commands called `preexec` and `precmd`.

- The `preexec` function is executed when a command is read and is about to be executed. So the `preexec` function captures the time when the execution starts.

- The `precmd` function is executed before each prompt. This function undertakes the subtraction: _current time - time when execution began_. This value is then displayed on the right in the terminal window.

The output on your zsh terminal will look somewhat like this:

&nbsp;
<img alt="Screenshot showing the output of the time taken by a command" src="{{ site.baseurl }}/assets/time-taken-by-command-output.png">
&nbsp;

This time will also be recorded in your terminal's history. If you want to find the time taken by a command you had run a while ago, you can open the logs and `grep` for the command.

All of this can be achieved on Bash as well, but there are some more steps involved. You can find the instructions for it [here](https://www.twistedmatrix.com/users/glyph/preexec.bash.txt).
