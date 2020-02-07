# Shell

  * [Startup Sequence Of Events](#startup-sequence-of-events)
  * [Shell Command Execution](#shell-command-execution)
  * [Shell Command Interpretation](#shell-command-interpretation)
    + [Anatomy of Commands](#anatomy-of-commands)
    + [Fundamental Terminal Commands](#fundamental-terminal-commands)
  * [Structure of Files and Folders Linux and Mac](#structure-of-files-and-folders-linux-and-mac)
  * [Summary](#summary)
  * [Recording iOS Simulator](#recording-ios-simulator)


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


## Structure of Files and Folders Linux and Mac

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
