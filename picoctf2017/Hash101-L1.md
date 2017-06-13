#Hash101


```
Welcome to Hashes 101!

There are 4 Levels. Complete all and receive a prize!


-------- LEVEL 1: Text = just 1's and 0's --------
All text can be represented by numbers. To see how different letters translate to numbers, go to http://www.asciitable.com/

TO UNLOCK NEXT LEVEL, give me the ASCII representation of 0111011101101111011100100110110001100100

>world
Correct! Completed level 1

------ LEVEL 2: Numbers can be base ANYTHING -----
Numbers can be represented many ways. A popular way to represent computer data is in base 16 or 'hex' since it lines up with bytes very well (2 hex characters = 8 binary bits). Other formats include base64, binary, and just regular base10 (decimal)! In a way, that ascii chart represents a system where all text can be seen as "base128" (not including the Extended ASCII codes)

TO UNLOCK NEXT LEVEL, give me the text you just decoded, world, as its hex equivalent, and then the decimal equivalent of that hex number ("foo" -> 666f6f -> 6713199)

hex>776f726c64            
Good job! 776f726c64 to ASCII -> world is world
Now decimal
dec>512970878052
Good job! 512970878052 to Hex -> 776f726c64 to ASCII -> world is world
Correct! Completed level 2

----------- LEVEL 3: Hashing Function ------------
A Hashing Function intakes any data of any size and irreversibly transforms it to a fixed length number. For example, a simple Hashing Function could be to add up the sum of all the values of all the bytes in the data and get the remainder after dividing by 16 (modulus 16)

TO UNLOCK NEXT LEVEL, give me a string that will result in a 10 after being transformed with the mentioned example hashing function

>J
Correct! Completed level 3

--------------- LEVEL 4: Real Hash ---------------
A real Hashing Function is used for many things. This can include checking to ensure a file has not been changed (its hash value would change if any part of it is changed). An important use of hashes is for storing passwords because a Hashing Function cannot be reversed to find the initial data. Therefore if someone steals the hashes, they must try many different inputs to see if they can "crack" it to find what password yields the same hash. Normally, this is too much work (if the password is long enough). But many times, people's passwords are easy to guess... Brute forcing this hash yourself is not a good idea, but there is a strong possibility that, if the password is weak, this hash has been cracked by someone before. Try looking for websites that have stored already cracked hashes.

TO CLAIM YOUR PRIZE, give me the string password that will result in this MD5 hash (MD5, like most hashes, are represented as hex digits):
d63d5efad4a59c06228d0596a89e2a34

>3mb0x
Correct! Completed level 4
You completed all 4 levels! Here is your prize: c3ee093f26ba147ccc451fd13c91ffc
```
##Level 1:

Using the website http://www.asciitohex.com/ and inputting the binary into its proper field will yield the correct string under ascii.

###Level 1 Alternate Solution:
Use python! Break the binary into 8-character chunks, then convert to decimal, then to a character, and append that to a string.
```
x = '0111011101101111011100100110110001100100'
out = ''
while len(x)>0:
    out += (chr(int(x[:8],2)))
    x = x[8:]
print(out)
#world
```

##Level 2: 
Use the same website as level 1, just take the hexadecimal field and remove the spaces.
For the second question, any online hex to decimal converter would work (http://www.binaryhexconverter.com/hex-to-decimal-converter for example).

###Level 2 Alternate Solution:
Use python to take each character of the word, convert it to a decimal using ord(), then to hex with hex(), which yields a 0x__ number. From there, remove the preceding '0x' and put that into a string. For part two, turn the result from part 1 into an integer and convert it to decimal by using the second parameter of the int() function.
```
x = 'world'
out = ''
for c in x:
    out+=(str(hex(ord(c)))[2:])
print(out)
#776f726c64
print(int(out,16))
#512970878052
```

##Level 3:
For this level, to get a value of 10 after the hashing function, the simplest solution is to look up an ascii table to find a single character in which that character's decimal value modulus 16 yields 10. To find "J", I counted by multiples of 16 (16*4 = 64), then added 10 once the characters were easy to type (64+10 = 74 = "J"). Since there is only one byte in the data, there is no need to sum and the answer is correct.
###Level 3 Alternate Solution:
You can brute force... I guess. Counting works too, but who would count when you could just type "thequickbrownfoxjumpsoverthelazydog" with an enter between each character.
```
>a
incorrect. sum of all characters = 97 mod 16 = 1 does not equal 5
>b
incorrect. sum of all characters = 98 mod 16 = 2 does not equal 5
>c
incorrect. sum of all characters = 99 mod 16 = 3 does not equal 5
>d
incorrect. sum of all characters = 100 mod 16 = 4 does not equal 5
>e
Correct! Completed level 3
```

##Level 4:
Copy and paste the given hash into a website which searches a store of md5 hashes. I used https://crackstation.net/




