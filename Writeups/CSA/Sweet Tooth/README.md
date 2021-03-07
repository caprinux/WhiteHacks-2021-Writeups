# Sweet Tooth
### Team: Elmo
#### Category: CSA
#### Flag: WH2021{chachabooboo}
---

### Challenge Description
Help! There's an attacker who wants to use [CSA's website](https://www.csa.gov.sg/) for phishing! He had to copy CSA's web codes somewhere!

Find out who is the attacker.

P.S. We heard rumours that the attacker have some liking for Singaporean desserts

---

### Challenge

Someone copied CSA's web codes. Hm. Sounds like a Ctrl-A Ctrl-C Ctrl-V job, _(wait a min. how did I know? maybe i was the one who phished it hmm)_

Anyways CSA's Workshop for WhiteHacks Day 1 was on GITHUB OSINT. Maybe the codes are in GITHUB. 

Actually, WhiteHacks also released a hint on their website for some time that hinted to search github but I think it was taken down.

No matter the case, github is the most likely place to dump a huge chunk of code so let's look into it!

---

### Solution

There are 2 ways we can find this attacker who phished the CSA website code. 

Just go to https://github.com/search/advanced and search https://www.csa.gov.sg OR you can just search WH2021 as well since it's the start of the flag.

Either ways, if you go to the Code section of the search results, you will find many code with CSA.gov.sg or WH2021.

Going back to the clue, ``the attacker loves desserts``, we scroll through the list and we find someone named chachabooboo, which is the inverse for booboochacha, a famous Singaporean dessert.

![download](https://user-images.githubusercontent.com/76640319/110242029-02441800-7f8f-11eb-85e2-e0e7b7fc2a65.jpg)

### YUM. 

Anyways, going through his account, we see a whole repository with csa.gov.sg web codes.

He is

### **IT**.

```
WH2021{chachabooboo}
``` 
https://github.com/chachabooboo/csawebsite
