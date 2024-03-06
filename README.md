

# MAKE
make can be considered the center of the development process by providing a roadmap of an application’s components and how they fit together.

## makefile 📄
makefile contains a set of rules or actions (Goals) used to build an application
**usage**
* default file `make`
* named file `make -f <makefile named>` or `make --file <makefile named>`
* make target `make <Target>`

**make default file name are searched in this hierachy**
* GNUmakefile
* Makefile

**To use multiple makefile, use include directive**
```
include filenames…
```
or to neglect File Not Found error if included file do not exists add -

```
-include filenames…
```
The default search directories are in this order (1) /usr/local/include,  (2) /usr/gnu/include, (3) /usr/local/include, (4) /usr/include.
**To specify the directory the included file is at, use the***
`-I` or `--include-dir` options with make



### ***Goal*** Structure 🔎📄
```
# this is a one goal from the goals in a make file

target ... : prerequisites     -----------------------
  ... recipe                   # all recipe (shell commands and process) are passed to the shell directly
  ... ...                      # so recipe syntax should should follow ✅ shell scripting not  ❌ makefile syntax
```                             

## Make command options

option                               |   Description
-------------------------------------|-------------------------------------
`-f` or  `--file `                   | 
`-t` or `--touch `                   |
`-q` or `--question`                 |
`-n` or `--just-print`               |
`-C dir` or  `--directory=dir`       | Change to directory dir before reading the makefiles
`-d` or `--debug[=options]`          |  Print debugging information in addition to normal processing.
➖                                   |  options `a` all -> all types of debugging output are enabled. This is equivalent to using `-d'.
➖                                   |        `b` basic -> basic Basic debugging prints each target that was found to be out-of-date, and whether the build was successful or not.
➖                                    | `v` verbose -> A level above `basic`; includes messages about which makefiles were parsed, prerequisites that did not need to be rebuilt, etc.
➖                                    | `i` implicit -> Prints messages describing the implicit rule searches for each target. This option also enables `basic' messages.
➖                                    | `j` jobs -> Prints messages giving details on the invocation of specific subcommands.
➖                                    |`m` makefile -> By default, the above messages are not enabled while trying to remake the makefiles. This option enables messages while rebuilding makefiles, too. Note that the `all` option does enable this option. This option also enables `basic' messages.
`-e` or `--environment-overrides` | Give variables taken from the environment precedence over variables from makefiles
`-f file` or  `--file=file` or `--makefile=file` | Read the file named file as a makefile
`-h` or `--help` | Remind you of the options that make understands and then exit.
`-i` or `--ignore-errors`  | Ignore all errors in commands executed to remake files
`-I dir` or `--include-dir=dir` |  Specifies a directory dir to search for included makefiles. If several `-I` options are used to specify several directories, the directories are searched in the order specified.
`-j [jobs]` or `--jobs[=jobs]` | Specifies the number of jobs (commands) to run simultaneously. With no argument, make runs as many jobs simultaneously as possible. If there is more than one `-j` option, the last one is effective
`-k` or `--keep-going`  | Continue as much as possible after an error. While the target that failed, and those that depend on it, cannot be remade, the other prerequisites of these targets can be processed all the same
`-l [load]` or `--load-average[=load]` or  `--max-load[=load]` |  Specifies that no new jobs (commands) should be started if there are other jobs running and the load average is at least load (a floating-point number). With no argument, removes a previous load limit
`-n` or  `--just-print` or `--dry-run` or `--recon` | Print the commands that would be executed, but do not execute them. See section Instead of Executing the Commands.
`-o file` or `--old-file=file` or `--assume-old=file` | Do not remake the file file even if it is older than its prerequisites, and do not remake anything on account of changes in file. Essentially the file is treated as very old and its rules are ignored
`-p` or `--print-data-base` | Print the data base (rules and variable values) that results from reading the makefiles; then execute as usual or as otherwise specified. This also prints the version information given by the `-v` switch. To print the data base without trying to remake any files, use `make -qp`. To print the data base of predefined rules and variables, use `make -p -f /dev/null`. The data base output contains filename and linenumber information for command and variable definitions, so it can be a useful debugging tool in complex environments.
`-q` or `--question` | "Question mode". Do not run any commands, or print anything; just return an exit status that is zero if the specified targets are already up to date, one if any remaking is required, or two if an error is encountered
`-r` or `--no-builtin-rules` | Eliminate use of the built-in implicit rules (see section Using Implicit Rules). You can still define your own by writing pattern rules (see section Defining and Redefining Pattern Rules).Also clears out the default list of suffixes for suffix rules  But you can still define your own suffixes with a rule for `.SUFFIXES`, and then define your own suffix rules. Note that only rules are affected by the `-r `option; default variables remain in effect
`-R` or `--no-builtin-variables` | Eliminate use of the built-in rule-specific variables You can still define your own, of course. The `-R` option also automatically enables the `-r` option, since it doesn't make sense to have implicit rules without any definitions for the variables that they use.
`-s` or `--silent` or `--quiet` | Silent operation; do not print the commands as they are executed. See section Command Echoing
`-S` or `--no-keep-going` or `--stop` | Cancel the effect of the `-k` option. This is never necessary except in a recursive make where `-k` might be inherited from the top-level make via MAKEFLAGS or if you set `-k` in MAKEFLAGS in your environment.
`-t` or `--touch' | Touch files (mark them up to date without really changing them) instead of running their commands. This is used to pretend that the commands were done, in order to fool future invocations of make
`-v` or `--version` | Print the version of the make program plus a copyright, a list of authors, and a notice that there is no warranty; then exit.
`-w` or  `--print-directory` | Print a message containing the working directory both before and after executing the makefile. This may be useful for tracking down errors from complicated nests of recursive make commands. See section Recursive Use of make. (In practice, you rarely need to specify this option since `make` does it for you; see section The `--print-directory` Option.)
`--no-print-directory` | Disable printing of the working directory under -w. This option is useful when -w is turned on automatically, but you do not want to see the extra messages. See section The `--print-directory' Option.
`-W file` or `--what-if=file` or `--new-file=file` or  `--assume-new=file` | Pretend that the target file has just been modified. When used with the `-n` flag, this shows you what would happen if you were to modify that file. Without `-n`, it is almost the same as running a touch command on the given file before running make, except that the modification time is changed only in the imagination of make. See section Instead of Executing the Commands.
`--warn-undefined-variables` | Issue a warning message whenever make sees a reference to an undefined variable. This can be helpful when you are trying to debug makefiles which use variables in complex ways.












## Make Variable

* Declare ->  `var1 = text text text` or   `r = text text text`
*  Assignment
  *  `=` recursively expanded -> value can not be another variable or function call ❌ `var2 = $(var1) text` but  ✅  `var2 = text text`
  *  `:=` simply expanded  ->  value can be another variable or function call ✅  `var2 := $(var1) text` and ✅ `var2 := text text`
  *  `+=` appending assignment -> append the new value to the end of old value `var1 += new value`
  *  `?=`  conditional assignment ->  set to a value to a variable only if variable is not already set `var1 ?= value`
* reference -> `$(var1)  ` or  `${var1}` and `$(r)` or `${r}` or can only be a letter not word if referenced withouth -> {}, () ✅ `$r` but not ❌ `$var1`

## Make Function
* Declare ->  
* reference -> 

## Directive

### Conditional Directive

**make conditional statement**
```
if conditional-directive-one          
text-if-true
else if conditional-directive-two
text--is-true
else
text-if-one-and-two-are-false
endif
```
**if conditional directive Types** 
* `ifeq (arg1, arg2)`  or `ifeq "arg1" "arg2"` -> if arg1 and arg2 are equal
* `ifneq (arg1, arg2)` or `ifneq "arg1" "arg2"` -> if arg1 aand arg2 are not equal
* `ifdef variable-name` -> if variable is defined
* `ifndef variable-name` -> if variable is not defined

#### usage
```
ifeq ($(var1), 1)
  var3 := 1
