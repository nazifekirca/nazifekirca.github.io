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
```
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

### Quotes and backticks
```
firstname='Cynthia'
lastname='Liu'
echo "Hi there" $firstname $lastname
```
```Output
Hi there Cynthia Liu
```

- the `$` is crucial for bash to treat something as a variable and not a string
- Do not add spaces around the `=` sign
- Single quotes (`'sometext'`) = Shell interprets what is netween the quotes literally
- Double quotes (`"sometext"`) = Shell interprets literally **except** using `$`and backticks
- Backticks (**\`sometext\`**) = creates a *shell-within-a-shell*; Shell runs the command and captures STDOUT back into a variable

### Examples

#### Single quotes
```Bash
now_var='NOW'
now_var_singlequote='$now_var'
echo $now_var_singlequote
```
```Output
$now_var
```
#### Double quotes
```Bash
now_var='NOW'
now_var_doublequote="$now_var"
echo $now_var_doublequote
```
```
NOW
```
#### Backticks

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

## Numeric variables in Bash

Numbers are not natively supported in Bash.

### expr

- `expr` is a useful utility program (like `cat` or `grep`)

> expr 1 + 4

```Output
5
```

- `expr` cannot handle decimal places

### bc

- `bc` (basic calculator) opens calculator which can handle decimal places
- `bc` can be used in piping by sending a string

> echo "5 + 7.5" | bc

```
12.5
```

- `bc` has a `scale` argument for defining the number of decimal places

> echo "10 / 3" | bc

```
3
```

> echo "scale=3; 10 / 3" | bc

```
3.333
```

```Bash
dog_name='Roger'
dog_age=6
echo "My dog's name is $dog_name and he is $dog_age years old"
```

### Double bracket notation (not for decimals)

> expr 5 + 7

```
12
```

> echo $((5 + 7))
```
12
```

```Bash
model1=87.65
model2=89.20
echo "The total score is $(echo "$model1 + $model2" | bc)"
echo "The average score is $(echo "($model1 + $model2) / 2" | bc)"
```

## Arrays in Bash

### 1) *Normal* numerical-indexed structure

- equivalent to a list in Python

#### Option 1 (declare)

> declare -a my_first_array

#### Option 2 (brackets and spaces)

> my_array=(1 3 5 2)


##### Return full array
> echo ${my_array[@]}
```
1 3 5 2
```

##### Return length of an array
> echo ${#my_array[@]}

##### Accessing array elements
> echo ${my_array[2]}

```
5
```
##### Manipulating array elements
> my_array[1]=999

> echo ${my_array[@]}
```
999 3 5 2
```
##### Slicing arrays

- Use `array[@]:N:M` to slice out a subset of the array
    - `N` is the starting index
    - `M` is the number of elements to be returned

```Bash
my_array=(15 20 300 42 23 2 4 33 54 67 66)
echo ${my_array[@]:3:2}
```

```Output
42 23
```

##### Appending to arrays

- Use array+=(elements)

```Bash
my_array=(300 42 23 2 4 33 54 67 66)
my_array+=(10)
echo ${my_array[@]}
```
```Output
300 42 23 2 4 33 54 67 66 10
```

### 2) *Associative* arrays

- similar to normal array, but with key-value pairs instead of numerical indexes (similar to a dictionary in Python)
- only available in Bash 4 onwards


#### Multiple line approach
```Bash
declare -A city_details # Declare first
city_details=([city_name]="New York" [population]=14000000) # Add elements
echo ${city_details[city_name]} # Index using key to return a value
```
```Output
New York
```

#### One line approach

```Bash
declare -A city_details=([city_name]="New York" [population]=14000000)
echo ${city_details[city_name]}
```

```Output
New York
```

#### Access the keys

- `!` to access the *keys*

```Bash
echo ${!city_details[@]}
```
```
city_name population
```


















### 
