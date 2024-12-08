# \[2021] Flags 2 - Intermediate

## Introduction

This challenge was part of the KaindorfCTF 2021. It provided a `.gif` file with multiple flags being shown after each other.

## Approach

Because of my basic knowledge in crypto I knew that this was the so-called `# Flag Semaphore`. With this information I would only have to get all the flags in the correct order and use a decoder to get the clear text.

For getting the flags I created following Python Script that seeks every time the gif changes and saves the new frame as a `.png` file.

```python
from PIL import Image

with Image.open('gif.gif') as im:
    for i in range(im.n_frames):
        im.seek(im.n_frames // im.n_frames * i)
        im.save('{}.png'.format(i))
```

With this I got all the flags as `.png` files and I was able to insert them into [dcode.fr](https://www.dcode.fr/maritime-signals-code).

<figure><img src=".gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

This revealed following flag:

```
KDCTF{PEARLHARBOR}
```

but it actually is:

```
KDCTF{pearlharbor}
```

> by c0de$t3rn, 2024
