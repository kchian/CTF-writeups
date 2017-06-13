#Keyz

To create a key, one can simply use the command
`ssh-keygen -t rsa`
which generated id_rsa.pub. To use for authentication, I renamed the file authorized_keys for use, then copied its contents into my local (Windows) machine to generate a private key. Since my SSH client of choice is PuTTY, I used PuTTYgen to create a private key in a .ppk file. Finally, after inputting all the settings into PuTTY (remembering to add the .ppk file to Connection>Auth>SSH>"Private key file for authentication:") and logging in, the flag is seen to be:
`who_needs_pwords_anyways`. How apt!

