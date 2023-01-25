# 🐍 Python Lessons

### Color Guide

Obviously the most important part, lol.&#x20;

Paste this into your script.

```python
from colorama import init, Fore, Back, Style

# essential for Windows environment
init()
# all available foreground colors
FORES = [ Fore.BLACK, Fore.RED, Fore.GREEN, Fore.YELLOW, Fore.BLUE, Fore.MAGENTA, Fore.CYAN, Fore.WHITE ]
# all available background colors
BACKS = [ Back.BLACK, Back.RED, Back.GREEN, Back.YELLOW, Back.BLUE, Back.MAGENTA, Back.CYAN, Back.WHITE ]
# brightness values
BRIGHTNESS = [ Style.DIM, Style.NORMAL, Style.BRIGHT ]
```

Then this defines a new print function that you can specify colors.&#x20;

```python
def print_with_color(s, color=Fore.WHITE, brightness=Style.NORMAL, **kwargs):
    """Utility function wrapping the regular `print()` function 
    but with colors and brightness"""
    print(f"{brightness}{color}{s}{Style.RESET_ALL}", **kwargs)
```

Then we can simply specify our text to be printed in whatever color we want like this.&#x20;

```python
age, last_name = 19, "Crespo"


print_with_color(last_name, color=Fore.RED, brightness=Style.BRIGHT) 
```

This will print out my name in red.&#x20;

### Python Syntax

Python can be run with the following style `#!/bin/python3.`

Python syntax is governed by indentation.

Basically only indentation that matters is spaces below and above each line of code.

![](../../.gitbook/assets/2022-08-27\_21-26.png)

Notice how as long as we indent things within a function, we should keep them indented the same unless we want to specify something else.

### Variables & Data Types&#x20;

There  are multiple ways of declaring data types.&#x20;

```
name = "Fabian" 
year = 2003
age, last_name = 19, "Crespo"
```

Notice that in we can simply declare them individually, while the other we could declare multiple varliables in a single line.&#x20;

### User Input

![](../../.gitbook/assets/2022-08-27\_22-42.png)

### SYS

This allows us to pass arguments from the command line.&#x20;

```
import sys

print(sys.argv)
if len(sys.argv) != 3:
    print("Please enter ip and port to run {}")
    sys.exit(5)
ip = sys.argv[1]
port = sys.argv[2]


print("{} {}".format(ip,port))

sys.exit(0)
```

Notice how many different things could be done in order to pass arguments within the command line, this could also be a good lesson to input -h and different commands to our script.&#x20;

### SubProcess&#x20;

#### subprocess.run()

The method `subprocess.run()` will take a list of strings as a positional argument. This is mandatory as it has the bash command and arguments for it. The first item in the list is the command name and the remaining items are the arguments to the command.

Let’s see a quick example.

```python
import subprocess
subprocess.run(["ls"])
```

The above script list all the items in the current working directory as the script lies. There are no arguments to the command in the above script. We have given only the bash command. We can provide additional arguments to the `ls` command like `-l`, `-a`, `-la`, etc.

Let’s see a quick example with command arguments.

```python
import subprocess
subprocess.run(["ls", "-la"])
```

The above command displays all the files including hidden files along with the permissions. We have provided the argument `la` which displays files and directories extra information and hidden files.

We may end up making some mistakes while writing the commands. Errors will raise according to the mistakes. What if you want to capture them and use them later? Yeah, we can do that using the keyword argument **stderr**.

Let’s see an example.

```python
import subprocess
result = subprocess.run(["cat", "sample.txt"], stderr=subprocess.PIPE, text=True)
print(result.stderr)
```



Make sure you don’t have the file with the name **sample.txt** in the working directory. The value to the keyword argument **stderr** is **PIPE** which helps to return the error in an object. We can access it later with the same name. And the keyword argument **text** helps to tell that the output should be a string.

Similarly, we can capture the output of the command using the **stdout** keyword argument.

```python
import subprocess
result = subprocess.run(["echo", "Hello, World!"], stdout=subprocess.PIPE, stderr=subprocess.PIPE, text=True)
print(result.stdout)
```

#### subprocess.Popen()

The class **subprocess.Popen()** is advanced than the method **subprocess.run()**. It gives us more options to execute the commands. We will create an instance of the **subprocess.Popen()** and use it for various things like knowing the status of the command execution, getting output, giving input, etc..,

There are several methods of the class **subprocess.Popen()** that we need to know. Let’s see them one by one along with the code examples.

```python
import subprocess
process = subprocess.Popen(["ls", "-la"])
process.wait()

print("Completed!")
```

If you see the output for the above code, then you will realize that `wait` is actually working. The print statement is executed after the completion of the command execution.

### Executing Bash Scripts

We have seen two ways to execute the commands. Now, let’s see how to execute the bash scripts in Python scripts.

The **subprocess** has a method called **call**. This method is used to execute the bash scripts. The method returns the exit code from the bash script. The default exit code for the bash scripts is **0**. Let’s see an example.

Create a bash script with the name practice.sh as follows.

```bash
#!/bin/bash

echo "Hello, World!"
exit 1
```

Now, write a Python script execute the above bash script.

```python
import subprocess
exit_code = subprocess.call('./practice.sh')
print(exit_code)
```

#### subprocess.run() – input

You can give input to the commands using the **input** keyword argument. We will give inputs in a string format. So, we need to set the keyword argument **text** to `True`. By default, it takes it in bytes.

Let’s look at an example.

```python
import subprocess
subprocess.run(["python3", "add.py"], text=True, input="2 3")
```

In the above program, the Python script **add.py** will take two numbers as input. We have given the input to the Python script using the **input** keyword argument.

#### Combining Variables&#x20;

So if i want the python script to run different commands or scripts i can make them assign an environmental variable.&#x20;

![](../../.gitbook/assets/2022-08-27\_23-01.png)

This can then be put into a script that will export these vraibles to run other binaries that i want.

I can also create a bash script that reads the ip and echoes it as the env variable and later on unsets it.

```
unset var_name
```

So basically a bash script that does the above. Prompts the user for the IP address and later on sets the IP as an enviromental variable and passes it on to lets say dirsearch.

We also gotta make sure that in python we must pass the bash command "source ./script.sh" if we are gonna do this before doing so.

![](../../.gitbook/assets/2022-08-27\_23-17.png)
