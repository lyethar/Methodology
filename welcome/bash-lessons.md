# 🐚 Bash Lessons

### Variables

```bash
#!/bin/bash

phrase="Hello to you!"
user=$(whoami) #This will execute the command whoami and put it to a variable
echo $phrase
echo "Hello " $user
```

### Hiding Input from User&#x20;

```
2>/dev/null at the end of hte staement makes it cleaner and hides unnecessary output
```



### Conditionals

When bash scripting, you can use conditionals to control which set of commands within the script run. Use `if` to start the conditional, followed by the condition in square brackets (`[ ]`). Make sure you leave a space between a bracket and the conditional statement! `then` begins the code that will run if the condition is met. `else` begins the code that will run if the condition is not met. Lastly, the conditional is closed with a backwards `if`, `fi`.

A complete conditional in a bash script uses the following syntax:

```
if [ $index -lt 5 ]then  echo $indexelse  echo 5fi









IFS	Description
$#	This variable holds the number of arguments passed to the script.
$@	This variable can be used to retrieve the list of command-line arguments.
$n	Each command-line argument can be selectively retrieved using its position. For example, the first argument is found at $1.
$$	The process ID of the currently executing process.
$?	The exit status of the script. This variable is useful to determine a command's success. The value 0 represents successful execution, while 1 is a result of a failure.
Of the ones shown above, we have 3 such special variables in our if-else condition.

IFS	Description
$#	In this case, we need just one variable that needs to be assigned to the domain variable. This variable is used to specify the target we want to work with. If we provide just an FQDN as the argument, the $# variable will have a value of 1.
$0	This special variable is assigned the name of the executed script, which is then shown in the "Usage:" example.
$1	Separated by a space, the first argument is assigned to that special variable.
```

Bash scripts use a specific list of operators for comparison. Here we used `-lt` which is “less than”. The result of this conditional is that if `$index` is less than 5, it will print to the screen. If it is 5 or greater, “5” will be printed to the screen.

Here is the list of comparison operators for numbers you can use within bash scripts:

* Equal: `-eq`
* Not equal: `-ne`
* Less than or equal: `-le`
* Less than: `-lt`
* Greater than or equal: `-ge`
* Greater than: `-gt`
* Is null: `-z`

When comparing strings, it is best practice to put the variable into quotes (`"`). This prevents errors if the variable is null or contains spaces. The common operators for comparing strings are:

* Equal: `==`
* Not equal: `!=`

For example, to compare if the variables `foo` and `bar` contain the same string:

```bash
if [ "$foo" == "$bar" ]
# Check for given argument
if [ $# -eq 0 ]
then
	echo -e "You need to specify the target domain.\n"
	echo -e "Usage:"
	echo -e "\t$0 <domain>"
	exit 1
else
	domain=$1
fi
```

```bash
#!/bin/bash
first_greeting="Nice to meet you!"
later_greeting="How are you?"
greeting_occasion=1


if [ $greeting_occasion -lt 1 ]
then
  echo $first_greeting
else 
  echo $later_greeting
fi

```

### Loops



There are 3 different ways to loop within a bash script: `for`, `while` and `until`.

A for loop is used to iterate through a list and execute an action at each step. For example, if we had a list of words stored in a variable `paragraph`, we could use the following syntax to print each one:

```
for word in $paragraphdo  echo $worddone



for ip in "10.10.10.170 10.10.10.174 10.10.10.175"
do
	ping -c 1 $ip
done
```

Note that `word` is being “defined” at the top of the for loop so there is no `$` prepended. Remember that we prepend the `$` when accessing the value of the variable. So, when accessing the variable within the `do` block, we use `$word` as usual.

Within bash scripting `until` and `while` are very similar. `while` loops keep looping while the provided condition is true whereas `until` loops loop until the condition is true. Conditions are established the same way as they are within an `if` block, between square brackets. If we want to print the `index` variable as long as it is less than 5, we would use the following `while` loop:

```
while [ $index -lt 5 ]do  echo $index  index=$((index + 1))done
```

Note that arithmetic in bash scripting uses the `$((...))` syntax and within the brackets the variable name is not prepended with a `$`.

The same loop could also be written as an `until` loop as follows:

```
until [ $index -eq 5 ]do  echo $index  index=$((index + 1))done
```

### Input

```
saycolors red green blue

lyethar-1@htb[/htb]$ ./script.sh ARG1 ARG2 ARG3 ... ARG9
       ASSIGNMENTS:       $0      $1   $2   $3 ...   $9
```

Within the script, these are accessed using `$1`, `$2`, etc, where `$1` is the first argument (here, “red”) and so on. Note that these are 1 indexed.

If your script needs to accept an indefinite number of input arguments, you can iterate over them using the `"$@"` syntax. For our `saycolors` example, we could print each color using:

```
for color in "$@"do  echo $colordone
```

Lastly, we can access external files to our script. You can assign a set of files to a variable name using standard bash pattern matching using regular expressions. For example, to get all files in a directory, you can use the `*` character:

```
files=/some/directory/*
```

You can then iterate through each file and do something. Here, lets just print the full path and filename:

```
for file in $filesdo  echo $filedone
```

```
file=/home/ccuser/workspace/learn-bash-scripting-inputs/lol.txt
while read p; do
  echo "$p"
done <lol.txt


#!/bin/bash
first_greeting="Nice to meet you!"
later_greeting="How are you?"
greeting_occasion=0

echo "How many times should I greet?"
read greeting_limit

while [ $greeting_occasion -lt $greeting_limit ]
do
  if [ $greeting_occasion -lt 1 ]
  then
    echo $first_greeting
  else
    echo $later_greeting
  fi
  greeting_occasion=$((greeting_occasion + 1))
done
```

### Functions

```
function name {
	<commands>
}
```
