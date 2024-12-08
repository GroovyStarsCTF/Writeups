# \[2018] Very Secret

## Introduction

"Very Secret" is a challenge played during the KaindorfCTF 2018. It provided the player with a `.pcap` file.

## Approach

The first thing I did was opening the file in Wireshark in order to analyze the packets.

![](<.gitbook/assets/image (10).png>)

As the image shows the vast majority of packets are `FTP` packets. This is why I expected some sort of file being sent over the network. I used the `ftp-data` filter to find such files.

I followed the `TCP` Stream (`Right Click` > `Follow` > `Follow TCP Stream`) in order to gain access to following `FTP` payload:

```
PKƐJL$ flag.txtUT

�&Z�&Z�&Zux���vqq�NM4��O�7.�7,���G��rqPKnc:$PKƐJLnc:$ ��flag.txtUT

�&Z�&Z�&Zux��PKVr
```

After some research I found out that this seems to be a `.zip` file. Therefore I copied this payload, created a `folder.zip` file with is as the content. After unzipping this file I found a `flag.txt` file which included following flag:

```
KDCTF{ea5y_do3s_1t___ea5y_do3s_1t}
```

> c0de$t3rn, 2024
