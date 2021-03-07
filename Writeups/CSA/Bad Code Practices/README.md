# Bad Code Practices

#### Team: Elmo
#### Category: CSA
#### Flag: WH2021{f0r_A_fun_ch@113ng1ng_N_eggc1t!ng_car33r_j0!n_C5@}

---

### Challenge Description
Looking at the codes, it seems that the attacker made multiple commits to hide a secret key.

---
### Solution

So the challenge description hinted us his commits.

Going to his csawebsite repository, we see 6 commits and each one has some minor changes.

By viewing the commits in sequence and seeing the changes in each commit, we have the following

WH2021 9_2_8_5_4_6_3_1_7 _this is probably the base since it holds the start of the flag WH2021_

1. C5@
2. fun
3. f0r

Looking at the base of the flag, it seems like theres some seequence involved. And looking at the changes in each commit, we can figure out that we are probably supposed to fill up their base of the flag with the changes of commits.

However, there are only 3 changes in this repository while there are 9 numbers to replace.

Going back to chachabooboo github profile, we see 3 other repositories. Httrack, Gophish, king-phisher. Hmm seems interesting.

We have a look at httrack first and we see the following `` This branch is even with xroche:master.``. 

That means that chachabooboo probably hasnt made any changes to this repository. Let's move on.

We go to his gophish repository, and we see that there are 3 changes. Let's compare and see what the changes are

![Screenshot 2021-03-07 220203](https://user-images.githubusercontent.com/76640319/110242395-d75ac380-7f90-11eb-99d8-ee07a48f8c58.png)

Once again, in the order of his commits, we have:

1. j0!n
2. A
3. car33r

Next in his king-phisher repository, there are 3 commits again. You know the drill. In the order of his commits, we have:

1. N
2. ch@113ng1ng
3. eggc1t!ng

We have 9 keywords so far. And in our base flag, we have 9 numbers as well. Perfect! Now how do we decide which repository changes come first?

Looking at his profile once again, we look at the sequence of repository commits he made.

First he created httrack, then gophish, king-phisher and lastly csawebsite.

So we can come up with this

1. gophish
2. king-phisher
3. csawebsite

And ranking the changes in each repository, we ultimately have

1. j0!n 
2. A 
3. car33r
4. N
5. ch@113ng1ng
6. eggc1t!ng
7. C5@
8. fun
9. f0r

Replacing each number with the corresponding keyword in the base flag WH2021 9_2_8_5_4_6_3_1_7, we ultimately get the flag!!

```
WH2021{f0r_A_fun_ch@113ng1ng_N_eggc1t!ng_car33r_j0!n_C5@}
```
