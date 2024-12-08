# \[2021] New Game!

## Introduction

This challenge provided a whole episode of the anime "New Game!" as a .mkv file. It was part of the Kaindorf CTF and includes a flag with the `KDCTF{...}` format.

<figure><img src=".gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

## Approach

The first idea I got for this challenge was to have a look at the subtitles of the video because I did not expect any sort of hint in the video itself. I used following `ffmpeg` command to extract the subtitles to a new file:

```bash
ffmpeg -i ./New_Game.mkv subtitles.srt
```

This created the `subtitles.srt` file including all the subtitles from the video. After looking through the file a bit and searching for some sort of flag, I found following suspicious line:

```
<font face="Open Sans Semibold" size="36"><b><i>_</i></b></font>
```

As we can see this was only a single underscore symbol as the subtitle and so I supposed that the flag was hidden in such single character subtitles. Therefore I used the `grep` command to look exactly for this:

<figure><img src=".gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

And as we can see right here we found something that looks just like the flag we were looking for. I then edited this output in order to get the correct flag:

```
KDCTF{cu73_61rl5_d01n6_64m3_d3v}
```

> by c0de$t3rn, 2024
