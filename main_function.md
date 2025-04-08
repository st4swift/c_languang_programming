## int main() function

[What does int argc, char *argv[] mean?](https://stackoverflow.com/questions/3024197/what-does-int-argc-char-argv-mean)


```
int main(void)

int main(int argc, char *argv[])

int main(int argc, char *argv[], char *envp[])
```
Alternatively, you could use:
```
int main(int argc, char** argv)

int main (int argc, char **argv, char **envp)
```

```
#include <stdio.h>
int main(int argc, char *argv[])
{
  while (--argc > 0)
    printf("%s ", argv[argc]);
  printf("\n"); 
}
```
Invoking this program from a command line:
  
     backward string1 string2
   
The arguments argc and argv would contain the following values at the start of the program:
```
Object
Value
argc	3
argv[0]	pointer to string "backward"
argv[1]	pointer to string "string1"
argv[2]	pointer to string "string2"
argv[3]	NULL
```


#### What is the 3rd parameter in the main function, char** envp?

The non-portable-but-not-uncommon third parameter of main — traditionally called envp — points to an array of C-style strings (aka., null-terminated byte strings) that describe the “environment variables” of the process for which the program is run.

As always, I recommend experimenting. Here is a little program that will print out your environment.
```
#include <stdio.h> 
 
int main(int argc, char* argv[], char **envp) { 
  while (*envp != NULL) { 
    printf("%s\n", *envp++); 
  } 
  return 0; 
}
```
I’m not going to quote its actual output in my terminal because that would reveal some personal info, but it looks something like this:
```
$ gcc t.c 
$ ./a.out 
SHELL=/bin/bash 
TERM=xterm-256color 
HISTSIZE=1000 
EDITOR=vim 
LANG=en_US.UTF-8 
HISTCONTROL=ignoredups 
ARCH=x86_64 
DISPLAY=:0 
COLORTERM=truecolor 
...
```
Note that we are not given the length of the array pointed to by envp, unlike the argv parameter (where the length of the array pointed to is provided using a separate argc parameter). Instead, the “end of the array” is indicated by a null pointer entry. (UPDATE: The argv array also has a null pointer at the end. That one is guaranteed by the standard. While it’s not really needed because of the argc count, it’s convenient if you want to use the kind of loop I used for envp above. Thanks to Paul for reminding me of this.)
