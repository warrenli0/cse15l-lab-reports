cd:
1. With no arguments:
```
[user@sahara ~]$ cd
[user@sahara ~]$
```
I got a blank output (nothing happened) since `cd` with no argument just leaves you in the same directory. This is not an error. <br>
2. With a path to a directory as an argument:
```
[user@sahara ~]$ cd lecture1
[user@sahara ~/lecture1]$
```
You can see that the working directory changed because `cd` moved me to the `lecture` directory. This is not an error.

3. With a path to a file as an argument:
```
[user@sahara ~/lecture1]$ cd Hello.java
bash: cd: Hello.java: Not a directory
[user@sahara ~/lecture1]$
```
The output is an error statement because you can't `cd` into a file.

ls:
1. With no arguments:
```
[user@sahara ~]$ ls
lecture1
[user@sahara ~]$
```
The output is all the subdirectories and files in the current directory. This is not an error.

2. With a path to a directory as an argument:
```
[user@sahara ~]$ ls lecture1
Hello.class  Hello.java  messages  README
[user@sahara ~]$
```
The output is all the subdirectories and files in the `lecture1` directory since the argument indicates that it should run the command in that directory. This is not an error.

3. With a path to a file as an argument:
```
[user@sahara ~/lecture1]$ ls Hello.java
Hello.java
[user@sahara ~/lecture1]$
```
The output this time is simply the file name because the only file in the path of the file is that file. This is not an error.

cat:
1. With no arguments:
```
[user@sahara ~/lecture1]$ cat
Some input
Some input
^C
[user@sahara ~/lecture1]$
```
With no argument, the `cat` argument simply defaults to `stdin`. When I entered "Some input" it just returned that back to me. This is not an error.

2. With a path to a directory as an argument:
```
[user@sahara ~]$ cat lecture1
cat: lecture1: Is a directory
[user@sahara ~]$ 
```
The output is an error telling me that `lecture1` is a directory, which `cat` can't be used on.

3. With a path to a file as an argument:
```[user@sahara ~/lecture1]$ cat Hello.java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class Hello {
  public static void main(String[] args) throws IOException {
    String content = Files.readString(Path.of(args[0]), StandardCharsets.UTF_8);    
    System.out.println(content);
  }
}[user@sahara ~/lecture1]$
```
The output is simply the contents of the `Hello.java` file which is the intended behavior of `cat` when used on a file. This is not an error.
