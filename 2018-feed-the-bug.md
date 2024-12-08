# \[2018] Feed the Bug

## Introduction

"Feed the Bug" was a reversing challenge in the 2018 KaindorfCTF providing a file called "feedthebug.exe".

## Approach

Since it was a reversing challenge the first thing to do was to actually revere the binary. I used the tool "Ghidra" for this. After opening the file in the tool I was able to rename several things and filter following code:

```c
do {
    _puts(" \\__/ ");
    _puts(" (OO) ");
    _puts("//||\\\\ ");
    _puts("What to feed the bug?");
    _scanf("%s",input);
    _puts("Feeding the Bug!");
    _Sleep@4(2000);
    inputLength = _strlen(input);
    sum = 0;
    local_1c = "";
    for (i = 0; i < (int)inputLength; i = i + 1) {
      sum = sum + input[i];
    }
    if (sum < 1337) {
      local_1c = "That\'s all?";
    }
    else if ((sum < 1338) || (2337 < sum)) {
      if (sum == 2338) {
        local_1c = "That was just right! Here:";
        local_11 = '\x01';
      }
      else if (0x922 < sum) {
        local_1c = "I can\'t eat that much...";
      }
    }
    else {
      local_1c = "Yummy, I want more!!!";
    }
    _puts(local_1c);
  } while (local_11 == '\0');
  _SetConsoleTextAttribute@8(local_28,10);
  for (i2 = 0; i2 < 0x1d; i2 = i2 + 1) {
    _putchar(local_a0[i2] / 13);
  }
```

Here is what the binary does:

The binary takes an input over the STDIN stream and sums up the ASCII values of the code. Based on the sum of the input there is a different output. The reversing showed that a sum of **2338** is required to achieve the output with the flag.

I used this number to calculated the correct payload using an ASCII table. Some dividing later I came up with following payload:

```
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA?
```

(65 \* 35 + 64)

Now i only had to insert this payload into the program in order to access the hidden flag:

![](<.gitbook/assets/image (9).png>)

As the output already shows, the flag is:

```
KDCTF{G0rd0n_R4ms4y_appr0ve5}
```

> by c0de$t3rn, 2024
