<!-- <!------------------------------------------------------------------------
_______________________________/\/\__________________/\/\_____________
_/\/\/\/\______/\/\/\__________/\/\____/\/\/\________________/\/\/\___
_/\/\__/\/\__/\/\__/\/\____/\/\/\/\__/\/\__/\/\______/\/\__/\/\__/\/\_
_/\/\__/\/\__/\/\__/\/\__/\/\__/\/\__/\/\__/\/\______/\/\__/\/\__/\/\_
_/\/\__/\/\____/\/\/\______/\/\/\/\____/\/\/\________/\/\____/\/\/\___
_________________________________________________/\/\/\_______________
------------------------------------------------------------------------>

# Dotfile Grande



<!------------------------------------------------------------------------
    From: https://github.com/denysdovhan/bash-handbook
------------------------------------------------------------------------>


<!------------------------------------------------------------------------
# bash-handbook

[![CC 4.0][cc-image]][cc-url]
[![NPM version][npm-image]][npm-url]
[![Gitter][gitter-image]][gitter-url]

This document was written for those who want to learn Bash without diving in too deeply.

> **Tip**: Try [**learnyoubash**](https://git.io/learnyoubash) — an interactive workshopper based on this handbook!

# Node Packaged Manuscript

You can install this handbook using `npm`. Just run:

```
$ npm install -g bash-handbook
```

You should be able to run `bash-handbook` at the command line now. This will open the manual in your selected `$PAGER`. Otherwise, you may continue reading on here.

The source is available here: <https://github.com/denysdovhan/bash-handbook>

# Translations

Currently, there are these translations of **bash-handbook**:

- [Português (Brasil)](/translations/pt-BR/README.md)
- [简体中文 (中国)](/translations/zh-CN/README.md)
- [繁體中文（台灣）](/translations/zh-TW/README.md)
- [한국어 (한국)](/translations/ko-KR/README.md)

[**Request another translation**][tr-request]

[tr-request]: https://github.com/denysdovhan/bash-handbook/issues/new?title=Translation%20Request:%20%5BPlease%20enter%20language%20here%5D&body=I%20am%20able%20to%20translate%20this%20language%20%5Byes/no%5D
------------------------------------------------------------------------>

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

<!------------------------------------------------------------------------
# Table of Contents

- [Introduction](#introduction)
- [Shells and modes](#shells-and-modes)
  - [Interactive mode](#interactive-mode)
  - [Non-interactive mode](#non-interactive-mode)
  - [Exit codes](#exit-codes)
- [Comments](#comments)
- [Variables](#variables)
  - [Local variables](#local-variables)
  - [Environment variables](#environment-variables)
  - [Positional parameters](#positional-parameters)
- [Shell expansions](#shell-expansions)
  - [Brace expansion](#brace-expansion)
  - [Command substitution](#command-substitution)
  - [Arithmetic expansion](#arithmetic-expansion)
  - [Double and single quotes](#double-and-single-quotes)
- [Arrays](#arrays)
  - [Array declaration](#array-declaration)
  - [Array expansion](#array-expansion)
  - [Array slice](#array-slice)
  - [Adding elements into an array](#adding-elements-into-an-array)
  - [Deleting elements from an array](#deleting-elements-from-an-array)
- [Streams, pipes and lists](#streams-pipes-and-lists)
  - [Streams](#streams)
  - [Pipes](#pipes)
  - [Lists of commands](#lists-of-commands)
- [Conditional statements](#conditional-statements)
  - [Primary and combining expressions](#primary-and-combining-expressions)
  - [Using an `if` statement](#using-an-if-statement)
  - [Using a `case` statement](#using-a-case-statement)
- [Loops](#loops)
  - [`for` loop](#for-loop)
  - [`while` loop](#while-loop)
  - [`until` loop](#until-loop)
  - [`select` loop](#select-loop)
  - [Loop control](#loop-control)
- [Functions](#functions)
  - [Debugging](#debugging)
- [Afterword](#afterword)
- [Want to learn more?](#want-to-learn-more)
- [Other resources](#other-resources)
- [License](#license)

------------------------------------------------------------------------>
<!-- END doctoc generated TOC please keep comment here to allow auto update -->

<!------------------------------------------------------------------------
# Introduction

If you are a developer, then you know the value of time. Optimizing your work process is one of the most important aspects of the job.

In that path towards efficiency and productivity, we are often posed with actions that must be repeated over and over again, like:

* taking a screenshot and uploading it to a server
* processing text that may come in many shapes and forms
* converting files between different formats
* parsing a program's output

Enter **Bash**, our savior.

Bash is a Unix shell written by [Brian Fox][] for the GNU Project as a free software replacement for the [Bourne shell](https://en.wikipedia.org/wiki/Bourne_shell). It was released in 1989 and has been distributed as the Linux and macOS default shell for a long time.

[Brian Fox]: https://en.wikipedia.org/wiki/Brian_Fox_(computer_programmer)
<!-- link this format, because some MD processors handle '()' in URLs poorly -->

<!------------------------------------------------------------------------

So why do we need to learn something that was written more than 30 years ago? The answer is simple: this _something_ is today one of the most powerful and portable tools for writing efficient scripts for all Unix-based systems. And that's why you should learn bash. Period.

In this handbook, I'm going to describe the most important concepts in bash with examples. I hope this compendium will be helpful to you.

# Shells and modes

The user bash shell can work in two modes - interactive and non-interactive.

## Interactive mode

If you are working on Ubuntu, you have seven virtual terminals available to you.
The desktop environment takes place in the seventh virtual terminal, so you can return to a friendly GUI
using the `Ctrl-Alt-F7` keybinding.

You can open the shell using the `Ctrl-Alt-F1` keybinding. After that, the familiar GUI will disappear and one of the virtual terminals will be shown.

If you see something like this, then you are working in interactive mode:

    user@host:~$

Here you can enter a variety of Unix commands, such as `ls`, `grep`, `cd`, `mkdir`, `rm` and see the result of their execution.

We call this shell interactive because it interacts directly with the user.

Using a virtual terminal is not really convenient. For example, if you want to edit a document and execute another command at the same time, you are better off using virtual terminal emulators like:

- [GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal)
- [Terminator](https://en.wikipedia.org/wiki/Terminator_(terminal_emulator))
- [iTerm2](https://en.wikipedia.org/wiki/ITerm2)
- [ConEmu](https://en.wikipedia.org/wiki/ConEmu)

## Non-interactive mode

In non-interactive mode, the shell reads commands from a file or a pipe and executes them. When the interpreter reaches the end of the file, the shell process terminates the session and returns to the parent process.

Use the following commands for running the shell in non-interactive mode:

    sh /path/to/script.sh
    bash /path/to/script.sh

In the example above, `script.sh` is just a regular text file that consists of commands the shell interpreter can evaluate and `sh` or `bash` is the shell's interpreter program. You can create `script.sh` using your preferred text editor (e.g. vim, nano, Sublime Text, Atom, etc).

You can also simplify invoking the script by making it an executable file using the `chmod` command:


    chmod +x /path/to/script.sh

Additionally, the first line in the script must indicate which program it should use to run the file, like so:

```bash
#!/bin/bash
echo "Hello, world!"
```

Or if you prefer to use `sh` instead of `bash`, change `#!/bin/bash` to `#!/bin/sh`. This `#!` character sequence is known as the [shebang](http://en.wikipedia.org/wiki/Shebang_%28Unix%29). Now you can run the script like this:

    /path/to/script.sh

A handy trick we used above is using `echo` to print text to the terminal screen.

Another way to use the shebang line is as follows:

```bash
#!/usr/bin/env bash
echo "Hello, world!"
```

The advantage of this shebang line is it will search for the program (in this case `bash`) based on the `PATH` environment variable. This is often preferred over the first method shown above, as the location of a program on a filesystem cannot always be assumed. This is also useful if the `PATH` variable on a system has been configured to point to an alternate version of the program. For instance, one might install a newer version of `bash` while preserving the original version and insert the location of the newer version into the `PATH` variable. The use of `#!/bin/bash` would result in using the original `bash`, while `#!/usr/bin/env bash` would make use of the newer version.


## Exit codes

Every command returns an **exit code** (**return status** or **exit status**). A successful command always returns `0` (zero-code), and a command that has failed returns a non-zero value (error code). Failure codes must be positive integers between 1 and 255.

Another handy command we can use when writing a script is `exit`. This command is used to terminate the current execution and deliver an exit code to the shell. Running an `exit` code without any arguments, will terminate the running script and return the exit code of the last command executed before `exit`.

When a program terminates, the shell assigns its **exit code** to the `$?` environment variable. The `$?` variable is how we usually test whether a script has succeeded or not in its execution.

In the same way we can use `exit` to terminate a script, we can use the `return` command to exit a function and return an **exit code** to the caller. You can use `exit` inside a function too and this will exit the function _and_ terminate the program.

# Comments

Scripts may contain _comments_. Comments are special statements ignored by the `shell` interpreter. They begin with a `#` symbol and continue on to the end of the line.

For example:

```bash
#!/bin/bash
# This script will print your username.
whoami
```

> **Tip**: Use comments to explain what your script does and _why_.

# Variables

Like in most programming languages, you can also create variables in bash.

Bash knows no data types. Variables can contain only numbers or a string of one or more characters. There are three kinds of variables you can create: local variables, environment variables and variables as _positional arguments_.

## Local variables

**Local variables** are variables that exist only within a single script. They are inaccessible to other programs and scripts.

A local variable can be declared using `=` sign (as a rule, there **should not** be any spaces between a variable's name, `=` and its value) and its value can be retrieved using the `$` sign. For example:

```bash
username="denysdovhan"  # declare variable
echo $username          # display value
unset username          # delete variable
```

We can also declare a variable local to a single function using the `local` keyword. Doing so causes the variable to disappear when the function exits.

```bash
local local_var="I'm a local value"
```

## Environment variables

**Environment variables** are variables accessible to any program or script running in current shell session. They are created just like local variables, but using the keyword `export` instead.

```bash
export GLOBAL_VAR="I'm a global variable"
```

There are _a lot_ of global variables in bash. You will meet these variables fairly often, so here is a quick lookup table with the most practical ones:

| Variable     | Description                                                   |
| :----------- | :------------------------------------------------------------ |
| `$HOME`      | The current user's home directory.                            |
| `$PATH`      | A colon-separated list of directories in which the shell looks for commands. |
| `$PWD`       | The current working directory.                                |
| `$RANDOM`    | Random integer between 0 and 32767.                           |
| `$UID`       | The numeric, real user ID of the current user.                |
| `$PS1`       | The primary prompt string.                                    |
| `$PS2`       | The secondary prompt string.                                  |

Follow [this link](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_03_02.html#sect_03_02_04) to see an extended list of environment variables in Bash.

## Positional parameters

**Positional parameters** are variables allocated when a function is evaluated and are given positionally. The following table lists positional parameter variables and other special variables and their meanings when you are inside a function.

| Parameter      | Description                                                 |
| :------------- | :---------------------------------------------------------- |
| `$0`           | Script's name.                                              |
| `$1 … $9`      | The parameter list elements from 1 to 9.                     |
| `${10} … ${N}` | The parameter list elements from 10 to N.                    |
| `$*` or `$@`   | All positional parameters except `$0`.                      |
| `$#`           | The number of parameters, not counting `$0`.                 |
| `$FUNCNAME`    | The function name (has a value only inside a function).     |

In the example below, the positional parameters will be `$0='./script.sh'`,  `$1='foo'` and `$2='bar'`:

    ./script.sh foo bar

Variables may also have _default_ values. We can define as such using the following syntax:

```bash
 # if variables are empty, assign them default values
: ${VAR:='default'}
: ${$1:='first'}
# or
FOO=${FOO:-'default'}
```

# Shell expansions

_Expansions_ are performed on the command line after it has been split into _tokens_. In other words, these expansions are a mechanism to calculate arithmetical operations, to save results of commands' executions and so on.

If you are interested, you can read [more about shell expansions](https://www.gnu.org/software/bash/manual/bash.html#Shell-Expansions).

## Brace expansion

Brace expansion allows us to generate arbitrary strings. It's similar to _filename expansion_. For example:

```bash
echo beg{i,a,u}n # begin began begun
```

Also brace expansions may be used for creating ranges, which are iterated over in loops.

```bash
echo {0..5} # 0 1 2 3 4 5
echo {00..8..2} # 00 02 04 06 08
```

## Command substitution

Command substitution allow us to evaluate a command and substitute its value into another command or variable assignment. Command substitution is performed when a command is enclosed by ``` `` ``` or `$()`.  For example, we can use it as follows:

```bash
now=`date +%T`
# or
now=$(date +%T)

echo $now # 19:08:26
```

## Arithmetic expansion

In bash we are free to do any arithmetical operations. But the expression must enclosed by `$(( ))` The format for arithmetic expansions is:

```bash
result=$(( ((10 + 5*3) - 7) / 2 ))
echo $result # 9
```

Within arithmetic expansions, variables should generally be used without a `$` prefix:

```bash
x=4
y=7
echo $(( x + y ))     # 11
echo $(( ++x + y++ )) # 12
echo $(( x + y ))     # 13
```

## Double and single quotes

There is an important difference between double and single quotes. Inside double quotes variables or command substitutions are expanded. Inside single quotes they are not. For example:

```bash
echo "Your home: $HOME" # Your home: /Users/<username>
echo 'Your home: $HOME' # Your home: $HOME
```

Take care to expand local variables and environment variables within quotes if they could contain whitespace. As an innocuous example, consider using `echo` to print some user input:

```bash
INPUT="A string  with   strange    whitespace."
echo $INPUT   # A string with strange whitespace.
echo "$INPUT" # A string  with   strange    whitespace.
```

The first `echo` is invoked with 5 separate arguments — $INPUT is split into separate words, `echo` prints a single space character between each. In the second case, `echo` is invoked with a single argument (the entire $INPUT value, including whitespace).

Now consider a more serious example:

```bash
FILE="Favorite Things.txt"
cat $FILE   # attempts to print 2 files: `Favorite` and `Things.txt`
cat "$FILE" # prints 1 file: `Favorite Things.txt`
```

While the issue in this example could be resolved by renaming FILE to `Favorite-Things.txt`, consider input coming from an environment variable, a positional parameter, or the output of another command (`find`, `cat`, etc). If the input *might* contain whitespace, take care to wrap the expansion in quotes.

# Arrays

Like in other programming languages, an array in bash is a variable that allows you to refer to multiple values. In bash, arrays are also zero-based, that is, the first element in an array has index 0.

When dealing with arrays, we should be aware of the special environment variable `IFS`. **IFS**, or **Input Field Separator**, is the character that separates elements in an array. The default value is an empty space `IFS=' '`.

## Array declaration

In bash you create an array by simply assigning a value to an index in the array variable:

```bash
fruits[0]=Apple
fruits[1]=Pear
fruits[2]=Plum
```

Array variables can also be created using compound assignments such as:

```bash
fruits=(Apple Pear Plum)
```

## Array expansion

Individual array elements are expanded similar to other variables:

```bash
echo ${fruits[1]} # Pear
```

The entire array can be expanded by using `*` or `@` in place of the numeric index:

```bash
echo ${fruits[*]} # Apple Pear Plum
echo ${fruits[@]} # Apple Pear Plum
```

There is an important (and subtle) difference between the two lines above: consider an array element containing whitespace:

```bash
fruits[0]=Apple
fruits[1]="Desert fig"
fruits[2]=Plum
```

We want to print each element of the array on a separate line, so we try to use the `printf` builtin:

```bash
printf "+ %s\n" ${fruits[*]}
# + Apple
# + Desert
# + fig
# + Plum
```

Why were `Desert` and `fig` printed on separate lines? Let's try to use quoting:

```bash
printf "+ %s\n" "${fruits[*]}"
# + Apple Desert fig Plum
```

Now everything is on one line — that's not what we wanted! Here's where `${fruits[@]}` comes into play:

```bash
printf "+ %s\n" "${fruits[@]}"
# + Apple
# + Desert fig
# + Plum
```

Within double quotes, `${fruits[@]}` expands to a separate argument for each element in the array; whitespace in the array elements is preserved.

## Array slice

Besides, we can extract a slice of array using the _slice_ operators:

```bash
echo ${fruits[@]:0:2} # Apple Desert fig
```

In the example above, `${fruits[@]}` expands to the entire contents of the array, and `:0:2` extracts the slice of length 2, that starts at index 0.

## Adding elements into an array

Adding elements into an array is quite simple too. Compound assignments are specially useful in this case. We can use them like this:

```bash
fruits=(Orange "${fruits[@]}" Banana Cherry)
echo ${fruits[@]} # Orange Apple Desert fig Plum Banana Cherry
```

The example above, `${fruits[@]}` expands to the entire contents of the array and substitutes it into the compound assignment, then assigns the new value into the `fruits` array mutating its original value.

## Deleting elements from an array

To delete an element from an array, use the `unset` command:

```bash
unset fruits[0]
echo ${fruits[@]} # Apple Desert fig Plum Banana Cherry
```

# Streams, pipes and lists

Bash has powerful tools for working with other programs and their outputs. Using streams we can send the output of a program into another program or file and thereby write logs or whatever we want.

Pipes give us opportunity to create conveyors and control the execution of commands.

It is paramount we understand how to use this powerful and sophisticated tool.

## Streams

Bash receives input and sends output as sequences or **streams** of characters. These streams may be redirected into files or one into another.

There are three descriptors:

| Code | Descriptor | Description          |
| :--: | :--------: | :------------------- |
| `0`  | `stdin`    | The standard input.  |
| `1`  | `stdout`   | The standard output. |
| `2`  | `stderr`   | The errors output.   |

Redirection makes it possible to control where the output of a command goes to, and where the input of a command comes from. For redirecting streams these operators are used:

| Operator | Description                                  |
| :------: | :------------------------------------------- |
| `>`      | Redirecting output                           |
| `&>`     | Redirecting output and error output          |
| `&>>`    | Appending redirected output and error output |
| `<`      | Redirecting input                            |
| `<<`     | [Here documents](http://tldp.org/LDP/abs/html/here-docs.html) syntax |
| `<<<`    | [Here strings](http://www.tldp.org/LDP/abs/html/x17837.html) |

Here are few examples of using redirections:

```bash
# output of ls will be written to list.txt
ls -l > list.txt

# append output to list.txt
ls -a >> list.txt

# all errors will be written to errors.txt
grep da * 2> errors.txt

# read from errors.txt
less < errors.txt
```

## Pipes

We could redirect standard streams not only in files, but also to other programs. **Pipes** let us use the output of a program as the input of another.

In the example below, `command1` sends its output to `command2`, which then passes it on to the input of `command3`:

    command1 | command2 | command3

Constructions like this are called **pipelines**.

In practice, this can be used to process data through several programs. For example, here the output of `ls -l` is sent to the `grep` program, which  prints only files with a `.md` extension, and this output is finally sent to the `less` program:

    ls -l | grep .md$ | less

The exit status of a pipeline is normally the exit status of the last command in the pipeline. The shell will not return a status until all the commands in the pipeline have completed. If you want your pipelines to be considered a failure if any of the commands in the pipeline fail, you should set the pipefail option with:

    set -o pipefail

## Lists of commands

A **list of commands** is a sequence of one or more pipelines separated by `;`, `&`, `&&` or `||` operator.

If a command is terminated by the control operator `&`, the shell executes the command asynchronously in a subshell. In other words, this command will be executed in the background.

Commands separated by a `;` are executed sequentially: one after another. The shell waits for the finish of each command.

```bash
# command2 will be executed after command1
command1 ; command2

# which is the same as
command1
command2
```

Lists separated by `&&` and `||` are called _AND_ and _OR_ lists, respectively.

The _AND-list_ looks like this:

```bash
# command2 will be executed if, and only if, command1 finishes successfully (returns 0 exit status)
command1 && command2
```

The _OR-list_ has the form:

```bash
# command2 will be executed if, and only if, command1 finishes unsuccessfully (returns code of error)
command1 || command2
```

The return code of an _AND_ or _OR_ list is the exit status of the last executed command.

# Conditional statements

Like in other languages, Bash conditionals let us decide to perform an action or not.  The result is determined by evaluating an expression, which should be enclosed in `[[ ]]`.

Conditional expression may contain `&&` and `||` operators, which are _AND_ and _OR_ accordingly. Besides this, there many [other handy expressions](#primary-and-combining-expressions).

There are two different conditional statements: `if` statement and `case` statement.

## Primary and combining expressions

Expressions enclosed inside `[[ ]]` (or `[ ]` for `sh`) are called **test commands** or **primaries**. These expressions help us to indicate results of a conditional. In the tables below, we are using `[ ]`, because it works for `sh` too. Here is an answer about [the difference between double and single square brackets in bash](http://serverfault.com/a/52050).

**Working with the file system:**

| Primary       | Meaning                                                      |
| :-----------: | :----------------------------------------------------------- |
| `[ -e FILE ]` | True if `FILE` **e**xists.                                   |
| `[ -f FILE ]` | True if `FILE` exists and is a regular **f**ile.             |
| `[ -d FILE ]` | True if `FILE` exists and is a **d**irectory.                |
| `[ -s FILE ]` | True if `FILE` exists and not empty (**s**ize more than 0).  |
| `[ -r FILE ]` | True if `FILE` exists and is **r**eadable.                   |
| `[ -w FILE ]` | True if `FILE` exists and is **w**ritable.                   |
| `[ -x FILE ]` | True if `FILE` exists and is e**x**ecutable.                 |
| `[ -L FILE ]` | True if `FILE` exists and is symbolic **l**ink.              |
| `[ FILE1 -nt FILE2 ]` | FILE1 is **n**ewer **t**han FILE2.                   |
| `[ FILE1 -ot FILE2 ]` | FILE1 is **o**lder **t**han FILE2.                   |

**Working with strings:**

| Primary        | Meaning                                                     |
| :------------: | :---------------------------------------------------------- |
| `[ -z STR ]`   | `STR` is empty (the length is **z**ero).                    |
| `[ -n STR ]`   |`STR` is not empty (the length is **n**on-zero).             |
| `[ STR1 == STR2 ]` | `STR1` and `STR2` are equal.                            |
| `[ STR1 != STR2 ]` | `STR1` and `STR2` are not equal.                        |

**Arithmetic binary operators:**

| Primary             | Meaning                                                |
| :-----------------: | :----------------------------------------------------- |
| `[ ARG1 -eq ARG2 ]` | `ARG1` is **eq**ual to `ARG2`.                         |
| `[ ARG1 -ne ARG2 ]` | `ARG1` is **n**ot **e**qual to `ARG2`.                 |
| `[ ARG1 -lt ARG2 ]` | `ARG1` is **l**ess **t**han `ARG2`.                    |
| `[ ARG1 -le ARG2 ]` | `ARG1` is **l**ess than or **e**qual to `ARG2`.        |
| `[ ARG1 -gt ARG2 ]` | `ARG1` is **g**reater **t**han `ARG2`.                 |
| `[ ARG1 -ge ARG2 ]` | `ARG1` is **g**reater than or **e**qual to `ARG2`.     |

Conditions may be combined using these **combining expressions:**

| Operation      | Effect                                                      |
| :------------: | :---------------------------------------------------------- |
| `[ ! EXPR ]`   | True if `EXPR` is false.                                    |
| `[ (EXPR) ]`   | Returns the value of `EXPR`.                                |
| `[ EXPR1 -a EXPR2 ]` | Logical _AND_. True if `EXPR1` **a**nd `EXPR2` are true. |
| `[ EXPR1 -o EXPR2 ]` | Logical _OR_. True if `EXPR1` **o**r `EXPR2` are true.|

Sure, there are more useful primaries and you can easily find them in the [Bash man pages](http://www.gnu.org/software/bash/manual/html_node/Bash-Conditional-Expressions.html).

## Using an `if` statement

`if` statements work the same as in other programming languages. If the expression within the braces is true, the code between `then` and `fi` is executed.  `fi` indicates the end of the conditionally executed code.

```bash
# Single-line
if [[ 1 -eq 1 ]]; then echo "true"; fi

# Multi-line
if [[ 1 -eq 1 ]]; then
  echo "true"
fi
```

Likewise, we could use an `if..else` statement such as:

```bash
# Single-line
if [[ 2 -ne 1 ]]; then echo "true"; else echo "false"; fi

# Multi-line
if [[ 2 -ne 1 ]]; then
  echo "true"
else
  echo "false"
fi
```

Sometimes `if..else` statements are not enough to do what we want to do. In this case we shouldn't forget about the existence of `if..elif..else` statements, which always come in handy.

Look at the example below:

```bash
if [[ `uname` == "Adam" ]]; then
  echo "Do not eat an apple!"
elif [[ `uname` == "Eva" ]]; then
  echo "Do not take an apple!"
else
  echo "Apples are delicious!"
fi
```

## Using a `case` statement

If you are confronted with a couple of different possible actions to take, then using a `case` statement may be more useful than nested `if` statements. For more complex conditions use `case` like below:

```bash
case "$extension" in
  "jpg"|"jpeg")
    echo "It's image with jpeg extension."
  ;;
  "png")
    echo "It's image with png extension."
  ;;
  "gif")
    echo "Oh, it's a giphy!"
  ;;
  *)
    echo "Woops! It's not image!"
  ;;
esac
```

Each case is an expression matching a pattern. The `|` sign is used for separating multiple patterns, and the `)` operator terminates a pattern list. The commands for the first match are executed. `*` is the pattern for anything else that doesn't match the defined patterns. Each block of commands should be divided with the `;;` operator.

# Loops

Here we won't be surprised. As in any programming language, a loop in bash is a block of code that iterates as long as the control conditional is true.

There are four types of loops in Bash: `for`, `while`, `until` and `select`.

## `for` loop

The `for` is very similar to its sibling in C. It looks like this:

```bash
for arg in elem1 elem2 ... elemN
do
  # statements
done
```

During each pass through the loop, `arg` takes on the value from `elem1` to `elemN`. Values may also be wildcards or [brace expansions](#brace-expansion).

Also, we can write `for` loop in one line, but in this case there needs to be a semicolon before `do`, like below:

```bash
for i in {1..5}; do echo $i; done
```

By the way, if `for..in..do` seems a little bit weird to you, you can also write `for` in C-like style such as:

```bash
for (( i = 0; i < 10; i++ )); do
  echo $i
done
```

`for` is handy when we want to do the same operation over each file in a directory. For example, if we need to move all `.bash` files into the `script` folder and then give them execute permissions, our script would look like this:

```bash
#!/bin/bash

for FILE in $HOME/*.bash; do
  mv "$FILE" "${HOME}/scripts"
  chmod +x "${HOME}/scripts/${FILE}"
done
```

## `while` loop

The `while` loop tests a condition and loops over a sequence of commands so long as that condition is _true_. A condition is nothing more than a [primary](#primary-and-combining-expressions) as used in `if..then` conditions. So a `while` loop looks like this:

```bash
while [[ condition ]]
do
  # statements
done
```

Just like in the case of the `for` loop, if we want to write `do` and condition in the same line, then we must use a semicolon before `do`.

A working example might look like this:

```bash
#!/bin/bash

# Squares of numbers from 0 through 9
x=0
while [[ $x -lt 10 ]]; do # value of x is less than 10
  echo $(( x * x ))
  x=$(( x + 1 )) # increase x
done
```

## `until` loop

The `until` loop is the exact opposite of the `while` loop. Like a `while` it checks a test condition, but it keeps looping as long as this condition is _false_:

```bash
until [[ condition ]]; do
  #statements
done
```

## `select` loop

The `select` loop helps us to organize a user menu. It has almost the same syntax as the `for` loop:

```bash
select answer in elem1 elem2 ... elemN
do
  # statements
done
```

The `select` prints all `elem1..elemN` on the screen with their sequence numbers, after that it prompts the user. Usually it looks like `$?` (`PS3` variable). The answer will be saved in `answer`. If `answer` is the number between `1..N`, then `statements` will execute and `select` will go to the next iteration — that's because we should use the `break` statement.

A working example might look like this:

```bash
#!/bin/bash

PS3="Choose the package manager: "
select ITEM in bower npm gem pip
do
  echo -n "Enter the package name: " && read PACKAGE
  case $ITEM in
    bower) bower install $PACKAGE ;;
    npm)   npm   install $PACKAGE ;;
    gem)   gem   install $PACKAGE ;;
    pip)   pip   install $PACKAGE ;;
  esac
  break # avoid infinite loop
done
```

This example, asks the user what package manager {s,he} would like to use. Then, it will ask what package we want to install and finally proceed to install it.

If we run this, we will get:

```
$ ./my_script
1) bower
2) npm
3) gem
4) pip
Choose the package manager: 2
Enter the package name: bash-handbook
<installing bash-handbook>
```

## Loop control

There are situations when we need to stop a loop before its normal ending or step over an iteration. In these cases, we can use the shell built-in `break` and `continue` statements. Both of these work with every kind of loop.

The `break` statement is used to exit the current loop before its ending. We have already met with it.

The `continue` statement steps over one iteration. We can use it as such:

```bash
for (( i = 0; i < 10; i++ )); do
  if [[ $(( i % 2 )) -eq 0 ]]; then continue; fi
  echo $i
done
```

If we run the example above, it will print all odd numbers from 0 through 9.

# Functions

In scripts we have the ability to define and call functions. As in any programming language, functions in bash are chunks of code, but there are differences.

In bash, functions are a sequence of commands grouped under a single name, that is the _name_ of the function. Calling a function is the same as calling any other program, you just write the name and the function will be _invoked_.

We can declare our own function this way:

```bash
my_func () {
  # statements
}

my_func # call my_func
```

We must declare functions before we can invoke them.

Functions can take on arguments and return a result — exit code. Arguments, within functions, are treated in the same manner as arguments given to the script in [non-interactive](#non-interactive-mode) mode — using [positional parameters](#positional-parameters). A result code can be _returned_ using the `return` command.

Below is a function that takes a name and returns `0`, indicating successful execution.

```bash
# function with params
greeting () {
  if [[ -n $1 ]]; then
    echo "Hello, $1!"
  else
    echo "Hello, unknown!"
  fi
  return 0
}

greeting Denys  # Hello, Denys!
greeting        # Hello, unknown!
```

We already discussed [exit codes](#exit-codes). The `return` command without any arguments returns the exit code of the last executed command. Above, `return 0` will return a successful exit code. `0`.

## Debugging

The shell gives us tools for debugging scripts. If we want to run a script in debug mode, we use a special option in our script's shebang:

```bash
#!/bin/bash options
```

These options are settings that change shell behavior. The following table is a list of options which might be useful to you:

| Short | Name        | Description                                            |
| :---: | :---------- | :----------------------------------------------------- |
| `-f`  | noglob      | Disable filename expansion (globbing).                 |
| `-i`  | interactive | Script runs in _interactive_ mode.                     |
| `-n`  | noexec      | Read commands, but don't execute them (syntax check).  |
|       | pipefail    | Make pipelines fail if any commands fail, not just if the final command fail. |
| `-t`  | —           | Exit after first command.                              |
| `-v`  | verbose     | Print each command to `stderr` before executing it.    |
| `-x`  | xtrace      | Print each command and its expanded arguments to `stderr` before executing it. |

For example, we have script with `-x` option such as:

```bash
#!/bin/bash -x

for (( i = 0; i < 3; i++ )); do
  echo $i
done
```

This will print the value of the variables to `stdout` along with other useful information:

```
$ ./my_script
+ (( i = 0 ))
+ (( i < 3 ))
+ echo 0
0
+ (( i++  ))
+ (( i < 3 ))
+ echo 1
1
+ (( i++  ))
+ (( i < 3 ))
+ echo 2
2
+ (( i++  ))
+ (( i < 3 ))
```

Sometimes we need to debug a part of a script. In this case using the `set` command is convenient. This command can enable and disable options. Options are turned on using `-` and turned off using `+`:

```bash
#!/bin/bash

echo "xtrace is turned off"
set -x
echo "xtrace is enabled"
set +x
echo "xtrace is turned off again"
```

# Afterword

I hope this small handbook was interesting and helpful. To be honest, I wrote this handbook for myself so as to not forget the bash basics. I tried to write concisely but meaningfully, and I hope you will appreciate that.

This handbook narrates my own experience with Bash. It does not purport to be comprehensive, so if you still want more, please run `man bash` and start there.

Contributions are absolutely welcome and I will be grateful for any corrections or questions you can send my way. For all of that create a new [issue](https://github.com/denysdovhan/bash-handbook/issues).

Thanks for reading this handbook!

# Want to learn more?

Here's a list of other literature covering Bash:

* Bash man page.  In many environments that you can run Bash, the help system `man` can display information about Bash, by running the command `man bash`.  For more information on the `man` command, see the web page ["The man Command"](http://www.linfo.org/man.html) hosted at [The Linux Information Project](http://www.linfo.org/).
* ["Bourne-Again SHell manual"](https://www.gnu.org/software/bash/manual/) in many formats, including HTML, Info, TeX, PDF, and Texinfo.  Hosted at <https://www.gnu.org/>.  As of 2016/01, this covers version 4.3, last updated 2015/02/02.

# Other resources

* [awesome-bash](https://github.com/awesome-lists/awesome-bash) is a curated list of Bash scripts and resources
* [awesome-shell](https://github.com/alebcay/awesome-shell) is another curated list of shell resources
* [bash-it](https://github.com/Bash-it/bash-it) provides a solid framework for using, developing and maintaining shell scripts and custom commands for your daily work.
* [Bash Guide for Beginners](http://tldp.org/LDP/Bash-Beginners-Guide/html/) a good resource between the [HOWTO](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO.html) and the [Bash Scripting](http://tldp.org/LDP/abs/html/) guide.
* [dotfiles.github.io](http://dotfiles.github.io/) is a good source of pointers to the various dotfiles collections and shell frameworks available for bash and other shells.
* [learnyoubash](https://github.com/denysdovhan/learnyoubash) helps you write your first bash script
* [shellcheck](https://github.com/koalaman/shellcheck) is a static analysis tool for shell scripts. You can either use it from a web page at [www.shellcheck.net](http://www.shellcheck.net/) or run it from the command line. Installation instructions are on the [koalaman/shellcheck](https://github.com/koalaman/shellcheck) github repository page.

Finally, Stack Overflow has many questions that are [tagged as bash](https://stackoverflow.com/questions/tagged/bash) that you can learn from and is a good place to ask if you're stuck.

# License

[![CC 4.0][cc-image]][cc-url]

&copy; [Denys Dovhan](http://denysdovhan.com)

[cc-url]: http://creativecommons.org/licenses/by/4.0/
[cc-image]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg?style=flat-square

[npm-url]: https://npmjs.org/package/bash-handbook
[npm-image]: https://img.shields.io/npm/v/bash-handbook.svg?style=flat-square

[gitter-url]: https://gitter.im/denysdovhan/bash-handbook
[gitter-image]: https://img.shields.io/gitter/room/nwjs/nw.js.svg?style=flat-square -->


<!------------------------------------------------------------------------
    From: https://github.com/huyng/bashmarks
------------------------------------------------------------------------>

<!------------------------------------------------------------------------

### Bashmarks is a shell script that allows you to save and jump to commonly used directories. Now supports tab completion.

## Install

1. git clone git://github.com/huyng/bashmarks.git
2. cd bashmarks
3. make install
4. source **~/.local/bin/bashmarks.sh** from within your **~.bash\_profile** or **~/.bashrc** file

## Shell Commands

    s <bookmark_name> - Saves the current directory as "bookmark_name"
    g <bookmark_name> - Goes (cd) to the directory associated with "bookmark_name"
    p <bookmark_name> - Prints the directory associated with "bookmark_name"
    d <bookmark_name> - Deletes the bookmark
    l                 - Lists all available bookmarks

## Example Usage

    $ cd /var/www/
    $ s webfolder
    $ cd /usr/local/lib/
    $ s locallib
    $ l
    $ g web<tab>
    $ g webfolder

## Where Bashmarks are stored

All of your directory bookmarks are saved in a file called ".sdirs" in your HOME directory.

------------------------------------------------------------------------>


<!-- # git-extra-commands

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![CircleCI](https://circleci.com/gh/unixorn/git-extra-commands.svg?style=shield)](https://circleci.com/gh/unixorn/git-extra-commands)
[![Code Climate](https://codeclimate.com/github/unixorn/git-extra-commands/badges/gpa.svg)](https://codeclimate.com/github/unixorn/git-extra-commands)
[![Issue Count](https://codeclimate.com/github/unixorn/git-extra-commands/badges/issue_count.svg)](https://codeclimate.com/github/unixorn/git-extra-commands)
[![GitHub stars](https://img.shields.io/github/stars/unixorn/git-extra-commands.svg)](https://github.com/unixorn/git-extra-commands/stargazers)

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

<!------------------------------------------------------------------------

## Table of Contents

- [Included Scripts](#included-scripts)
- [Useful git aliases](#useful-git-aliases)
- [Installing](#installing)
  - [Pre-requisites](#pre-requisites)
  - [zgen](#zgen)
  - [Antigen](#antigen)
  - [oh-my-zsh](#oh-my-zsh)
  - [Bash / Manual Installation](#bash--manual-installation)
- [Other useful git stuff](#other-useful-git-stuff)
  - [Articles / Blog posts / Books](#articles--blog-posts--books)
  - [External Git Utilities](#external-git-utilities)
- [Miscellaneous Tips](#miscellaneous-tips)
  - [Rewrite git:// with https://](#rewrite-git-with-https)
  - [or replace with `ssh`](#or-replace-with-ssh)
- [Contributing](#contributing)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

<!------------------------------------------------------------------------

**git-extra-commands** is a ZSH plugin that packages some extra `git` helper scripts I've found. This collection (and the scripts that I wrote in it) is licensed with the Apache Version 2 license.

However, some of the scripts in this collection came from other sources and may have different licensing - if they do, their license information is included inline in the script source.

This collection doesn't actually require ZSH, but packaging it as a ZSH plugin makes it more convenient for people using a ZSH framework to use this collection.

If you wrote one of these scripts and want it removed from this collection, please either make a PR and/or file an issue against the repo and I will remove it.

## Included Scripts

| Script | Original Source | Description |
| ------ | --------------- | ----------- |
| `git-add-username-remote` | Ryan Tomayko's [dotfiles](https://github.com/rtomayko/dotfiles) | Adds a remote for the current repository for the given github username. |
| `git-age` | Kristoffer Gronlund's [wiki](https://github.com/krig/git-age/wiki) | A git-blame viewer, written using PyGTK.|
| `git-attic` | Christian Neukirchen's [blog](http://chneukirchen.org/blog/archive/2013/01/a-grab-bag-of-git-tricks.html) | Displays a list of deleted files in your repo. The output is designed to be copy and pasted: Pass the second field to `git show` to display the file contents, or just select the hash without ^ to see the commit where removal happened. |
| `git-big-file` | Mislav Marohnić's [dotfiles](https://github.com/mislav/dotfiles) | Show files in the repo larger than a threshold size. |
| `git-branch-name` | Joe Block <jpb@unixorn.net> | Prints the current branch name in automation-friendly format. |
| `git-branch-rebaser` | Vengada Rangaraju <krangaraju@castlighthealth.com> | Kicks off an interactive rebase of all the commits on your branch. _Including pushed commits_, so be careful. |
| `git-change-author` | Michael Demmer in [jut-io/git-scripts](https://github.com/jut-io/git-scripts/blob/master/bin/git-change-author) | Change one author/email in the history to another. |
| `git-change-log` | John Wiegley's [git-scripts](https://github.com/jwiegley/git-scripts) | Transform `git log` output into a complete Changelog for projects that haven't been maintaining one. |
| `git-changes` | Michael Markert's [dotfiles](https://github.com/cofi/dotfiles) | List authors in the repo in descending commit-count order. |
| `git-churn` | Gary Bernhardt's [dotfiles](https://github.com/garybernhardt/dotfiles/blob/master/bin/git-churn) | Show which files are getting changed most often in the repository. |
| `git-clone-subset` | Rodrigo Silva (MestreLion) <linux@rodrigosilva.com> | Uses `git clone` and `git filter-branch` to remove from the clone all files but the ones requested, along with their associated commit history. |
| `git-comma` | Christian Neukirchen's [blog](http://chneukirchen.org/blog/archive/2013/01/a-grab-bag-of-git-tricks.html) | Adds and commits a file in one command |
| `git-conflicts` | Seth Messer's [bits and bobs](https://github.com/megalithic/bits-and-bobs/) repo | Show files with conflicts |
| `git-copy-branch-name` | Zach Holman's [dotfiles](https://github.com/holman/dotfiles) | Copy the current branch's name to the clipboard (macOS Only). |
| `git-credit` | Zach Holman's [dotfiles](https://github.com/holman/dotfiles) | Quicker way to assign credit to another author on the latest commit. |
| `git-current-branch` | Joe Block <jpb@unixorn.net> | Prints the name of the current branch, mainly useful in automation scripts. |
| `git-cut-branch` | Ryan Tomayko's [dotfiles](https://github.com/rtomayko/dotfiles) | Create a new branch pointed at **HEAD** and reset the current branch to the head of its tracking branch |
| `git-delete-local-merged` | From a deleted post by @tekkub | Delete all local branches that have been merged into **HEAD**. |
| `git-delete-merged-branches` | ? | Purges all branches that have been merged to a target branch (defaults to branches merged to master). |
| `git-delete-tag` | Joe Block <jpb@unixorn.net> | Delete a tag, both locally and from the origin remote. |
| `git-diff-last` | [Sebastian Schuberth](https://github.com/sschuberth) | Show the last change made to a file in the repository. |
| `git-divergence` | Gary Bernhardt's [dotfiles](https://github.com/garybernhardt/dotfiles/blob/master/bin/git-churn) | Shows differences between local branch and its tracking branch. |
| `git-edit-conflicts` | Joe Block <jpb@unixorn.net> | Edit the files that are marked as conflicted during a merge/rebase in your `$EDITOR/$VISUAL`. |
| `git-find-dirty` | Matthew McCullough's [scripts](https://github.com/matthewmccullough/scripts/) repository | |
| `git-flush` | John Wiegley's [git-scripts](https://github.com/jwiegley/git-scripts) | Compact your reposistory by dropping all reflogs, stashes, and other cruft that may be bloating your pack files. |
| `git-force-mtimes` | John Wiegley's [git-scripts](https://github.com/jwiegley/git-scripts) | Sets mtimes of all files in the reprository their last change date based on git's log. Useful to avoid too new dates after a checkout confusing `make` or `rake`. |
| `git-forest` | Jan Engelhardt | Prints a text-based tree visualisation of your repository. Requires [Git.pm](https://metacpan.org/release/Git) |
| `git-git` | Joe Block <jpb@unixorn.net> | Typing `git git foo` will make git do a `git foo` instead of complaining. |
| `git-github-open` | ? | Open GitHub file/blob page for FILE on LINE. |
| `git-gitlab-mr` | Noel Cower's [gist](https://gist.github.com/nilium/ac808ee3729cdce01ec0f3c0a499f099) | Open a merge request on GitLab |
| `git-ignored` | ? | Show files being ignored by git in the repo. |
| `git-improved-merge` | Mislav Marohnić's [dotfiles](https://github.com/mislav/dotfiles) | Sophisticated git merge with integrated CI check and automatic cleanup. |
| `git-incoming` | Michael Markert's [dotfiles](https://github.com/cofi/dotfiles) | Show commits in the tracking branch that are not in the local branch. |
| `git-lines` | [Neil Killeen](https://github.com/kiLLeen) <nkilleen@castlighthealth.com> | Gives you a list of author names with the number of lines last updated by that user in files in the current directory tree with the extension specified. |
| `git-ls-object-refs` | Ryan Tomayko's [dotfiles](https://github.com/rtomayko/dotfiles) | Find references to an object with SHA1 in refs, commits, and trees. All of them. |
| `git-maildiff` | Sanjeev Kumar's [blogpost](http://www.devilsan.com/blog/my-first-git-command-git-ipush-using-python) | A simple git command to email diff in color to reviewer/ co-worker. |
| `git-maxpack` | John Wiegley's [git-scripts](https://github.com/jwiegley/git-scripts) | Compress a repo's pack files as much as possible. |
| `git-move-commits` | Corey Oordt's [git-scripts](https://github.com/coordt/git-scripts/blob/master/git-move-commits) | `git move-commits num-commits correct-branch` moves the last n commits to correct-branch (creating it if necessary). |
| `git-neck` | Christian Neukirchen's [blog](http://chneukirchen.org/blog/archive/2013/01/a-grab-bag-of-git-tricks.html) | Show commits from the HEAD until the first branching point. Companion script for `git-trail`. |
| `git-nuke` | Zach Holman's [dotfiles](https://github.com/holman/dotfiles) | Nukes a branch locally and on the origin remote. |
| `git-object-deflate` | Ryan Tomayko's [dotfiles](https://github.com/rtomayko/dotfiles) | Deflate an loose object file and write to standard output. |
| `git-outgoing` | Michael Markert's [dotfiles](https://github.com/cofi/dotfiles) | Show commits that are on the local branch that have not been pushed to the tracking branch. |
| `git-overwritten` | Mislav Marohnić's [dotfiles](https://github.com/mislav/dotfiles) | Aggregates git blame information about original owners of lines changed or removed in the '<base>...<head>' diff. |
| `git-pie-ify` | JeeBak Kim's [gist](https://gist.github.com/jeebak/f9088cede18d31f2d3a0) | `git pie-ify pattern replacement` |
| `git-plotrepo` | Matthew McCullogh's [scripts collection](https://github.com/matthewmccullough/scripts/blob/master/git-plotrepo.rb) | Uses dot to draw a graph of the repository. |
| `git-promote` | Trevor's **Improving My git Workflow** blog post (404 now) | Promotes a local topic branch to a remote tracking branch of the same name. |
| `git-prune-branches` | Michael Demmer in [jut-io/git-scripts](https://github.com/jut-io/git-scripts/blob/master/bin/git-prune-branches) | Deletes each fully merged branch after prompting for confirmation, than asks if you want the deleted branches deleted from your upstream remotes. |
| `git-pruneall` | Ryan Tomayko's [dotfiles](https://github.com/rtomayko/dotfiles) | Prune branches from specified remotes, or all remotes when no remote is specified. |
| `git-publish` | Michael Markert's [dotfiles](https://github.com/cofi/dotfiles) | `git publish remote [remote-branch]` |
| `git-purge-from-history` | David Underhill’s blog | Permanently delete files or folders from your git repository. |
| `git-pylint` | Joe Block <jpb@unixorn.net> | Runs pylint on any .py files modified or added in the `git status` output. |
| `git-rank-contributors` | William Morgan <wmorgan-git-wt-add@masanjin.net> | Rummages through the changelog and orders contributors by the size of the diffs they're responsible for. |
| `git-rebase-authors` | Mislav Marohnić's [dotfiles](https://github.com/mislav/dotfiles) | Adds authorship info to interactive `git rebase` output |
| `git-rebase-theirs` | Rodrigo Silva (MestreLion) <linux@rodrigosilva.com> | Resolve rebase conflicts by favoring 'theirs' version. |
| `git-recently-checkedout-branches` | Mislav Marohnić's [dotfiles](https://github.com/mislav/dotfiles) | Shows timestamp and name of recently checked-out branches in reverse chronological order. |
| `git-rel` | Ryan Tomayko's [dotfiles](http://github.com/rtomayko/dotfiles) | Shows the relationship between the current branch and *ref*>*. With no *ref*, the current branch's remote tracking branch is used. |
| `git-related` | Mislav Marohnić's [dotfiles](https://github.com/mislav/dotfiles) | Show other files that often get changed in commits that touch `<file>`. |
| `git-rename-branches` | Rodrigo Silva (MestreLion) <linux@rodrigosilva.com> | Rename multiple branches that start with a given name. |
| `git-reset-with-fire` | Joe Block <jpb@unixorn.net> | Hard reset the working directory, then zap any files not known to git. |
| `git-restore-mtime` | Rodrigo Silva (MestreLion) <linux@rodrigosilva.com> | Change mtime of files based on commit date of last change. |
| `git-rm-deleted-from-repo` | Joe Block <jpb@unixorn.net> | Removes files you deleted with `rm` from the repo for you. |
| `git-root-directory` | Joe Block <jpb@unixorn.net> | Prints the path to the root of the git repository you're in. |
| `git-run-command-on-revisions` | Gary Bernhardt's [dotfiles](https://github.com/garybernhardt/dotfiles) | Runs a given command over a range of Git revisions. |
| `git-shamend` | Danielle Sucher's [git-shamend](http://www.daniellesucher.com/2014/05/08/git-shamend/) blog post | Amends your staged changes as a fixup (keeping the pre-existing commit message) to the specified commit, or HEAD if no revision is specified. |
| `git-show-overwritten` | Mislav Marohnić's [dotfiles](https://github.com/mislav/dotfiles) | Aggregates `git blame` information about the original owners of lines changed or removed in the '<base>...<head>' diff. |
| `git-sp` | A. Schwarz's [git-sp](https://github.com/Schwarzy1/git-sp) | "Simple push", single short command to commit, and push. Use -a flag to add all files to commit. |
| `git-switch` | Andrew Steele's [dotfiles](https://github.com/Andrew565/dotfiles) | Make it easier to switch to a branch by a substring of its name. More useful if you are good about deleting branches which have been merged upstream and if your branch names include unique identifiers like ticket/issue numbers. |
| `git-submodule-rm` | Greg V's [dotfiles](https://github.com/myfreeweb/dotfiles) & [Pascal Sommer](https://github.com/pascal-so/) | Allows you to remove a submodule easily with `git submodule-rm path/to/submodule`. |
| `git-tag-and-sign` | ? | Create and sign a new tag |
| `git-thanks` | Mislav Marohnić's [dotfiles](https://github.com/mislav/dotfiles) | List the contributors to a repository in descending commit order, even if their contribution has been completely replaced. |
| `git-track` | Zach Holman's [dotfiles](https://github.com/holman/dotfiles) | Sets up your branch to track a remote branch. Assumes you mean *origin/localbranchname*. |
| `git-trail` | Christian Neukirchen's [blog](http://chneukirchen.org/blog/archive/2013/01/a-grab-bag-of-git-tricks.html) | Show all branching points in the repo's Git history so you can see how to reach commits in the current branch from other branches. |
| `git-undelete` | ? | Undeletes a file. |
| `git-undo-push` | ? | Undoes your last push to branch **$1** of origin |
| `git-unpushed` | Zach Holman's [dotfiles](https://github.com/holman/dotfiles) | Show the diff of everything you haven't pushed to the origin remote yet |
| `git-unreleased` | Mislav Marohnić's [dotfiles](https://github.com/mislav/dotfiles) | Shows git commits since the last tagged version. |
| `git-up` | Ryan Tomayko's [dotfiles](http://github.com/rtomayko/dotfiles) | |
| `git-upstream-sync` | Joe Block <jpb@unixorn.net> | Fetches *upstream/yourforkname* and rebases it into your local fork, then pushes to your origin remote. |
| `git-what-the-hell-just-happened` | Gary Bernhardt's [dotfiles](https://github.com/garybernhardt/dotfiles/blob/master/bin/git-what-the-hell-just-happened) | Show what just happened. |
| `git-when-merged` | Michael Haggerty [git-when-merged](https://github.com/mhagger/git-when-merged) | Find when a commit was merged into one or more branches. |
| `git-where` | Mislav Marohnić's [dotfiles](https://github.com/mislav/dotfiles) | Shows where a particular commit falls between releases. |
| `git-whoami` | Peter Eisentraut | Shows what username & email you have configured for the repo you're in |
| `git-winner` | Garry Dolley [https://github.com/up_the_irons/git-winner](https://github.com/up_the_irons/git-winner) | Shows what authors have made the most commits, both by number of commits and by number of lines changed. |
| `git-wordiness` | Noel Cower | Shows how wordy people's commit messages are. Useful for shaming the folks who commit atrocities like `git commit -m fixup` |
| `git-wtf` | William Morgan <wmorgan-git-wt-add@masanjin.net> | `git-wtf` displays the state of your repository in a readable, easy-to-scan format. It's useful for getting a summary of how a branch relates to a remote server, and for wrangling many topic branches. |
| `github-open` | Ryan Tomayko's [dotfiles](http://github.com/rtomayko/dotfiles) | |

## Useful git aliases

Here are some helpful aliases for your `~/.gitconfig`

| alias | Description |
| ----- | ----------- |
| `ahead-of-master = log --oneline origin/master..HEAD` | Show commits that haven't made it to master yet. |
| `fetch-pull-requests = fetch origin '+refs/pull/*/head:refs/remotes/origin/pull/*'` | Fetch pull requests from github so you can `git checkout pull/123` and test them locally. |
| `roots = log --all --oneline --decorate --max-parents=0` | Show the root commits. |
| `unpushed = log @{u}..` | Show which commits have not been pushed to the tracking branch and are safe to amend/rebase. |
| `work-in-progress = rebase -i @{u}` | Starts an interactive rebase of all the commits you haven't pushed yet. Handy for collapsing a bunch of work-in-progress snapshots into logical commits before pushing, without having to worry about accidentally squashing a commit someone else has already referred to. |

## Installing

### Pre-requisites

* A relatively recent version of `git`. The version of `git` Apple includes in macOS is very stale. You should really `brew install git` to get the current version if you're on macOS - if not for features, for security updates.
* Python 3+
* Ruby 2.2+

### zgen

If you're using [zgen](https://github.com/tarjoilija/zgen):

1. Add `zgen load unixorn/git-extra-commands` to your `.zshrc` along with your other `zgen load` commands.
2. `zgen reset && zgen save`

### Antigen

If you're using [Antigen](https://github.com/zsh-users/antigen):

1. Add `antigen bundle unixorn/git-extra-commands` to your `.zshrc` where you've listed your other plugins.
2. Close and reopen your Terminal/iTerm window to **refresh context** and use the plugin. Alternatively, you can run `antigen bundle unixorn/git-extra-commands` in a running shell to have `antigen` load the new plugin.

### oh-my-zsh

If you're using [oh-my-zsh](github.com/robbyrussell/oh-my-zsh):

1. In the command line, change to _oh-my-zsh_'s custom plugin directory :

    `cd ~/.oh-my-zsh/custom/plugins/`

2. Clone the repository into a new `git-extra-commands` directory:

    `git clone https://github.com/unixorn/git-extra-commands.git git-extra-commands`

3. Edit your `~/.zshrc` and add `git-extra-commands` – same as clone directory – to the list of plugins to enable:

    `plugins=( ... git-extra-commands )`

4. Then, restart your terminal application to **refresh context** and use the plugin. Alternatively, you can source your current shell configuration:

    `source ~/.zshrc`

### Bash / Manual Installation

Nothing here actually requires you to use ZSH or zgen, that's just a convenient distribution method for anyone using a ZSH framework.

If you aren't using any ZSH frameworks, or if you're using `bash`, `fish` or another shell, do the following steps:

1. `git clone` this repository
2. Add `cloneDirectory/bin` to your `$PATH` in your shell's startup file.

## Other useful git stuff

### Articles / Blog posts / Books

* [awesome-github](https://github.com/fffaraz/awesome-github) - Faraz Fallahi maintains a curated list of Github & Git resources.

* Scott Chacon's [Pro Git](http://git-scm.com/book) book is a great resource for getting more out of `git`.

* Zach Dennis has a great blog post - [A Git Walkthrough](http://www.mutuallyhuman.com/blog/2012/06/22/a-git-walkthrough/) - it's worth reading on it's own, but here are a couple of good sites I found through it:
    * [gitready.com/](http://gitready.com/) is a great reference which has been collecting information and tips for `git` since 2009.
    * [gitimmersion.com/](http://gitimmersion.com/)

* There’s a quick [Introduction to git](https://learnxinyminutes.com/docs/git/) on [learnxinyminutes.com](https://learnxinyminutes.com)

* There's a more detailed `git` tutorial on [learnenough.com](http://www.learnenough.com/git-tutorial)

* Kate Hudson maintains the [git flight rules](https://github.com/k88hudson/git-flight-rules) collection of useful `git` usage tips.

* [git-tips/tips](https://github.com/git-tips/tips) is a collection of git tips.

* Christian Neukirchen wrote a great blog post, [A Grab Bag of Git Tricks](http://chneukirchen.org/blog/archive/2013/01/a-grab-bag-of-git-tricks.html) on `git` that is the source for several scripts in this collection.

* Mislav Marohnić has a good article on git tips on his [blog](http://mislav.net/2010/07/git-tips/). Several of his `git` scripts are in this collection.

* When you manage to get your `git` working directory in a sad state, you can run into the chicken-egg problem where if you just knew what command to `man`, you could dig yourself out of the hole, but if you knew that, you wouldn't be in the bad place anyway. [Oh Shit, Git!](http://ohshitgit.com/) has a collection of bad situations explained in plain English and how to get yourself out of them.

* Tim Green maintains the excellent [Github Cheat Sheet](https://github.com/tiimgreen/github-cheat-sheet) collection of tips and aliases.

* [firstaidgit.io](http://firstaidgit.io/) is a searchable selection of the most frequently asked Git questions

* [Git From the Inside Out](https://maryrosecook.com/blog/post/git-from-the-inside-out) - A good essay that explains how git works, focusing on the graph structure underpinnings of `git` and how they affect its behavior.

* [“Git” it together: Some tips on commit etiquette and best practices for junior developers](https://hackernoon.com/git-it-together-some-tips-on-commit-etiquette-and-best-practices-for-junior-developers-1f147b8dfd56) is a good article explaining some best practices on how to write a _good_ commit message.

* [Git Rebase in Depth](https://git-rebase.io/) is a good tutorial on `git rebase` that covers the common use cases for rebasing.

* [Git Submodules Revisted](https://dev.to/dwd/git-submodules-revisited-1p54) is a good article by Dave Cridland on using submodules in your code.

* [How to Review a Merge Commit](https://haacked.com/archive/2014/02/21/reviewing-merge-commits/) - Good article on dealing with reviewing the changes made during a merge.

* [Top ten pull request review mistakes](https://blog.scottnonnenberg.com/top-ten-pull-request-review-mistakes/) is a great article by Scott Nonnenberg on how to do better code reviews on PRs.

* [A Tidy, Linear Git History](http://www.bitsnbites.eu/a-tidy-linear-git-history/) - Marcus Geelnard wrote a blog post about the value of a linear commit history.

* [More Productive Git](https://increment.com/open-source/more-productive-git/) by James Turnbull is a quick tutorial for beginning `git` users.

* Julia Evans wrote a great blog post about [Git Exercises](https://jvns.ca/blog/2019/08/30/git-exercises--navigate-a-repository/).

* Roger Dudler wrote a good introduction to `git` in his [git, the simple guide](https://rogerdudler.github.io/git-guide/) post.

* Patrick Porto wrote [4 Branching Workflows for git](https://medium.com/@patrickporto/4-branching-workflows-for-git-30d0aaee7bf) which discusses the pros and cons of four of the more popular `git` workflows.

### External Git Utilities

* [bfg repo-cleaner](https://rtyley.github.io/bfg-repo-cleaner/) - Removes large or troublesome blobs like `git filter-branch` does, but faster.
* [bitbucket-git-helpers](https://github.com/unixorn/bitbucket-git-helpers.plugin.zsh) - Helper scripts to allow you to create bitbucket PRs from a shell session.
* [blackbox](https://github.com/StackExchange/blackbox) - Tom Limoncelli open sourced the tool they use at Stack Exchange to use GPG to store secrets in a git repository.
* [branch-manager](https://github.com/elstgav/branch-manager) - ZSH plugin for branch management
* [commit-helper](https://github.com/andre-filho/commit-helper) - A python script that helps you write commits following commit conventions.
* [diff-so-fancy](https://github.com/so-fancy/diff-so-fancy) - Better looking git diffs
* [git-aliases.zsh](https://github.com/peterhurford/git-aliases.zsh) - Peter Hurford's git plugin which you may prefer to the git plugin from oh-my-zsh.
* [git-also](https://github.com/anvaka/git-also) - Shows what files are most often committed with a given file in the repository.
* [git-amend](https://github.com/colinodell/git-amend-old) - Bash script to amend older commits with staged changes.
* [git-branch-status](https://github.com/dmcgowan/git-branch-status) - A git utility to make managing large number of branches either across many remotes easier. Branch status allows comparing all branches against their upstream or any arbitrary branch to show the number of commit differences.
* [git-branches](https://github.com/shurcooL/git-branches) - Prints the commit behind/ahead counts for branches.
* [git-bump](https://github.com/arrdem/git-bump) - Hook scripts to automatically bump the version file in a repository
* [git-chart](https://github.com/flashcode/gitchart) - A python script that builds charts from a git repository
* [git-complete-urls](https://github.com/rapgenic/zsh-git-complete-urls) - ZSH plugin to enhance git completion to include in the remotes completion (e.g. from `git clone`) any URL in the clipboard.
* [git-cop](https://github.com/bkuhlmann/git-cop) - Enforces Git rebase workflow with consistent Git commits for a clean and easy to read/debug project history.
* [git-crypt](https://www.agwa.name/projects/git-crypt/) - Enables transparent encryption and decryption of files in a git repository. Files which you choose to protect are encrypted when committed, and decrypted when checked out.
* [git-deploy-s3](https://github.com/bradt/git-deploy-s3) - Keeps your git repo's assets in sync with Amazon S3.
* [git-diffall](https://github.com/thenigan/git-diffall) - Provides a directory based diff mechanism for git.
* [git-extend](https://github.com/nickolasburr/git-extend) - Extend Git builtins with command wrappers.
* [git-fastclone](https://github.com/square/git-fastclone) - Think `git clone --recursive` on steroids. If you're doing repeated checkouts of a given repo on a machine (like a ci box), **git-fastclone** will speed things up considerably.
* [git-flow-completion](https://github.com/bobthecow/git-flow-completion) - Bash, Fish and Zsh completion support for [git-flow](http://github.com/nvie/gitflow)
* [git-follow](https://github.com/nickolasburr/git-follow) - Follow lifetime changes of a pathspec.
* [git-graph](https://github.com/jerith666/git-graph) - creates a Graphviz graph showing the high-level structure of a repository's history.
* [git-gutter](https://github.com/jisaacks/GitGutter) - Plugin for Sublime Text 2/3 to display the git diff in the edit window gutter.
* [git-it-on.zsh](https://github.com/peterhurford/git-it-on.zsh) - Another plugin by Peter Hurford that adds a gitit command that will open your current directory on github, in your current branch.
* [git-quick-stats](https://github.com/arzzen/git-quick-stats) - A simple and efficient way to access various statistics in git repository.
* [git-repo-updater](https://github.com/earwig/git-repo-updater) - Allows you to easily update multiple git repositories at once.
* [git-secrets](https://github.com/awslabs/git-secrets) - Prevents you from committing secrets and credentials into git repositories.
* [git-standup](https://github.com/kamranahmedse/git-standup) - Recall what you did on the last working day. Can work in a directory full of git repos to see a consolidated view of all work in all the repos.
* [git-stashd](https://github.com/nickolasburr/git-stashd) - Autostashing daemon for dirty worktrees.
* [git-submodule-tools](https://github.com/kollerma/git-submodule-tools) - A collection of scripts that should help make life with git submodules easier.
* [git-sweep](https://github.com/arc90/git-sweep) - A utility script to remove branches that have been merged to master.
* [git-todo](https://github.com/ibolmo/git-todo/blob/master/git-todo) - helper script to show all the todo entries in your repo.
* [git-up (gem)](https://github.com/aanand/git-up) - Fetch and rebase all locally-tracked remote branches.
* [git-up (python)](https://pypi.python.org/pypi/git-up) - Python implementation of Aanand's original ruby gem
* [git-wayback-machine](https://github.com/MadRabbit/git-wayback-machine) - A simple script to quickly navigate a project's state through it's GIT history
* [git_history_visualizer](https://github.com/kidpixo/git_history_visualizer) - python script to visualize the history of files in a git repository
* [gitbaby](https://github.com/lordadamson/gitbaby) - Helper scripts to manage your git repositories
* [gitgo](https://github.com/ltj/gitgo) - Open a GitHub/Gitlab hosted repository in your browser via the command line (macOS only).
* [gitsh](https://github.com/thoughtbot/gitsh) - An interactive shell for git. From within gitsh you can issue any git command, even using your local aliases and configuration.
* [hitch](https://github.com/therubymug/hitch) - Allows developers to be properly credited when Pair Programming and using `git`.
* [hub](https://github.com/github/hub) - A command line tool that wraps git in order to extend it with extra features and commands that make working with GitHub easier.
* [joe](https://github.com/karan/joe) - Generates `.gitignore` files from the command line for you.
* [mergepbx](https://github.com/simonwagner/mergepbx) - Helper script for merging XCode project files.
* [xcode-build-scripts](https://github.com/indirect/xcode-git-build-scripts) - Helper scripts to use with XCode projects

## Miscellaneous Tips

### Rewrite git:// with https://

```sh
git config --global url."https://github".insteadOf git://github
```

### or replace with `ssh`
 Use `ssh` instead of `https://`

 ```sh
 git config --global url."git@github.com:".insteadOf "https://github.com/"
 ```

**Credit:** [@grawity](https://gist.github.com/grawity/4392747) & [@hansdg1](https://github.com/hansdg1) by way of [Kovrinic](https://gist.github.com/Kovrinic/ea5e7123ab5c97d451804ea222ecd78a)

## Contributing

* Please include an entry both in the credits section of README.md for any scripts and a credit comment in the script itself in your PRs so authors get their work credited correctly.
* Please use `#!/usr/bin/env interpreter` instead of a direct path to the interpreter, this makes it easier for people to use more recent versions when the ones packaged with their OS (macOS and CentOS, I'm looking at you!) are stale. -->