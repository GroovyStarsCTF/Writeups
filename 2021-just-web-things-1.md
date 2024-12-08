# \[2021] Just Web Things 1

## Introduction

"Just Web Things 1" is a challenge from the 2021 Kaindorf CTF which provides a website that tells me that I don't seem to have a big brain :(

<figure><img src=".gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

## Approach

While analyzing the cookies of the page I found one called `vibe_check` and that one looked like a JWT (Json Web Token) to me. This is the value of the token:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE3MTg5MDA5ODgsIm5iZiI6MTcxODgxMDk4OCwiaWF0IjoxNzE4ODE0NTg4LCJpc3MiOiJwZXBlIiwiYXVkIjoicGxlYnMiLCJiaWdfYnJhaW4iOmZhbHNlfQ.IGRetMdJX-GFqtXew9eNvmZqSWE7RFxYIEMEQlHlg6I
```

I used "CyberChef" in order to decode the token to find out more about following payload:

```
{
    "exp": 1718900988,
    "nbf": 1718810988,
    "iat": 1718814588,
    "iss": "pepe",
    "aud": "plebs",
    "big_brain": false
}
```

As we can see, there is an attribute called "big\_brain" which I might have to set to true in order to proceed on the page. However, there is an issue with just changing values in a JWT. Normally a token is split into three different parts:

* The Header
  * this includes meta data like the type of topen and the algorithm used for the signature
* The Payload:
  * this includes the JSON payload with the data of the user
* The Signature
  * this is a hash calculated using the other two values and a secret.

Because of the signature you normally would not be able to modify payload. However, there is a misconfiguration that would allow this, therefore I tried it anyways.

I only had to take the first two parts of the token, update them how I want them and then append them using a `.`. The most important change is that you set the algorithm in the header to `none`. It is important to put another dot at the end of the token so the server would know that there are three segments. Using this knowledge I created following new token:

```
eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJleHAiOjE3MTg5MDA5ODgsIm5iZiI6MTcxODgxMDk4OCwiaWF0IjoxNzE4ODE0NTg4LCJpc3MiOiJwZXBlIiwiYXVkIjoicGxlYnMiLCJiaWdfYnJhaW4iOnRydWV9.
```

![](<.gitbook/assets/image (4).png>)

Now I set the cookie with my new token and was able to reach following page:

![](<.gitbook/assets/image (6).png>)

Now we know that the flag of this challenge is:

```
KDCTF{n0ne_al6o_1s_5till_be77er_than_4lgo_fr3ifach}
```
