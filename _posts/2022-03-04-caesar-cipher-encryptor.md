---
title: Caesar Cipher Encryptor
---

```python
Difficulty: 'Easy'
Category:   'Strings'
```
# Caesar Cipher Encryptor
Given a non-empty string of lowercase letters and a non-negative integer representing a key, write a function that returns a new string obtained by shifting every letter in the input string by k positions in the alphabet, where k is the key.

Note that letters should "wrap" around the alphabet; in other words, the letter `z` shifted by one returns the letter `a`.

**Sample Input**
```python
string = "xyz"
key = 2
```

**Sample Output**
```python
"zab"
```

**Solution**

How to implement that "wrapping" around the alphabet, as problem statement mentions it? Well, we can do it with the remainder of division. Add key to the position of a letter in the alphabet, then divide it by the length of the alphabet and take the remainder.
```python
def caesarCipherEncryptor(string, key):
    alphabet = "abcdefghijklmnopqrstuvwxyz"
    encrypted = []
	
    for letter in string:
        letterIndex = alphabet.index(letter)
        newIndex = (letterIndex + key) % len(alphabet)
        encrypted.append(alphabet[newIndex])
	
    return "".join(encrypted)
```
