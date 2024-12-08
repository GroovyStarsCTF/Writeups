# \[2021] The Room

## Introduction

"The Room" is a challenge in the 2021 KaindorfCTF. It provided me with a maze of nested directories. At the end of a path is always a "dead\_end" file which contains a base64 encoded string.

## Approach

Since I would have never been able to finish looking for the flag myself, I wrote a little python script that would check every file and search for our flag:

```python
import os
import base64
import re

pattern = re.compile('KDCTF{.*}')

def read_files_recursively(dir_path):
    for root, dirs, files in os.walk(dir_path):
        for file in files:
            file_path = os.path.join(root, file)
            with open(file_path, 'r') as f:
                content = f.read()
                try:
                    decoded = base64.b64decode(content).decode()

                    if (pattern.match(decoded)):
                        print(decoded)
                        return

                except:
                    pass

read_files_recursively('./')
```

This resulted in following output:

```
KDCTF{n3v3r_0p3n_7h3_r00m}
```

This is also our flag :)

> c0de$t3rn, 2024
