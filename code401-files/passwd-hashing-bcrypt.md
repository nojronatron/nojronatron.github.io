# Reading Notes Class 14

[Intro to password hashing](https://auth0.com/blog/hashing-passwords-one-way-road-to-security/)

[bcrypt overview](https://danboterhoven.medium.com/why-you-should-use-bcrypt-to-hash-passwords-af330100b861)

[jBCrypt (the paragraphs and code example at the top of the page)](https://www.mindrot.org/projects/jBCrypt/)

## Password Hashing

Authentication: Verifiy the identity of a person/user or service.

Usually a username + password combination or other "who I am and what I have" combination.

Storing passwords is a security risk so must be managed carefully:

- Cleartext: Any program can read this format. Can be easily viewed and should not be used.  
- Plain Text: Unformatted text e.g. text in a plain text *.txt file.
- Plaintext: Input to a cryptographic algorithm.

### Hashing

- A one-way operation (or very difficult to reverse).
- Using an algorithm, calculate a value for a cleartext input so it cannot be read directly nor can it be directly reverse-engineered.
- Usually outputs a fixed-length string representation of the input.

Plaintext => Hashing Algorithm => Hashed text

### Algorithms

MDx (Message Digest) algorithms like MD5.

SHA (Secure Hash Algorithms) like SHA-1, SHA-2, and SHA-256.

Using a hashing algorithm usually involves importing the package, instantiating an object from the class, updating the object with the plaintext, and finally executing a method that produces the hashed text.

A same-sized hashed text will always be produced.

One-way hashing algorithms are known as "one way functions".

One-way Hashing Algo's must not reveal the "pre-image" of the hash text, meaning input values should not be discoverable just by looking at the output, whether the hashing algorithm is known or not.

A handy analogy is the Modulus function: `5 % 3 = 2` but so does `10 % 4 = 2` => The input value(s) are not revealed!

Avalanche Effect: A small change in an input produces a big difference in the output.

### Other Hashing Functions

Producing a CRC: In this case, the idea is to hash the datagram and send the hashed DG along with (or following) the DG's network packet, so the receiving node can compare the CRC to the DG they received.

CRC Hashing is not cryptographically secure, and could be reverse engineered.


## BCrypt Overview

## jBCrypt

Paragraphs and code example.

## Footer

Back to root [readme](../README.html)
