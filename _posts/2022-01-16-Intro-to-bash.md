---
layout: post
title: Intro to Bash Scripting
subtitle: (draft)
categories: Bash
tags: [Bash, Intro]
---
*The content is based on DataCamp's [Intro to Bash Scripting](https://www.datacamp.com/courses/introduction-to-bash-scripting) course.*

## Intro

> Bash stands for **B**ourne **A**gain **Sh**ell

Bash was developed in the 80's. It is often the default in Unix systems and Macs. Unix is the backbone of the internet, which is why all mayor cloud providers have commandline interfaces to their products.

### Prerequisites: 

- Understand what the command line is (terminal, shell)
- Understand basic commands such as `cat`, `grep`, `sed` etc.
- check out the [bash shell cheat sheet](https://www.educative.io/blog/bash-shell-command-cheat-sheet) and this [explanation of sed](https://www.grymoire.com/Unix/Sed.html#uh-0)

#### Basic commands

- `(e)grep` filters input based on regex pattern matching
- `cat` concatenates file contents line-by-line
- `tail` \ `head` give only the last -n lines
- `wc` does a word or line count (flags: -w -l)
- `sed` pattern-matched string replacement

#### REGEX

Regular expression are a vital skill for Bash scripting. Great [site to test your expressions](https://regex101.com/).


- `[]` create a set, for example: `[afct]`
- `^` inverse a set, for example: `^[afct]`

#### Piping

- `|` used for piping, for example: `sort | uniq -c`

##### Examples

fruits.txt
```bash
banana
apple
carrot
```
> grep 'a' fruits.txt

```Output
banana
apple
carrot
```Output
> grep 'p' fruits.txt

```Output
apple
```
> grep '[pc]' fruits.txt

```Output
apple
carrot
```
> cat fruits.txt \| sort \| uniq -c \| head -n 3

```Output
1 apple
1 banana
1 carrot
```

## Bash Scripts

### General structure

A bash script usually begins with

- `#!/usr/bash` is called ***shebang*** and tells the interpreter that this is a bash script
- `which bash` can be used to *check where bash is*
- *Middle* of script contains the code
- `.sh` is conventionally used as file extension
- `bash script_name.sh`, run the script
- `./script_name.sh`, run the script if shebang is the first line 


#### Example

```bash
#!/usr/bash
echo "hello world"
echo "Goodbye world
```
> ./eg.sh

or
> bash eg.sh

```output
Hello world
Goodbye world
```

Each line in your Bash script can be a shell command. Thus, you can also include pipes in your Bash script.

### Three streams for programs

- `STDIN` (standard input) - stream of data into the program
- `STDOUT` (standard output) - stream of data out of the program
- `STDERR` (standard error) - errors in the program

The streams come from and write out to the terminal.

`2> /dev/null` in script calls redirects STDERR to be deleted (`1> /dev/null` would be STDOUT)

![STDOUT_STDIN](/assets/images/post_images/intro_to_bash_scripting/STDOUT_STDIN.png)

#### Example

sports.txt
```bash
football
basketball
swimming
```
> cat sports.txt 1> new_sports.txt
<br>cat new_sports.txt

### Arguments (ARGV)

Pass arguments by adding a space after the script execution call

- `ARGV` is the array of all the arguments given to the program
-  Each argument can be accessed via the `$` notation
    - the first argument as `$1`, the second as `$2` etc.
- `$@` and `$*` give all the arguments in ARGV
- `$#` give the length (number) of arguments

#### Example

```bash
#!/usr/bash
echo $1
echo $2
echo $@
echo "There are " $# "arguments"
```

> bash args.sh one two three four five

```Output
one
two
one two three four five
There are 5 arguments
```

## Basic variables in Bash

variables1.sh
```
firstname='Cynthia'
lastname='Liu'
echo "Hi there" $firstname $lastname
```
> bash variables1.sh

```Output
Hi there Cynthia Liu
```

- the `$` is crucial for bash to treat something as a variable and not a string
- Do not add spaces around the `=` sign
- Single quotes (`'sometext'`) = Shell interprets what is netween the quotes literally
- Double quotes (`"sometext"`) = Shell interprets literally **except** using `$`and backticks
- Backticks (**\`sometext\`**) = creates a *shell-within-a-shell*; Shell runs the command and captures STDOUT back into a variable

### Examples

*Single quotes*
```Bash
now_var='NOW'
now_var_singlequote='$now_var'
echo $now_var_singlequote
```
```Output
$now_var
```
*Double quotes*
```Bash
now_var='NOW'
now_var_doublequote="$now_var"
echo $now_var_doublequote
```
```
NOW
```
*Backticks*

Typing the following command into the terminal returns the current date
> date

```Output
Tue Jan 18 10:51:50 CET 2022
```
By using backticks, you can use `date` to invoke a *shell-within-a-shell*

```
rightnow_doublequote="The date is `date`."
echo $rightnow_doublequote
```
```Output
The date is Tue Jan 18 10:51:50 CET 2022
```
A *shell-within-a-shell* can also be achieved by using `$(date)`
```
rightnow_doublequote="The date is $(date)."
echo $rightnow_doublequote
```
```Output
The date is Tue Jan 18 10:51:50 CET 2022
```

