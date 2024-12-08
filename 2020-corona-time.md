# \[2020] Corona Time

## Introduction

"Corona Time" is a challenge of the 2020 KaindorfCTF. It provided me with following image of some sort of encoded message:

<img src=".gitbook/assets/image (2).png" alt="" data-size="original">

## Approach

Due to my major knowledge in "Protein Biosynthesis" I instantly knew how to solve this challenge. The only tool we need to solve this challenge is the so called "RNA codon table" which looks like this:

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption><p>RNA codon table</p></figcaption></figure>



> source: https://de.wikipedia.org/wiki/Code-Sonne#/media/Datei:Aminoacids\_table.svg

As we can see from this image, a combination of three bases would result in a certain amino acid. You might have already realized, that the table only includes the letters "A", "U", "C" and "G" while the encrypted code includes "T". To understand this we have to get a bit deeper into the topic "DNA". In our DNA we can find following base pairs:

* A (Adenine) - T (Thymine)
* C (Cytosine) - G (Guanine)

During the process of "Protein Biosynthesis" the DNA is being split up and the creation of the "mRNA" begins. However, instead of T (Thymine) the mRNA includes U (Uracil). So in order to decode this using our sun above, we have to replace each "T" with "U".

```
UGU -> C
CAG -> Q
CGG -> R
CAG -> Q
AAC -> N
GCU -> A
UAA -> .
ACU -> T
AUC -> I
AUG -> M
GAA -> E
UAG -> .
CGA ->R
CAG ->Q
UGU ->C
AAA ->K
UCA ->S
```

Now we have the string "CQRQNA.TIME.RQCKS". Now we only have to add our flag format and we found ourselves a flag:

```
KDCTF{CQRQNA.TIME.RQCKS}
```