else ifeq ($(var1),2)
  var3 := 2
else
 var3 := 0
endif
```


### override Directive
```
override variable = value
```
or
```
override variable := value
```
To append more text to a variable defined on the command line, use:
```
override variable += more text
```


Terms        |    Description
-------------|-----------------
\-           | surpress any error `-rm leave.txt` will ignore error if the file do not exists and move to next command
@            | surpress printing recipe statement before executing the recipe which is a default make behaviour.
\#           | comments
\\           | string new line or escape character for special characters like `\#`
Goal         | Complete single make process -> target, prerequisites, recipe
Target       | name of a file that is generated by a program or name of an action to carry out eg name.o,  clean 
prerequisite | required conditions needed to exits, mostly files needed to create the target
recipe       | Actions(shell commands passed by make to the default shell) that make carries out. It more than one command, either on the same line or each on its own line. its starts with tab character at the beginning of every recipe line. **if you wish to change recipe starting character. set `.RECIPEPREFIX` Variable** e.g `.RECIPEPREFIX = >`.
Default Goal | the first goal in the makefile is default. To change default goal. set `.DEFAULT_GOAL` variable like `.DEFAULT_GOAL := <prefered default goal>`


Variables        |  Description
-----------------|------------------ 
`.PHONY`         | This prevents make from getting confused that the target is a process not a file
`.RECIPEPREFIX`  | Character that begings every recipe line. Default is a tab, e.g `.RECIPEPREFIX = >`.
`.DEFAULT_GOAL`  | the first goal in the makefile is default. e.g  `.DEFAULT_GOAL := <prefered default goal>`
`.INCLUDE_DIRS`  |  contain the current list of directories that make will search for included files
`MAKEFILE_LIST`  | Contains the name of each makefile that is parsed by make, in the order in which it was parsed.
`MAKE_RESTARTS`  | This variable is set only if this instance of make has restarted or remade. it will contain the number of times this instance has restarted
`MAKE_TERMOUT`   | Make stdout variable, if populated make sends to stdout
`MAKE_TERMERR`   | Make stderr variable, if populated make sends to stderr
`.VARIABLES`     | Expands to a list of the names of all global variables defined so far.
`.FEATURE`S      | Expands to a list of special features supported by this version of make
`.INCLUDE_DIRS`  | Expands to a list of directories that make searches for included makefiles
`.EXTRA_PREREQS` | Each word in this variable is a new prerequisite which is added to targets for which it is set.
`$@`             | The file name of the target of the rule
`$%`             | The target member name, when the target is an archive member
`$<`             | The name of the first prerequisite
`$^`             | The names of all the prerequisites, with spaces between them.
`$+`             | This is like `$^`, but prerequisites listed more than once are duplicated in the order they were listed in the makefile
`$?`             | The names of all the prerequisites that are newer than the target, with spaces between them
`$\|`            | The names of all the order-only prerequisites, with spaces between them
`$*`             | The stem with which an implicit rule matches 
`$(@D)`          | The directory part of the file name of the target, with the trailing slash removed
`$(@F)`          | The file-within-directory part of the file name of the target.
`$(*D)` or `$(*F)` |  The directory part and the file-within-directory part of the stem; dir and foo in this example.
`$(%D)` or `$(%F)` | The directory part and the file-within-directory part of the target archive member name.
`$(<D)` or `$(<F)` | The directory part and the file-within-directory part of the first prerequisite.
`$(^D)` or `$(^F)` | Lists of the directory parts and the file-within-directory parts of all prerequisites.
`$(+D)` or `$(+F)` | Lists of the directory parts and the file-within-directory parts of all prerequisites, including multiple instances of duplicated prerequisites.
`$(?D)` or `$(?F)` | Lists of the directory parts and the file-within-directory parts of all prerequisites that are newer than the target