#Digital Camouflage

The hint to this challenge is: 
> It looks like someone logged in with their password earlier. Where would log in data be located in a network capture?

Download the data.pcap file and open it in Wireshark
In the search field, search for HTTP and find the POST request, which indicates a form submission. That HTTP request contains URL-encoded credentials in plain text.
`userid=mathewsr&pswrd=aHJLUVNTTFd2Rw%3D%3D`
Since the password is the flag, after decoding the url-encoding the string is `aHJLUVNTTFd2Rw==`. The two equal signs at the end indicate base 64, which can quickly be translated using web tools or python to find the flag as `hrKQSSLWvG`

###Alternate solution

For a slightly more reliable solution, one could use tcpdump to read the pcap file and grep common username/password aliases from the text.
`$ tcpdump -A -r data.pcap | grep -i 'user\|password\|pass`
the result reads 
`...m....userid=mathewsr&pswrd=aHJLUVNTTFd2Rw%3D%3D`
which can be interpreted to find the same flag.
