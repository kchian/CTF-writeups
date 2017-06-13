#bashloop

Since the problem involves iterating through a range of numbers, and piping that as input into an executable, a simple for loop using bash should work:

```
ploppanda@shell-web:~$ cat bashloop.sh
cd /problems/884bb3c8fc9e0dbccc09787c1b016cd4
for x in {0..4096}; do
    ./bashloop $x;
done
```
Which, when run, would output a very large amount of 
```Nope. Pick another number between 0 and 4096```

To remedy this, I used an inverse grep command:

```
ploppanda@shell-web:~$ bash bashloop.sh  | grep -v Nope
Yay! That's the number! Here be the flag: bcf9ac72d8721c303ae95239c2deacb3
```