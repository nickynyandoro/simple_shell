<h1>ALX Simple Shell Team Project</h1>                                                                                        
                                                                                                                              
This is an ALX collaboration project on Shell. We were tasked to create a simple shell that mimics the Bash shell. The name of
 our shell is <b>hsh</b>.                                                                                                     
                                                                                                                              
<h2>Project was done using</h2>                                                                                               
<ul>                                                                                                                          
<li>C language</li>                                                                                                           
<li>Shell</li>                                                                                                                
<li>Betty linter</li>                                                                                                         
</ul>                                                                                                                         
                                                                                                                              
<h2>Description</h2>                                                                                                          
hsh is a simple UNIX command language interpreter that reads commands from either a file or standard input and executes them. 
                                                                                                                              
<h2>How hsh works</h2>
                                                                                                        
1. Prints a prompt and waits for a command from the user                                                                         

2. Creates a child process in which the command is checked                                                                       

3. Checks for built-ins, aliases in the PATH, and local executable programs                                                      

4. The child process is replaced by the command, which accepts arguments                                                         

5. When the command is done, the program returns to the parent process and prints the prompt                                     

6. The program is ready to receive a new command                                                                                 

7. To exit: press Ctrl-D or enter "exit" (with or without a status)                                                              

8. Works also in non interactive mode                                                                                            
                                                                                                                              
<h2>Invocation</h2>                                                                                                           
Usage: hsh [filename]                                                                                                         
                                                                                                                              
To invoke hsh, compile all .c files in the repository and run the resulting executable.                                       
                                                                                                                              
hsh can be invoked both interactively and non-interactively. If hsh is invoked with standard input not connected to a terminal
, it reads and executes received commands in order.                                                                           
                                                                                                                              
Example:

$ echo "echo 'hello'" | ./hsh                                                                                                 
'hello'                                                                                                                       
$                                                                                                                             
If hsh is invoked with standard input connected to a terminal (determined by isatty(3)), an interactive shell is opened. When 
executing interactively, hsh displays the prompt $ when it is ready to read a command.                                        
                                                                                                                              
Example:                                                                                                                      
                                                                                                                              
$./hsh                                                                                                                        
$                                                                                                                             
Alternatively, if command line arguments are supplied upon invocation, hsh treats the first argument as a file from which to r
ead commands. The supplied file should contain one command per line. hsh runs each of the commands contained in the file in or
der before exiting.                                                                                                           
                                                                                                                              
Example:                                                                                                                      
                                                                                                                              
$ cat test                                                                                                                    
echo 'hello'                                                                                                                  
$ ./hsh test                                                                                                                  
'hello'                                                                                                                       
$                                                                                                                             
                                                                                                                              
<h2>Environment</h2>                                                                                                          
Upon invocation, hsh receives and copies the environment of the parent process in which it was executed. This environment is a
n array of name-value strings describing variables in the format NAME=VALUE. A few key environmental variables are:           
                                                                                                                              
<h2></h2>                                                                                                                     
                                                                                                                              
$ echo "echo $HOME" | ./hsh                                                                                                   
/home/projects                                                                                                                
                                                                                                                              
PWD                                                                                                                           
The current working directory as set by the cd command.                                                                       
                                                                                                                              
$ echo "echo $PWD" | ./hsh                                                                                                    
/home/projects/alx/simple_shell                                                                                               
OLDPWD                                                                                                                        
The previous working directory as set by the cd command.

$ echo "echo $OLDPWD" | ./hsh                                                                                                 
/home/projects/alx/printf                                                                                                     
PATH                                                                                                                          
A colon-separated list of directories in which the shell looks for commands. A null directory name in the path (represented by
 any of two adjacent colons, an initial colon, or a trailing colon) indicates the current directory.                          
                                                                                                                              
$ echo "echo $PATH" | ./hsh                                                                                                   
/home/projects/.cargo/bin:/home/projects/.local/bin:/home/projects/.rbenv/plugins/ruby-build/bin:/home/projects/.rbenv/shims:/
home/proj
                                                                              
