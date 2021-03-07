# Piggy Bank Revenge
---
### Challenge Description
Seems there was an issue with the previous implementation. I've introduced a HOTFIX that should prevent any further vulnerabilities. I've achieved an unhackable piggy bank now for sure.

nc chals.whitehacks.ctf.sg 20201

This will require a bit more knowledge about programming than Piggy Bank. Give it a try and learn something new(?)

---
### Challenge

Wow... our endless piggy bank was fixed. Back to being broke uwu

But... if there's a will there's a way. 

We try executing the Binary ELF file and it does the exact same thing as before, except it no longer accepts negative values.

We'll see what we can do with this.

---
### Solution

We open up our source code once again and pretty much everything is the same except for the HOTFIX to patch the negative deposit from the previous challenge.

After looking at the code for sometime, the only thing that comes to mind is an **Integer Overflow** attack. 

Essentially, we will try to overflow the number of bytes that the Int() can take and see what magic that does for us.

If you google ``Int max for C`` you will find that the maximum value that Int() can hold is 2147483647.

Looking at the source code for the binary once again, we see that 

``` if(amount * 100 < user_cents) ```

the amount that we want to deposit will be multiplied by 100. 

So perhaps we would want to input a value like 2147483647/100, so something like 21470000. After trying that, I realised it's not enough to overflow yet, so I try increasing the value slightly and tried to input 21480000.

Magically, it worked!! Now we have a few million dollars again and can buy the flag :)

```
WH2021{(Don't)Try_th1s_0n_youR_B4nk!}
```

p.s. when are banks irl gonna implement this feature smh
