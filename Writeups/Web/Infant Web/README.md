# Infant Web

#### Team: Elmo
#### Category: Web
#### Flag: WH2021{Youre_on_track_for_w3b_greatNess!}

---

### Challenge Description
Today is the day to begin your web security journey!

chals.whitehacks.ctf.sg:50301

I highly encourage you to try this challenge even if you've never done web security before. It is intended for people with zero pre-requisite to web security.

If you're a web security wizard, you can consider passing this challenging on to your teammates.

Note: Hints will be generous for this challenge, feel free to get help from an admin (NOT OTHER TEAMS).

### Challenge

Aight they said ask for help. Lets go ask ~~other team~~ admin for flag.

**10 minutes later**

Admin no give me flag :(( uwu

Opening the challenge site, I was greeted by some basic web theory, and at the end of the page, I was hinted to open the source code.

Opening the source code, I find some commented text

```
                        _   _            _      _                _             
   __ _  ___   ___   __| | | |_   _  ___| | __ | |__   __ _  ___| | _____ _ __ 
  / _` |/ _ \ / _ \ / _` | | | | | |/ __| |/ / | '_ \ / _` |/ __| |/ / _ \ '__|
 | (_| | (_) | (_) | (_| | | | |_| | (__|   <  | | | | (_| | (__|   <  __/ |   
  \__, |\___/ \___/ \__,_| |_|\__,_|\___|_|\_\ |_| |_|\__,_|\___|_|\_\___|_|   
  |___/    
 
```
omo they call me hacker, am i cool now mum _squeals in delight_

Anyways, scrolling down in the source code, I see more **actually useful** commented text
```
 <!--
          TODO: John, once you've completed the web recon page
                at /web-recon-secret-url-31337.html please help
                me to update the href in this element. Thanks :)
        -->
```

Following this, I moved to the recon page by appending /web-recon-secret-url-31337.htm! to the end of the challenge site.

Scrolling to the end once again, I see the following
```
To give you a hint, the path looks like so /s_______.txt, where each underscore corresponds with a letter I've hidden. Once you find this file you'll be lead to the next and final stage. All the best!
```

With some googling, I found this site https://perishablepress.com/all-the-little-txt-files-you-can-put-in-the-root-directory-of-your-website/. Which indicated a common .txt file name being security.txt

With that, I removed the /web-recon-secret-url-31337.html in the web address and appended /security.txt

This brings me to another page which has the following
```
Contact: mailto:goodjob@idiot.sg
Acknowledgments: https://blog.idiot.sg/
Preferred-Languages: en
Policy: http://whateverwebsiteweuse.com/final-section-lets-get-flag-8008.html
```

Following the policy, I append /final-section-lets-get-flag-8008.html to my challenge site. And scrolling all the way down, I see an input field.

Opening the source code once again to read the Javascript code, it shows the following: 
```js
 var password = document.getElementById("passwd").value;
            
            if(password[0] == 'i'){
                if(password[1] == 'd'){
                    if(password[2] == 'i'){
                        if(password[3] == 'o'){
                            if(password[4] == 't'){
                                flag(password);
                                return;
```

Piecing all the letters together, I key in the password as idiot and voila.

```
Congratulations, here is the flag: WH2021{Youre_on_track_for_w3b_greatNess!}
```
