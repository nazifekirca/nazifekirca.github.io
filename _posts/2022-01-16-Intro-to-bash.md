---
layout: post
title: Intro to Bash Scripting
subtitle: (draft)
categories: Bash
tags: [Bash, Intro]
---

<style>
    table {
        width:100%;
    }
</style>


## Intro

> Bash stands for *B*ourne *A*gain *Sh*ell

Bash was developed in the 80's. It is often the default in Unix systems and Macs.

Unix is the backbone of the internet. All mayor cloud providers have commandline interfaces to their products.

### Prerequisites: 

- Understand what the command line is (terminal, shell)
- Understand basic commands such as **cat**, **grep**, **sed** etc.

| command | function |
|---------| -------- |
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|
| (e)grep| filters input based on regex pattern matching|
| cat | concatenates file contents line-by-line  |
| tail \ head | give only the last -n lines |
| wc | does a word or line count (falgs: -w -l) |
| sed | pattern-matched string replacement  |

### REGEX

Regular expression are a vital skill for Bash scripting. See [this site](https://regex101.com/) to test your expressions.

| sign | explanation | example |
| ---- | ----------- | ------- |
| [] | create a set | [afct] |
| ^ | inverse a set | ^[afct] |

### Piping


| sign | explanation | example |
| ---- | ----------- | ------- |
| \| | used for piping | sort \| uniq -c |


## Bash Scripts

A bash script usually begins with

| convention | explanation | example |
| ---- | ----------- | ------- |
| #!/usr/bash | the ***shebang*** tells the interpreter that this is a bash script |  |
| which bash | check where bash is |  |
| Middle of script contains the code |  |  |
| .sh as file extension  | Save and run  |  |
| bash script_name.sh  | run the script  |  |
| ./script_name.sh  | run the script if shebang is the first line  |  |

### Example

```bash
#!/usr/bash
echo "hello world"
echo "Goodbye world
```
```output
Hello world
Goodbye world
```

Each line in your Bash script can be a shell command. Thus, you can also include pipes in your Bash script.

[bash shell cheat sheet](https://www.educative.io/blog/bash-shell-command-cheat-sheet)

[explanation of sed](https://www.grymoire.com/Unix/Sed.html#uh-0)