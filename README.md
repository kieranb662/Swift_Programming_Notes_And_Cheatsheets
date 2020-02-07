# CheatSheets and Notes

* Swift Markup
* YAML 
* Moustache 
* Shell


# Swift MarkUp 

Not everything is here, I never really found a use for all of it so I just kept the stuff I used frequently.

## Basic Syntax

| Style                 | Syntax                          | Rendered                       |
|-----------------------|---------------------------------|--------------------------------|
| Single Row Comment    | /// Example                     | Example                        |
| Block Comment         | /** <br>Example<br>*/           | Example                        |
| Header(H1)            | \# example                      |                                |
| Header(H2)            | \#\# example                    |                                |
| Italicized            | \*example\*                     | *example*                      |
| Bold                  | \*\*example\*\*                 | **example**                    |
| Unordered List        | \* example                      |                                |
| Ordered List          | 1. example                      |                                |
| Inline Code           | \`var example\`                 | `var example`                  |
| Multi-Line Code Block | \`\`\`<br>var example<br>\`\`\` | ```   var example   ``` |

## Some Delimeters

|            |               |              |
|------------|---------------|--------------|
| Attention  | Invariant     | Since        |
| Author     | Note          | Throws       |
| Authors    | Parameter     | To Do        |
| Bug        | Parameters    | Version      |
| Copyright  | Postcondition | Warning      |
| Complexity | Returns       | Precondition |
| Date       | Requires      | Remark       |
| Important  | See Also      | Images       |


## Generic Example

``` Swift
/**
# Important Function

Example description of a function 
- parameters:
  - first: Description of *first*
  - second: Description of *second*
  
- returns: *third* number 

*/
```

# YAML 

YAML is a simple serialization language that is used by many as a format for configurations files.  YAML uses key-value pairs like JSON.    Comments are written by Prepending a `#` to the comment. 

**Indentation** 

All indentation must be in the form of spaces (**Not** tabs).

**Numeric Values** 

Values that can be recognised come in the form of 
* Integers (decimal, hexidecimal , or octal)
* Floating point
* Scientific Notation (eg. 12.3015e+05)
* Infinity (eg.  .inf)
* Not a Number (.NAN)


**Strings** 

Strings do not need to be wrapped in double quotes unless you wish to have escaped sequences handled. 

Multiline strings can be converted to single lines by using the `>` character in the first line of the value 
````
bar: >
this is not a normal string it
spans more than
one line
see?
````
To keep the lines formatted as is use the `|` operator 
````
bar: |
this is not a normal string it
spans more than
one line
see?
````

**Nulls**

Use either `~` or the unquoted word `null`

**Booleans**

True can be written in the following ways: 
* True 
* On 
* Yes 

False can be written in the following ways 
* False 
* Off
* No

**Arrays** 

Arrays in YAML can be represented in either brackets `[...]` or in the multiline format 
````
items:
  - 1 
  - 2 
  - 3
  - 4 
  - 5 
names:
  - "one"
  - "two"
  - "three"
  - "four"
  ````
  
**Dictionaries** 
  
Similar to arrays, dictionaries can come in a single line format `{...}` or in the multiline form.
  ````
  foo:
  bar:
    - bar
    - rab
    - plop
    
````

**Anchors**

If values are to be referenced or used multiple times, anchors can be used to reduce copy/pasting long entries multiple times.  Here is an example from the spec website link. 
```
hr:
  - Mark McGwire
  # Following node labeled SS
  - &SS Sammy Sosa
rbi:
  - *SS # Subsequent occurrence
  - Ken Griffey
```

**References** 
* YAML Spec - https://yaml.org/spec/1.2/spec.html
* Info on the `<<` - https://stackoverflow.com/questions/41063361/what-is-the-double-left-arrow-syntax-in-yaml-called-and-wheres-it-specced


# .moustache

The mustache file format is used to create "Logic-less templates" for various file types. There are no if statements, else statements, or for loops. The only component found within them is the **tags** . 

**Variables** 

`{{variable}}` is a tag whose key(variable) will be searched for in the current context. 

for unescaped HTML use `{{{variable}}}` or  `{{& variable}}`

**Sections** 

A section begins with a `{{#variable}}` and ends with a `{{/variable}}`.  Behavior of the section is determined by the value of the key. 

* For false or empty values - The section is not rendered. 
* For non-empty lists - the value in the section will be rendered once for each item in the list. 
* lambdas - if the section value is a callable function, should handle its own creation of the block. 
* Non-False values - renders the block with the value once 

**Inverted Sections**

A section begins with a `{{^variable}}` and ends with a `{{/variable}}`.  Behavior of the section is determined by the value of the key. In this case text will be rendered if the value of the key doesnt exist, is false or is an empty list. 

**Comments** 

Written in the form `{{! variable}}`.  These values will never be rendered. 

**Partials** 

Written in the form `{{> variable}}`. Used for referencing other mustache files to be nested within the current file.


**References** 

* Mustache Manual - https://mustache.github.io/mustache.5.html

# Shell

## Startup Sequence Of Events

**Definitions**
* `getty` - program which determines the baud rate, displays the message `login:`, and waits for someone to type
* `passwd` - file containing one line for each user of the system. Example entry `pat:*:99:7::/users/pat:/usr/bin/ksh`.

 Specifies:
  * login name
  * home directory
  * program to startup when user logs in.


* `shadow` - Storage for encrypted user passwords. Not readable by normal users.

