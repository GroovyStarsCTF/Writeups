# \[2021] Obfuskierung Oida

## Introduction

This challenge provided a file called `challenge.ws`. According to the title I expected some sort of obfuscation in the code. The provided code looked like this:

```
'use strict';

HACKL AMOI WOS haudiummideppata (text, schlissl) {
    OIDA schlissllaenge WENNST MANST schlissl.length;

    DRAH DI HAM Array.prototype.slice.call(text).map(HACKL AMOI WOS (c, index) {
                    DRAH DI HAM String.fromCharCode(c.charCodeAt(0) ^ schlissl[index % schlissllaenge].charCodeAt(0));
                }).join('');
}

FIX OIDA dieKrone = require("readline");
FIX OIDA leser WENNST MANST dieKrone.createInterface({
    input: process.stdin,
    output: process.stdout
});

FIX OIDA schlissl WENNST MANST "leberkaskropfnvombilla";


leser.question("Ruck aus des Passwort du wappla: ", HACKL AMOI WOS(password) {
    OIDA zwischndrinn WENNST MANST haudiummideppata(password, schlissl);

    OIDA zwischnspeicher WENNST MANST Buffer.from(zwischndrinn);
    OIDA deskummtausa WENNST MANST zwischnspeicher.toString('base64');   

    WOS WÜSTN(deskummtausa DES GEHT SI SCHO AUS "JyEhMTQQJUAYLV4DOQ8pCQFWDjMDUAhRHw=="){
        I MAN JA NUR("Leiwand oida, des Passwort is die gschissene Flag!")
        leser.close();
    }A SCHO WUASCHT	 {
        I MAN JA NUR("Jetzt muast mit mir auf a Eitrige mit an Buckel, deppata. Dei Passwort woah foisch.")
    }
});

leser.on("close", HACKL AMOI WOS() {
    I MAN JA NUR("\nPfiati!");
    DES IS MA ECHT Z'DEPPAT(0);
});
```

## Approach

Because of the `use strict` I instantly recognized that this had to be `Javascript` code, therefore I began to translate this code in order to make it more readable. There were multiple spots in the code in which you could guess what their translation meant. Here is a quick translation table:

| WS                      | JS          |
| ----------------------- | ----------- |
| HACKL AMOI WOS          | function    |
| FIX OIDA                | const       |
| WENNST MANST            | =           |
| DRAH DI HAM             | return      |
| OIDA                    | let         |
| WOS WÜSTN               | if          |
| A SCHO WUASCHT          | else        |
| I MAN JA NUR            | console.log |
| DES IS MA ECHT Z'DEPPAT | exit        |
| DES GEHT SI SCHO AUS    | ==          |

Using this table I was able to refactor the code to the following `Javascript` code:

```js
'use strict';

function haudiummideppata(text, schlissl) {
    let schlissllaenge = schlissl.length;

    return Array.prototype.slice.call(text).map(function (c, index) {
        return String.fromCharCode(c.charCodeAt(0) ^ schlissl[index % schlissllaenge].charCodeAt(0));
    }).join('');
}

const dieKrone = require("readline");
const leser = dieKrone.createInterface({
    input: process.stdin,
    output: process.stdout
});

const schlissl = "leberkaskropfnvombilla";


leser.question("Ruck aus des Passwort du wappla: ", function (password) {
    let zwischndrinn = haudiummideppata(password, schlissl);

    let zwischnspeicher = Buffer.from(zwischndrinn);
    let deskummtausa = zwischnspeicher.toString('base64');

    if (deskummtausa == "JyEhMTQQJUAYLV4DOQ8pCQFWDjMDUAhRHw==") {
        console.log("Leiwand let, des Passwort is die gschissene Flag!")
        leser.close();
    } else {
        console.log("Jetzt muast mit mir auf a Eitrige mit an Buckel, deppata. Dei Passwort woah foisch.")
    }
});

leser.on("close", function () {
    console.log("\nPfiati!");
    exit(0);
});

```

Now it was easier to analyze the behavior of this program. Let me break it down for you:

The program reads a password from the the STDIN and XORs it with the key `leberkaskropfnvombilla`. The result of this will be encoded in Base64 and is expected to equal `JyEhMTQQJUAYLV4DOQ8pCQFWDjMDUAhRHw==`. The console logs revealed that the correct password is also the flag of the challenge.

In order to gather the flag I would only have to take the expected Base64 output (`JyEhMTQQJUAYLV4DOQ8pCQFWDjMDUAhRHw==`), decode it and XOR the result with `leberkaskropfnvombilla`. I did this using Cyberchef:&#x20;

<figure><img src=".gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

As we all can see, this resulted in the following flag:

```
KDCTF{D3s_1s_a_fl4g_o1d4}
```

> by c0de$t3rn
