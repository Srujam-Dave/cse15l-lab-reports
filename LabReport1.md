## Lab Report 1

# 1. The cd Command
- No Arguments
```
[user@sahara ~/lecture1/messages]$ cd
[user@sahara ~]$ 
```
Before the commmand was run, the working directory was /lecture1/messages. When the cd command is run with no arguments, it changes the working directory back to the home directory, which is exactly 
what happened. This is not an error. 

- Directory as an Argument
```
[user@sahara ~/lecture1]$ cd messages
[user@sahara ~/lecture1/messages]$ 
```
Before the command was run, the working directory was /lecture1. When the cd command was run, it changed the working directory to /lecture1/messages, since messages is a subdirectory in the lecture1 
directory. This is not an error. 

- File as an argument
```
[user@sahara ~/lecture1/messages]$ cd en-us.txt
bash: cd: en-us.txt: Not a directory
```
Before the command was run, the working directory was /lecture1/messages. When the cd command was run, the line `bash: cd: en-us.txt: Not a directory` was printed to the console, since the cd 
command is meant to take in a directory as an argument, but a file was written instead. This is an error - the cd command is meant to change the working directory, and the idea of changing the 
working directory to a file is nonsensical. 

# 2. The ls command
- No arguments
```
[user@sahara ~/lecture1]$ ls
Hello.java  messages  README
```
The current working directory was /lecture1. The output lists all the files and subdirectories inside of /lecture1, which is expected - without any arguments, the ls command lists all the contents 
of the current working directory. This is not an error. 

- Directory as an Argument
```
[user@sahara ~/lecture1]$ ls messages
en-us.txt  es-mx.txt  zh-cn.txt
```
The current working directory was /lecture1. The output lists all the files and subdirectories inside of /lecture1/messages. This is expected - the ls command lists the contents of the directory 
that is passed as an argument. This is not an error.

- File as an argument
```
[user@sahara ~/lecture1/messages]$ ls en-us.txt
en-us.txt
```

The current working directory was /lecture1/messages. The output is the name of the file that was entered as an argument. The ls command is supposed to behave this way when given a file name as 
input. This is not an error. 

# 3. The cat command
- No arguments
```
[user@sahara ~/lecture1]$ cat
hello world
hello world
^C
```
The current working directory was /lecture1. The cat command initially does not produce any output, but instead waits for more input from the keyboard. It then outputs exactly whatever keyboard 
input was submitted (in this case, the phrase `hello world`). This would have contintued indefinitely, but I exited the program by pressing cntrl C. This isn't an error.

- Directory as an Argument
```
[user@sahara ~/lecture1]$ cat messages
cat: messages: Is a directory
```
The current working directory was /lecture1. The output was a message saying that the command could not run because a directory was submitted as an argument. This gives an error message because the
cat command is not supposed to concatenate the contents of an entire directory, and instead is meant to be used on individual files. 

- File as an Argument

```
[user@sahara ~/lecture1]$ cat Hello.java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);    
    System.out.println(content);
  }
}
```
The current working directory was /lecture1. When the cat command was run with Hello.java as an argument, the contents of Hello.java are printed to the terminal, which is expected behavior from the 
cat command. This is not an error. 
