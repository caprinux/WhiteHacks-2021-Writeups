# Secure Banking

#### Team: Elmo
#### Category: Crypto
#### Flag: WH2021{$m00000n3y_g0_Burrrrrrrrrrrrrrr}

---

### Challenge Description
Your friend Peter has built a new online transaction and banking service called AAA Banking. He claims it is extremely secure, using SHA256 hashing to create and verify HMACs. To get you onto the platform, he has sent you $20 for free! Try it out now! Check out the platform!

You are given the following details:

Details: ZnJvbT1QZXRlciZhbW91bnQ9MjA=

Verification Hash: 24a2efde8a32e7046aaeb11eb32a37ecf49937ef84c7a6b4bd943556fd2369cd

However, as a White Hacker, you are obviously sceptical of such a [website](http://chals.whitehacks.ctf.sg:9111/index.php).

Knowing that your friend is also an Admin and has over millions of dollars, can you get him to send you a million dollars as Admin?

Note: You DO NOT need any form of brute force or directory busting to complete this challenge!

---
### Challenge 

Ah more money again? owo

Anyways, going to the website provided and keying the provided details and verification hash, it said 

```
$20 from Peter has been approved! Hope you enjoyed using AAA banking services
```

... I just checked my PayNow but the 20$ not there... skem.

---
### Solution

Before we go on to the attack, the ``Details: ZnJvbT1QZXRlciZhbW91bnQ9MjA=`` definitely looks like base 64 encoded text. 

Using cyberchef, we can decode it and see how the data is sent. ``from=Peter&amount=20``

Anyways, the website also included the following text:
```
Using state of the art SHA256 encryption and an unguessable 19 character secret key, we promise our bank will never get hacked

```
```
How it works?
Decode the given string to obtain transaction details
Check the SHA256(secret + decoded_string) against given hash
Once checked to be same, increase safety by adding slashes
to characters that need to be escaped in decoded string
Parse the string to obtain the details within the safe string
```
Since there is a secret key of length 19, and seeing how it works, I can be pretty sure that this is [HMAC](https://www.youtube.com/watch?v=wlSG3pEiQdc&ab_channel=Computerphile) that is broken by a hash extension attack.

This calls for my handy tool, the [Hash_Extender](https://github.com/iagox86/hash_extender), my every so trusty right-hand man.

If you don't have it, you can get it by 
```
git clone https://github.com/iagox86/hash_extender
cd hash_extender
make
```

The rough idea of how this hash extender work is that I want to make it so that the details read by the system will be something like from=Admin&amount=1000000.

So to do this, I will append the data to the back of my details, and I will also generate the new verification hash, aka the Signature.

With the hash extender tool, I input the following arguments

```
$ ./hash_extender --secret 19 --append '&from=Admin&amount=1000000' --signature '24a2efde8a32e7046aaeb11eb32a37ecf49937ef84c7a6b4bd943556fd2369cd' --data 'from=Peter&amount=20'
```

output: 
```
Type: sha256
Secret length: 19
New signature: 3ac04e9e4a435072edf4961702a6eddb9cf52a3387019006119d05af98a17ebc
New string: 66726f6d3d506574657226616d6f756e743d3230800000000000000000000000000000000000000000000001382666726f6d3d41646d696e26616d6f756e743d31303030303030
```

The string and signature will be printed in hex by default. Hence when we return this to the bank system, we want to convert the new string from hex to bytes and bytes to ascii.

This can be easily done with [CyberChef](https://gchq.github.io/CyberChef/)

![Screenshot 2021-03-07 222807](https://user-images.githubusercontent.com/76640319/110243229-746b2b80-7f94-11eb-92a2-aa4c6f2a670a.png)

Hence we now have

Details: ZnJvbT1QZXRlciZhbW91bnQ9MjCAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAE4JmZyb209QWRtaW4mYW1vdW50PTEwMDAwMDA=
Signature: 3ac04e9e4a435072edf4961702a6eddb9cf52a3387019006119d05af98a17ebc

Sending this back to the banking system prints the flag for us

```
Congrats! Heres your flag!

WH2021{$m00000n3y_g0_Burrrrrrrrrrrrrrr}
```
<details> 
  <summary>Indeed </summary>
   money go burrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrr
</details>


