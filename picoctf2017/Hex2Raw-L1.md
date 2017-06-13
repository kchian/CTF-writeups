#Hex2Raw
After cli-ing yourself to the given directory (/problems/c69bcda4ca5a28fd9d18790fc763db73), and listing the files, one finds an executable called hex2raw. 
To solve the problem presented, one must break the string into bits of hex, and convert that into characters.

The first iteration of the python code I used to solve the problem looked as follows:
```
if __name__ == "__main__":
    x = "416f1c7918f83a4f1922d86df5e78348"
    with open("out", "w") as f:
        for i in range(0,len(x)-2,2):
            f.write(bytearray.fromhex(x[i:i+2]).decode())
```
where an error 
```
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xf8 in position 0: invalid start byte
```
was continuously being thrown. To remedy this, I attempted to use latin-1 as an encoding, but after piping out to the hex2raw command,
```
$ cat ~/out | ./hex2raw
Give me this in raw form (0x41 -> 'A'):
416f1c7918f83a4f1922d86df5e78348

You gave me:
416f1c7918c3b83a4f1922c3986dc3b5
That's not what I wanted...
```
which is slightly off. 

Finally, I realized that going through python and all of its encoding complexities wasn't necessary. Linux's built-in command xxd did the trick

```
ploppanda@shell-web:~$ echo "416f1c7918f83a4f1922d86df5e78348" > hex2raw_input
ploppanda@shell-web:~$ xxd -r hex2raw_input hex2raw_soln
```
Here, xxd -r reverses the hexdump found in the input(hex2raw_input) and outputs binary into the outfile (hex2raw_soln). It can then be piped into the hex2raw binary as shown. The command is more complex than just `cat ~/hex2raw_soln | ./hex2raw` because the command must both continue to allow user input and send things to the standard output for viewing.

```
ploppanda@shell-web:/problems/c69bcda4ca5a28fd9d18790fc763db73$ (cat ~/hex2raw_soln && cat)|./hex2raw
Give me this in raw form (0x41 -> 'A'):
416f1c7918f83a4f1922d86df5e78348

You gave me:
416f1c7918f83a4f1922d86df5e78348

Yay! That's what I wanted! Here be the flag:
1d2411efe307f5ac07bd28bbabb5769e
```