1. Unix System Kernel program `init` automatically starts up a `getty` program on each terminal port whenever system is allowing users to log in.
2. User types in characters followed by pressing Enter
3. Getty program disappears after starting and passing the input characters to the process `login`
4. `login` displays the string `Password:` and waits for input
5. `login` verifies user/password against the entries in /etc/passwd
6. If no startup program is specified the standard shell is run by default.

## Shell Command Execution

**Definitions**
* process - when the kernel copies a specific program into memory and begins execution. This copied program is the process.

1. When shell starts up, it displays a command prompt and waits for user input.
2. Each time you type in a command and press enter, shell analyzes the line and carries out the request.
3. If asked to execute a specific program, shell searches the disk for the name of the program.
4. When found shell asks the kernel to initiate the programs execution
5. Shell "goes to sleep" until the program is finished.
6. If program writes to standard output then it will appear in the terminal unless redirected. Programs that read standard input, will wait for you to type input unless redirected from a file or piped to another command.
7. Once finished execution control returns to shell.

## Shell Command Interpretation

**Definitions**
* Command Line - The line typed into the shell.

Shell uses whitespace characters to determine where the program name starts and ends, and where each argument starts and ends.

1. Shell scans the command line and considers everything from the start of the line to the first whitespace as the name of the program to execute.
2. Shell scans for and substitutes variables and filenames when a special character is found. Also shell looks for redirection and pipe characters and performs operations accordingly.
3. The set of characters up to the next whitespace is the first argument.
4. then continues this process for proceeding arguments.

*Note* - Multiple whitespace characters are ignored by the shell.

### Anatomy of Commands

Command (-option) (something)

### Fundamental Terminal Commands

`whoami` - Tells you who you are logged in as.
`pwd` - Tells you the present working directory.
`ls` - Lists all files/folders in the present directory
`ls -a` - Lists all files/folders including hidden files.
`echo` - prints a string.
`killall` - kills the process specified.
`echo -n "String"` - prints String in the next line before the username.


## Structure of Files and Folders Linux/Mac

  1. Every file or directory belongs to some user.
  2. Users are grouped into groups.
  3. groups can be assigned to a file.
  4. Files can be Readable, Writable or Executable.

## Summary

**Commands**

Commands have the form `command arguments`

Multiple commands can be typed on the same line by separating them with a semicolon(;).

Every command that gets executed returns a number known as the `exit status`. Zero means success and nonzero means failure.

The pipe symbol `|` redirects the standard output from one command to the standard input of another

placing a `!` at the beginning of the pipeline will cause the exit status of the pipeline to be the logical negation of the last command.

If the command sequence is terminated by an ampersand(&), it is run asynchronously in the background.

Typing of a command can continue to the next line if the last character is the backslash(`\`)

`&&` between two commands causes the second command to be executed only if the first was successful

`||` between two commands causes the second to execute only if the first has a nonzero exit status

**Comments**

If a word begins with the character `#` the rest of the line is considered to be a comment and shell ignores it.

**Variables**

A shell variable name must start with an alphabetic or underscore character and can be followed by any number of alphanumeric or underscore characters.

Values can be assigned to each variable by using the syntax:
`variable=value variable=value ...`

*Note* - Filename substitution is not performed on value

**Positional Parameters**

When a shell program is executed, the name of the program is assigned to the variable `$0`. The arguments are assigned to `$1`, `$2`, ... .

Parameters greater than 9 must be enclosed in brackets `${10}`

**Special Parameters**

* `$#` - The number of arguments passed; or the number of parameters set by executing the set statement
* `$*` - Collectivelly references all positional parameters as `$1, $2, ...`
* `$@` - Same as `$*` except when double quoted `"$@"` collectively references all positional parameters as `"$1", "$2", ...`
* `$$` - The process id number of the program being executed
* `$!` - The process id number of the last program sent to the background for execution.
* `$?` - The exit status of the last command not executed in the background
* `$-` - The current option flags in effect

**Built In Variables**
* CDPATH - The directories to be searched whenever cd is executed without a full path as argument
* ENV - The name of the file that the shell executes in the current environment when started interactively.
* FCEDIT - The editor used by fc. If not set, ed is used.
* HISTFILE - If set, it specifies a file to be used to store the command history. If not set, or if file isnt writable, $HOME/.sh_history is used.
* HISTSIZE - If set, specifies the number of previously entered commands accessible for editing. default is 128
* HOME - The users home directory, the directory that cd changes to when no argument is supplied.


## Recording iOS Simulator 

```Shell
# 1. Boot up the iPhones to be tested

# This pulls from the list of simulators the one that matches "iPhone Xʀ" and then outputs the udid using a regex
udid=`xcrun simctl list | grep "iPhone Xʀ" | grep -E -o -i "([0-9a-f]{8}-([0-9a-f]{4}-){3}[0-9a-f]{12})"`
# boot the device using the UDID
xcrun simctl boot $udid

#  2. Run the tests and record the video
# Note - must be in directory of the .xcodeproj file

# Run the test to be recorded.
xcodebuild test -project gitlab-ui-test.xcodeproj -scheme ui -destination 'platform=iOS Simulator,name=iPhone Xʀ,OS=12.4' &
# Start the video recording of the device
xcrun simctl io booted recordVideo Xr-Gitlab-UI-Test.mp4
# Shutdown the currently running simulator(s)
xcrun simctl shutdown booted


# Multiple at once
xcrun simctl list devices | grep "iPhone" | while read line ; do echo $line ; done


# correct regular expression for pulling iPhone names.
xcrun simctl list devices | grep "iPhone" | egrep -o "^[^(]+"
```

