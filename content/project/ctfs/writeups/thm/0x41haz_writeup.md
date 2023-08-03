# 0x41haz
## Simple Reversing Challenge
### Task 1: Find the password! 
> In this challenge, you are asked to solve a simple reversing solution. Download and analyze the binary to discover the password.
> 
> There may be anti-reversing measures in place!

After downloading the attached task file, we can start analyzing it.

 To discover what type of file we are dealing with we run *file* command followed by the name of the file.
 
```
$ file 0x41haz.0x41haz                                                                                            
0x41haz.0x41haz: ELF 64-bit MSB *unknown arch 0x3e00* (SYSV)
```

We discovered that this is a ELF 64bit executable file type but it seems that there are some obfuscation technique in place:
\
 **MSB *unknown arch 0x3e00* (SYSV)**
 
 Googling it we can find that to bypass this we can patch the sixth byte from 0x02 to 0x01.
 To perform this we can use *hexedit* to change the specific byte.
 
 After changing the sixth byte we get the following:
 ```
0x41haz.0x41haz: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), 
dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2,
BuildID[sha1]=6c9f2e85b64d4f12b91136ffb8e4c038f1dc6dcd,
for GNU/Linux 3.2.0, stripped
 ```
 
 It's time to analyze the file with Ghidra and see what we can discover.
 Looking at the functions we discover the below decoded function.
 ```
 undefined8 FUN_00101165(void)

{
  size_t sVar1;
  char local_48 [42];
  undefined8 local_1e;
  undefined4 local_16;
  undefined2 local_12;
  int local_10;
  int local_c;
  
  local_1e = 0x6667243532404032;
  local_16 = 0x40265473;
  local_12 = 0x4c;
  puts("=======================\nHey , Can You Crackme ?\n=======================");
  puts("It\'s jus a simple binary \n");
  puts("Tell Me the Password :");
  gets(local_48);
  sVar1 = strlen(local_48);
  local_10 = (int)sVar1;
  if ((int)sVar1 != 0xd) {
    puts("Is it correct , I don\'t think so.");
                    /* WARNING: Subroutine does not return */
    exit(0);
  }
  local_c = 0;
  while( true ) {
    if (0xc < local_c) {
      puts("Well Done !!");
      return 0;
    }
    if (*(char *)((long)&local_1e + (long)local_c) != local_48[local_c]) break;
    local_c = local_c + 1;
  }
  puts("Nope");
                    /* WARNING: Subroutine does not return */
  exit(0);
}
```

We found some hex strings, lets decode them using *xxd*:
```
echo 0x6667243532404032 | xxd -r
echo 0x40265473 | xxd -r
echo 0x4c | xxd -r
```
local_1e = 0x6667243532404032; -> fg$52@@2\
local_16 = 0x40265473; -> @&Ts\
local_12 = 0x4c; ->  L

concatenate them and try the resulting string as input for the password.

**fg$52@@2@&TsL**

![try1](https://user-images.githubusercontent.com/70201797/166164363-b1d60e03-e187-4707-aa20-52f152000e16.png)

Let's reverse the hex strings to follow the little-endian format and try again. 
```
echo 0x6667243532404032 | xxd -r | rev
echo 0x40265473 | xxd -r | rev
echo 0x4c | xxd -r | rev
```
**2@@25$gfsT&@L**

![try2](https://user-images.githubusercontent.com/70201797/166164391-0a17a6f0-ccf9-4ecd-8fe2-d77fd71628b4.png)

**Hurray!**

[Heartstone back to home](https://matteogreek.github.io)
