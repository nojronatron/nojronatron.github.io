# Reading Notes Class 14

[Intro to password hashing](https://auth0.com/blog/hashing-passwords-one-way-road-to-security/)

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

### One Way Hashing

One-way hashing algorithms are known as "one way functions".

One-way Hashing Algo's must not reveal the "pre-image" of the hash text, meaning input values should not be discoverable just by looking at the output, whether the hashing algorithm is known or not.

A handy analogy is the Modulus function: `5 % 3 = 2` but so does `10 % 4 = 2` => The input value(s) are not revealed!

### Hashing Complexity and Uses

Avalanche Effect: A small change in an input produces a big difference in the output.

Deterministic Algorithm: The same input *always* produces the same output.

Hash outputs can be used to:

- Transmit password hash text across the network/internet without revealing the data or inputs.
- Store password hash texts in databases for comparison next time a user logs in.

### Salting

Add a dash of salt to improve/change the flavor of your food.

Similarly, add a special code/value into the hashing algorithm to produce a slightly different hash text.

Salt values must also be stored or it could be used to reverse-engineer the hash texts you are storing.

Salted password hashes can be helpful against "Rainbow Table Attacks", where a list of already leaked/discovered hashes are tested against an algorithm to reverse-engineer the passwords/encrypted plain text.

### Other Hashing Functions

Producing a CRC: In this case, the idea is to hash the datagram and send the hashed DG along with (or following) the DG's network packet, so the receiving node can compare the CRC to the DG they received.

CRC Hashing is not cryptographically secure, and could be reverse engineered.

### Hashing Collisions

Just like with modulus, two different inputs that produce exactly the same output is considered a collision.

Forcing collisions is a technique used to 'break' a hashing function without ever discovering the actual input values for a given collision.

*Take note*: Collisions *have been found* in commonly used hashing algorithms.

- MD5 is considered fully reversible.
- SHA-1 has a documented collision (per Google/Alphabet) and is considered "unsafe".

### Hashing Security Measures

Hashing algorithms should be slow, in order to deter brute-force attacks.

Safer algorithms today are: SHA-256 and SHA-3.

Use salting techniques to reduce the likelihood of a collision.

## BCrypt Overview

[bcrypt overview](https://danboterhoven.medium.com/why-you-should-use-bcrypt-to-hash-passwords-af330100b861)

Features:

- One-way hashing.
- Salted passwords.
- Random 'user salts', generated at the time the user account is setup.
- Blowfish Block Cipher Crypto Algorithm

Authors: Niels Provos and David Mazieres.

Created in 1999.

Blowfish Block Ciper Cypto Algorithm is an adaptive hash function.

Uses a 'keyfactor' to force varying outputs and slows the hashing algorithm.

Fends against Rainbow Hash Table attacks.

## jBCrypt

[jBCrypt (the paragraphs and code example at the top of the page)](https://www.mindrot.org/projects/jBCrypt/)

Paragraphs and code example.

JBCrypt is:

- Java implementation of OpenBSD's Blowfish passwd hash algorithm (Niels Provos and David Mazieres).
- Blowfish was developed by none other than Bruce Schneier!
- Parameterized computational cost allows slowing the hashing speed as computers get faster.

JBCrypt Code snippet for reference:

```java
// Hash a password for the first time
String hashed = BCrypt.hashpw(password, BCrypt.gensalt());

// gensalt's log_rounds parameter determines the complexity
// the work factor is 2**log_rounds, and the default is 10
String hashed = BCrypt.hashpw(password, BCrypt.gensalt(12));

// Check that an unencrypted password matches one that has
// previously been hashed
if (BCrypt.checkpw(candidate, hashed))
{
  System.out.println("It matches");
}
else
{
  System.out.println("It does not match");
}
```

## Footer

Back to root [readme](../README.html)
