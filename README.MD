# Password Cracking Lab (Demo)

Author: Mickeal Colley  
Date: 2025-10-24

This repository demonstrates an offline password-cracking workflow using John the Ripper in a safe, reproducible environment. A disposable demo account and locally-generated hash were used—no real system credentials are included.

Quick reproduction (one-liners):
```bash
echo "password1" > /tmp/my-small-wordlist.txt
HASH=$(openssl passwd -1 password1)
echo "fakeuser:x:1001:1001:Fake User:/home/fakeuser:/bin/bash" > /tmp/passwd.fake
echo "fakeuser:$HASH:18000:0:99999:7:::" > /tmp/shadow.fake
sudo unshadow /tmp/passwd.fake /tmp/shadow.fake > /tmp/unshadow_fake.txt
john --wordlist=/tmp/my-small-wordlist.txt --pot=/tmp/john_fake.pot /tmp/unshadow_fake.txt
john --show --pot=/tmp/john_fake.pot /tmp/unshadow_fake.txt

