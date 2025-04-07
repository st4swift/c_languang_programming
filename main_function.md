## int main() function

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
