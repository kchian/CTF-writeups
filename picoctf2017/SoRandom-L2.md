#SoRandom

The key to solving this flag is realizing that a when created with a seed, the random function would output the same numbers in sequence no matter where/when it was run. In other words, the function gives random numbers, but always in the same order when there's the same seed. So, I created a python script which reversed the original script.
Here's part of sorandom.py with my interpretation:

```
  if c.islower(): #If lowercase
    encflag += chr((ord(c)-ord('a')+random.randrange(0,26))%26 + ord('a'))
    
    #see how far the character numerically is above 'a'
    #add a random amount while making sure it stays less than 26
    #add the value of 'a' again to make it an lowercase character
    
  elif c.isupper(): # same with uppercase and numbers
    encflag += chr((ord(c)-ord('A')+random.randrange(0,26))%26 + ord('A'))
  elif c.isdigit():
    encflag += chr((ord(c)-ord('0')+random.randrange(0,10))%10 + ord('0'))
  else:
    encflag += c
```
To reverse the code, it's easiest to see what it'd do on paper. 
If the character was "c", and the random number was 1, the function would evaluate as such: 
encflag += chr((99-97+random.randrange(0,26))%26 + ord('a'))
=chr((99-97 + 1)) + ord('a'))
=chr(3) + ord('a')
=chr(3) + 97 
='d'

With this in mind, reversing the code is as simple as reversing a math equation with only basic functions.

```
import random, string

flag = ""
x = None
encflag = open("encflag", "r").read()[:-1]
random.seed("random")
for c in encflag:
    if c.islower():
        x = random.randrange(0, 26) % 26
        flag += chr((ord(c) - ord('a') - x) % 26 + ord('a'))
    elif c.isupper():
        x = random.randrange(0, 26) % 26
        flag += chr((ord(c) - ord('A') - x) % 26 + ord('A'))
    elif c.isdigit():
        flag += chr((ord(c) - ord('0') - random.randrange(0, 10)) % 10 + ord('0'))
    else:
        flag += c
print("Guessably Randomized Flag: " + flag)
```
To reverse the flag, one simply has to subtract that randomized number instead of add it, then go through the same process to keep it lowercase, uppercase, or a number.