<h2>Command Execution</h2>                                                                                                    
After receiving a command, hsh tokenizes it into words using " " as a delimiter. The first word is considered the command and 
all remaining words are considered arguments to that command. hsh then proceeds with the following actions:                   
                                                                                                                              
1. If the first character of the command is neither a slash (\) nor dot (.), the shell searches for it in the list of shell bu
iltins. If there exists a builtin by that name, the builtin is invoked.                                                       
2. If the first character of the command is none of a slash (\), dot (.), nor builtin, hsh searches each element of the PATH e
nvironmental variable for a directory containing an executable file by that name.                                             
3. If the first character of the command is a slash (\) or dot (.) or either of the above searches was successful, the shell e
xecutes the named program with any remaining given arguments in a separate execution environment.                             
                                                                                                                              
Exit Status                                                                                                                   
hsh returns the exit status of the last command executed, with zero indicating success and non-zero indicating failure.       
                                                                                                                              
If a command is not found, the return status is 127; if a command is found but is not executable, the return status is 126.   
                                                                                                                              
All builtins return zero on success and one or two on incorrect usage (indicated by a corresponding error message).           
                                                                                                                              
Signals                                                                                                                       
While running in interactive mode, hsh ignores the keyboard input Ctrl+c. Alternatively, an input of end-of-file (Ctrl+d) will
 exit the program.                                                                                                            
                                                                                                                              
User hits Ctrl+d in the third line.

$ ./hsh                                                                                                                       
$ ^C                                                                                                                          
$ ^C                                                                                                                          
$                                                                                                                             
<h2>Variable Replacement</h2>                                                                                                          
hsh interprets the $ character for variable replacement.                                                                      
                                                                                                                              
$ENV_VARIABLE                                                                                                                 
ENV_VARIABLE is substituted with its value.                                                                                   
                                                                                                                              
Example:                                                                                                                      
                                                                                                                              
$ echo "echo $PWD" | ./hsh                                                                                                    
/home/projects/alx/simple_shell
                                                                                               
$?
                                                                                                                            
? is substitued with the return value of the last program executed.                                                           
                                                                                                                              
Example:                                                                                                                      
                                                                                                                              
$ echo "echo $?" | ./hsh                                                                                                      
0                                                                                                                             
$$                                                                                                                            
The second $ is substitued with the current process ID.                                                                       
                                                                                                                              
Example:                                                                                                                      
                                                                                                                              
$ echo "echo $$" | ./hsh                                                                                                      
6494                                                                                                                          

Comments 
                                                                                                                     
hsh ignores all words and characters preceeded by a # character on a line.                                                    
                                                                                                                              
Example:                                                                                                                      
                                                                                                                              
$ echo "echo 'hello' #this will be ignored!" | ./hsh                                                                          
'hello'                                                                                                                       

Operators
                                                                                                                     
hsh specially interprets the following operator characters:

; - Command separator                                                                                                         
Commands separated by a ; are executed sequentially.                                                                          
                                                                                                                              
Example:                                                                                                                      
                                                                                                                              
$ echo "echo 'hello' ; echo 'world'" | ./hsh                                                                                  
'hello'                                                                                                                       
'world'    
                                                                                                                   
&& - AND logical operator
                                                                                                     
command1 && command2: command2 is executed if, and only if, command1 returns an exit status of zero.                          
                                                                                                                              
Example:                                                                                                                      
                                                                                                                              
$ echo "error! && echo 'hello'" | ./hsh                                                                                       
./hsh: 1: error!: not found                                                                                                   
$ echo "echo 'all good' && echo 'hello'" | ./hsh                                                                              
'all good'                                                                                                                    
'hello'   
                                                                                                                    
|| - OR logical operator                                                                                                      
command1 || command2: command2 is executed if, and only if, command1 returns a non-zero exit status.                          
                                                                                                                              
Example:                                                                                                                      
                                                                                                                              
$ echo "error! || echo 'but still runs'" | ./hsh                                                                              
./hsh: 1: error!: not found                                                                                                   
'but still runs'                                                                                                              
The operators && and || have equal precedence, followed by ;.                                                                 
                                                                                                                              
<b>hsh Builtin Commands </b>                                                                                                         

cd                                                                                                                            

