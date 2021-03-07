# Piggy Bank

#### Team: Elmo
#### Category: Pwn
#### Flag: WH2021{N0w_the_p1ggy_is_wORS3_than_empty_:'(}

---

### **Challenge Description**

Time to save your angbao money! $_$

nc chals.whitehacks.ctf.sg 20101

Solve this challenge to unlock Piggy_Bank_Revenge!\

[Piggy.zip](https://github.com/caprinux/WhiteHacks-2021-Writeups/files/6097202/Piggy.zip)


---

### Challenge

So for this challenge, we are given the source code as well as the ELF binary file.

Firstly we execute the binary ELF file, and it brings us to a shop where we can buy a flag. 

However, we are not given sufficient funds in our wallet, and the bank does not have much money either.

We are presented with the following options: Deposit, Withdraw, Buy Flag and exit.

Hmmmmmmmmmmmmmmmmm... okay not enough money to buy flag so I guess we can't solve this challenge bye!!

---

### Solution

or so you thought. We have a look at the source code, and the deposit function immediately catches my eye:

```

	printf("How much would you like to DEPOSIT?\n");

	printf("> $");

	scanf("%d", &amount);

	// Check if wallet contains enough

	if(amount * 100 < user_cents){

		// Make deposit if valid value

		user_cents  -= amount * 100;

		piggy_cents += amount * 100;

```

So as long as the amount that we deposit is less than the amount that we have in our wallet, the function passes. 
Wait does that mean I can deposit negative money from the piggy bank owo
Sounds like a smexy endless piggy bank (wished i had one too, mines always empty)

Anyways, we execute the binary file and deposits a negative amount of money.
VOILA! Our wallet now has a few million dollars and we easily purchase the flag.

``WH2021{N0w_the_p1ggy_is_wORS3_than_empty_:'(}``
