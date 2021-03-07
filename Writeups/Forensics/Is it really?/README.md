# Is it really?
---

### Challenge Description
A malicious file was downloaded and picked up by our antivirus...

[signup.pdf](https://github.com/caprinux/WhiteHacks-2021-Writeups/files/6097179/signup.pdf)

---
### Solution

This challenge was pretty straightforward.

In this challenge, I used ``Binwalk``.

Binwalk is a tool for searching a given binary image for embedded files and executable code. Specifically, it is designed for identifying files and code embedded inside of firmware images. 

```
sudo apt-get install binwalk
```

With binwalk, we can analyse our pdf file.

```
$ binwalk signup.pdf
```

Output:
```
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PDF document, version: "1.3"
69            0x45            Zip archive data, at least v2.0 to extract, uncompressed size: 68, name: eicar.txt
226           0xE2            Zip archive data, at least v2.0 to extract, uncompressed size: 332, name: __MACOSX/._eicar.txt
687           0x2AF           End of Zip archive, footer length: 22
443555        0x6C4A3         End of Zip archive, footer length: 22
```

As you can see, it consists of eicar.txt and __MACOSX/._eicar.txt.

Since the challenge only asks us for the name of the malicious file, we submit the name of the file as the flag and voila!!

```
WH2021{eicar.txt}
```
