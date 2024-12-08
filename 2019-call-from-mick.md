# \[2019] Call from mick

## Introduction

This challenge was part of the KaindorfCTF 2019. It provided a `.pcap` file which can be opened with a tool like Wireshark.

## Approach

Since the challenge is called "Call from mick" I expected it to have something to do with VoiP. After some quick research about the Protocols used I found out that Wireshark has a feature for such analysis:

<figure><img src=".gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

I then clicked on "Play Streams" to see if there is indeed something in this call and what a surprise, I found an audio stream of two people talking about the flag :)

<figure><img src=".gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

```
KDCTF{pr3sid3nt_is_c4lling}
```

> by c0de$t3rn, 2024
