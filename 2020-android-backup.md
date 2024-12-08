# \[2020] Android Backup

## Introduction

This challenge provided a file called `backup.ab` which seems to be a backup of an Android mobile device. The description of the challenge stated that I would have to add the `KDCTF{}` part of the flag myself, therefore I would not have to look for it in the results.

## Approach

Because I could not do anything with the file directly, I was looking for a way to extract this backup into something more useful. During my research I came across a StackOverflow thread recommending this command:

```bash
( printf "\x1f\x8b\x08\x00\x00\x00\x00\x00" ; tail -c +25 backup.ab ) |  tar xfvz -
```

Source: https://stackoverflow.com/questions/18533567/how-to-extract-or-unpack-an-ab-file-android-backup-file

I used this command on my backup file which resulted in a new directory called `apps`. I found following sub directories in this directory:

<figure><img src=".gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

From an earlier lesson about `Forensics` I remembered that the browser history would not be encrypted and can be easily read from a backup. This is why I checked out this first. There I found following `.db` files:

<figure><img src=".gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

I used my `SQLite Viewer` extension in VSCode to view the contents of the database:

<figure><img src=".gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

I found following entries in the `searches` table and especially the one with `andr0id_b4ckup5_ar3_nic3` was very interesting because it looked just like a flag. I tried inserting it in the `KDCTF{}` and it was actually the fitting flag. Therefore the correct flag was:

```
KDCTF{andr0id_b4ckup5_ar3_nic3}
```

> by c0de$t3rn, 2024
