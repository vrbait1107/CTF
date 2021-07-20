# Linux Function Hooking

<br/>


```

### Task 1: Introduction 

```
1. I am ready to learn!

Ans: No Answer Needed

```
### Task 2: What are Shared Libraries? 

```
1. What is the name of the dynamic linker/loader on linux?

Ans: ld.so, ld-linux.so

```

### Task 3: Getting A Tad Bit Technical 

```
1. What environment variable let's you load your own shared library before all others? 
Ans: LD_PRELOAD

2. Which file contains a whitespace-separated list of ELF shared objects to be loaded before running a program?
Ans. /etc/ld.so.preload

3. If both the environment variable and the file are employed, the libraries specified by which would be loaded first?
Ans: Environment Variable

```

### Task 4: Putting On Our Coding Hats 
```
1. How many arguments does write() take? 
Ans: 3

2. Which feature test macro must be defined in order to obtain the  definitions  of RTLD_NEXT from <dlfcn.h>? 
Ans: _GNU_SOURCE

```

### Task 5:  Let's Gooooooooo 

```
1.  When compiling our code to produce a Shared Object, which flag is used to create position independent code?
Ans: -fPIC

2. Can hooking libc functions affect the behavior of Python3? (Yay/Nay)
Ans: Yay

```

### Task 6: Hiding Files From ls 

```
1. There are two mandatory fields of a dirent structure. One is d_name, and the other one is?
Ans: d_ino

2. I have read and understood how I can hide files using shared objects!
Ans: No Anwers Needed.

```

### Task 7:  Conclusion 
1. Hooray! You made it to the end! 
Ans: No Answers needed.

```


```


