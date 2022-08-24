> Copyright (C) 2022 Sandesh Regmi
The permission to modify, delete, copy, merge, publish and use is herbly allowed to any users but they should mention the above copyright line
**Before starting, I hope you guys are clear with the basics of linux otherwise you can't utilize the power of shell script efficiently.**

------------


If you can't understand the definition of shell scripting, take it as the group of linux command which is merged into a file and if it is executed, it means numbers of commands are goint to get executed from the file.

Head over to `/etc/shells` and do `ls` over there, you will see many shells installed in your system. You will see bash shell as well which is one of the most common and used shell in linux. Nowadays, **Z-Shell** which is commonly known as zsh is also gaining popularity. You can install other shell in your linux machine just like you normally install other program using your package manager in linux or if are not able to do so, you can simply google it.

`filename.sh` : "sh" is the extension of a bash shell. Bash is not a programming language rather it is a command line interpreter or scripting language.

`echo $SHELL` : To see the currently logged in shell.

Let's say, I am currently logged in as a zsh shell user in my terminal and I can shift myself to bash by writing 'bash' in your terminal. On the other hand, you can change your shell using `chsh -s /bin/bash` and then switch the user using the command `su - {username}`.


`#!/bin/bash` :  This is called shebang(only #!) and `/bin/bash` is written in order to indicate that we are trying to use bash interpreter. If we are trying to use zsh interpreter, we should mention `/bin/zsh` after shebang.
Make sure to mention the shebang and interpreter at the first line of your script.

## Displaying output in your terminal 

```bash
echo "Hello Sandesh"
echo "Hello I am displaying this " ; echo "In a new line"
```

You will notice that after you wrote `;`, second command is going to be displayed in a new line.

## Running script with executable permission
You create a shell script file with an extension of `sh` at the end and in order to run it, there are several methods. One of the method of doing so is by allowing the executable permission to the script and running it.
You can do so just like:
```bash
chmod +x filename.sh ; ./filename.sh
```

*Note: `..` means parent directory whereas `.` means current directory and we are trying to run `filename.sh` file present in our current directory thus we wrote single dot at the beginning.*

## Running script without providing executable permission
Let's say you had created a file name `a.sh` and you can directly run it using `bash a.sh` or `zsh a.sh` or `ksh a.sh`. This concluded that writing the name of the shell and mentioning the file name will directly run the scripting file and it don't need any exexcutable permission as well but if you are trying to run like `bash a.sh`, make sure to provide the bash interpreter after the **shebang line**.

## Exporting the path and run:
Let's say I have all of my scripts inside `script` directory situated inside `/home/user/Documents/`. So, I can specify the path of my shell script and I can just write `<filename>.sh` instead of giving executable permissions and this is how you can specify the path:

```bash
export PATH:$PATH:/home/user/Documents/script
```

# Variables in shell scripting:


## Declaring variable in bash:

While declaring the variable in bash, it don't care about the datatypes. You can declare the variable in bash as:
Syntax:
```bash
variable_name="value"
```

For an example,
```bash
var='Sandesh'
```

And also, you can use that same variable name to declare the integer or float value but it's value is going to be modified. But, make sure to avoid spaces before and after '=' otherwise it is going to throw you an error. However, spaces are mandatory before and after "=" sign only. On the other hand, don't give spaces while giving the variable name rather use underscore(_).

**unset var**: Dropping it's value 'Sandesh' from the above case
You can delete the value of variable using `unset` keyword. It can not only delete the value of variable, but also can drop the value from an array as well which we are going to later in this course.

## Declaring constant variable:

```bash
readonly b='Sand'
```

Here, in order to declare constant variable, you will need to use readonly keyword
While declaring variable, you can even assign the value of variable to the linux command which is commonly known as command substitution. Just look at the given example and identify it:
```bash
dsk='lsblk'
```

Or you can even do this as well:
```bash
directory=$(pwd cd.. pwd)
```

## Printing variable
Till now so far, we have seen the way of declearing and undeclearing variable. So, let's see how we can print the value of variable:

**Syntax**:

```bash
echo "${variable_name}" or echo "$variable_name"
```

However, if you replace double quotes with single quotes, then you are not going to see the value of variable printed in your terminal but instead you will it's name with $ sign get printed.

## Comments

For comment(Which is the piece of line that is ignored by the interpreter of bash), you use #
> "#" will not be executed as this is comment as I had added "#" at the first 
## User input in bash
```bash
echo "Enter anything and then it will be stored in a variable situated below this line"
read a
echo "You entered $a"
```

Another way of doing so:
```bash
echo -p "Are you fine? Reply me in either yes or no!" mood
```
	   
In the above line, `-p` is used to get user prompt in the same line where it asks for your prompt and to store it in the variable named mood

## Passing multiple value to different variable:

Here is a simple bash program that takes name, surname, age of a person:
```bash
echo "Enter your name, surname, and age:"
read nam thar umer
echo "So, you are $nam $thar who is $umer years of old"
```


## Array in bash:

Basically, array can be defined as the sequence of characters.
```bash
arr=("hello","how","r","are","you")
arr+=("?") #I am appending the value to an array at the end.
echo "array's first element says $arr[0]"
```
In the above array, there is `r`, which is the third element of the array named arr and if we wanna delete it, we use `unset` as discussed above just like:
```bash
unset arr[2]
```

**Usage:**
```bash
unset <array name if you want to drop an array or index of an array>
```
Indexing starts from 0 and if there are n elements in an array, then the last element will have the index of n-1. In the above case, if you want to access first element of array then use arr[0] and if you want to access all the elements of that array then instead of arr[0], you replace it with `arr[*]`, where `*`(a wildcard) in linux stands for all.
To display the number of elements of an array, you need to put `#` before array name and put `@` in the place where you used to put the index number just like
```bash
$#arr[@]
```
 In case of strings, you can get and print the length by
```bash
${#string_variable_name}
```
After assigning value to the variable, you can normally print it out using `echo`.
Some special bash variable:
| command | use |
| --- | --- |
| $0 | name of bash script |
| $n | bash script arguments  {where, n can be any number} | 
| $? | exit status of last executed command |
| $@ | value of all arguments passed to the scripts |
| $$ | process id of the current shell |
| $# | number of arguments passed to the scripts |
## If else or decision making statement in bash:
**Syntax:**
```bash
if [ condition ];
then
  [command]
elif [ condition ]; then
  echo 'Use it only if you need else if'
else
  [command]
fi
```
For an example,
```bash
nam="Sandesh"
if [ ${nam} = "Sand" ]; then
  echo "Hello Sand"
elif [ ${nam} = "Esh" ]; then
  echo "Hello Esh"
else
  echo "Executing else statement"
fi
```
In you are familier with other programming language, then we use `>` or `<` to check whether something is greater or lesser. 
In bash, we use 
| operator | use |
| --- | --- |
|`-lt`| less than |
|`-gt`| greater than |
|`-le`| less than and equal to |
|`-ge`| greater than and equal |
|`-ne`| not equal to |
|`-eq`| equal to |
**Bonus tip:** 
*Might be harder to remember right, you can just write the command `man test` and there is a manual page for you. You don't need to remember any more.*
## Case statement in bash
```bash
echo "Enter your number"
read n
case $n in
  [1-4])
    echo "Lies between 1 to 4"
    ;;
  [5-10])
    echo "Lies between 5 to 10"
    ;;
  *)
  echo "I don't know" ;;
esac
```
## Loop in shell scripting
Basically, loop can be defined as the process of doing something repedeately. 
Let us say you are about to create about 100 users and insert their contact details and insert into the database which is quite time consuming right? What can be the alternative for that? Well, loop is there to help you at such conditions which can do you job within some minutes of count. 
In bash, basically there are three types of loops which are **for** loop, **while** loop and **until** loop. Well, three of them might be sounding a bit confusing right, but don't worry. As you go through the repository, you will find everything easy
**For loop**
 - Runs as long as the condition is true
Syntax:
```bash
for ((initialize ; condition ; increment/decrement )); do 
  echo "$"
done
Here is an example:
for ((i = 0; i < 10; i++)); do
  echo "${i+1}.)Namaste"
done
```
Or, you can specify the specific range as well just like:
```bash
#The following program will list the contents inside the /opt directory
for i in /opt/*; do 
  echo "$i\n\n"
done
```
**While loop**
 - Runs as long as the condition is true
Syntax:
```bash
while [ condition ]; do
  [command]
  increment or decrement[if need else if you want a infinite loop skip this]
done
```
**Until loop**
- Runs as long as the condition becomes false
Syntax:
```bash
until [ condition ]; do
  [command]
  {increment or decrement if need}
done
```
## Functions:
Usually, the idea of function is same as the idea of loop which is to deduct the code reusability but it is a bit different from that of loop.
**Ways of declearing Functions**
 ```bash
function function_name() {
  rest is upon you[Means you need to write script inside that enclosed block]
}
function_name() {
  rest is upon you[Means you need to write script inside that enclosed block]
}
```
**Calling the function:**
```bash
function_name
```
**Note: But while calling the function, you are not allowed to use parenthesis**
I hope that after coming up to this point, you are well familier with bash and now you will be capable of creating your own great bash programs to do your time consuming and boring jobs.
------------
**If you have any comment or question regarding bash, you can simply google it or my twitter account is mentioned in my github profile. You can simply ping me upon there too.**