Usage: cd [DIRECTORY]                                                                                                         

Changes the current directory of the process to DIRECTORY.                                                                    

If no argument is given, the command is interpreted as cd $HOME.                                                              

If the argument - is given, the command is interpreted as cd $OLDPWD and the pathname of the new working directory is printed 
to standad output.

If the argument, -- is given, the command is interpreted as cd $OLDPWD but the pathname of the new working directory is not pr
inted.                                                                                                                        

The environment variables PWD and OLDPWD are updated after a change of directory.                                             
Example:                                                                                                                      
                                                                                                                              
$ ./hsh                                                                                                                       
$ pwd                                                                                                                         
/home/projects/alx/simple_shell                                                                                               
$ cd ../                                                                                                                      
$ pwd                                                                                                                         
/home/projects/alx                                                                                                            
$ cd -                                                                                                                        
$ pwd                                                                                                                         
/home/projects/alx/simple_shell                                                                                               

alias                                                                                                                         

Usage: alias [NAME[='VALUE'] ...]                                                                                             

Handles aliases.                                                                                                              

alias: Prints a list of all aliases, one per line, in the form NAME='VALUE'.                                                  


alias NAME [NAME2 ...]: Prints the aliases NAME, NAME2, etc. one per line, in the form NAME='VALUE'.                          

alias NAME='VALUE' [...]: Defines an alias for each NAME whose VALUE is given. If name is already an alias, its value is repla
ced with VALUE.                                                                                                               
Example:                                                                                                                      
                                                                                                                              
$ ./hsh                                                                                                                       
$ alias show=ls                                                                                                               
$ show                                                                                                                        
AUTHORS            builtins_help_2.c  errors.c         linkedlist.c        shell.h       test                                 
README.md          env_builtins.c     getline.c        locate.c            hsh                                                
alias_builtins.c   environ.c          helper.c         main.c              split.c                                            
builtin.c          err_msgs1.c        helpers_2.c      man_1_simple_shell  str_funcs1.c                                       
builtins_help_1.c  err_msgs2.c        input_helpers.c  proc_file_comm.c    str_funcs2.c                                       

exit                                                                                                                          

Usage: exit [STATUS]                                                                                                          

Exits the shell.                                                                                                              

The STATUS argument is the integer used to exit the shell.                                                                    

If no argument is given, the command is interpreted as exit 0.                                                                

Example:                                                                                                                      
                                                                                                                              
$ ./hsh                                                                                                                       
$ exit                                                                                                                        

env

Usage: env                                                                                                                    

Prints the current environment.                                                                                               

Example:                                                                                                                      
                                                                                                                              
$ ./hsh                                                                                                                       
$ env                                                                                                                         
NVM_DIR=/home/projects/.nvm                                                                                                   
...                                                                                                                           

setenv                                                                                                                        

Usage: setenv [VARIABLE] [VALUE]                                                                                              

Initializes a new environment variable, or modifies an existing one.                                                          

Upon failure, prints a message to stderr.                                                                                     

Example:                                                                                                                      
                                                                                                                              
$ ./hsh                                                                                                                       
$ setenv NAME Poppy                                                                                                           
$ echo $NAME                                                                                                                  
Poppy                                                                                                                         

unsetenv                                                                                                                      

Usage: unsetenv [VARIABLE]                                                                                                    

Removes an environmental variable.                                                                                            

Upon failure, prints a message to stderr.                                                                                     

Example:                                                                                                                      
                                                                                                                              
$ ./hsh                                                                                                                       
$ setenv NAME Poppy                                                                                                           
$ unsetenv NAME                                                                                                               
$ echo $NAME                                                                                                                  
                                                                                                                              
$                                                                                                                             

<h2>What we learned: </h2>
                                                 
1. How a shell works and finds commands                                                                                          

2. Creating, forking and working with processes                                                                                  

3. Executing a program from another program                                                                                      

4. Handling dynamic memory allocation in a large program                                                                         

5. Pair programming and team work

6. Building a test suite to check our own code                                                                                   
                                                                                                                              
<h2>Authors</h2>                                                                                                              
                                                                                                                              
Nicky
