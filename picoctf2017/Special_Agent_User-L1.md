#Special Agent User
In order to find the browser a user may be using, HTTP has a field called User-Agent. This challenge is, quite simply, looking for this field. By filtering Wireshark by HTTP, then scrolling through the ~8 requests, one can find that the User-Agent fields are as follows:
```
User-Agent: Wget/1.16 (linux-gnu)
User-Agent: Wget/1.16 (linux-gnu)
User-Agent: Wget/1.16 (linux-gnu)
User-Agent: Mozilla/5.0 (X11; OpenBSD i386) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36
User-Agent: Wget/1.16 (linux-gnu)
User-Agent: Wget/1.16 (linux-gnu)
```

The wget is likely what the browser runs on, and thus can be ignored as it is not a browser as we're looking for. To find the flag, the browsers listed in `Mozilla/5.0 (X11; OpenBSD i386) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36` can be attempted sequentially. The shrewd would notice that the challenge has a note which suggests the correct answer has >3 version numbers. As a result, the flag is Chrome 36.0.1985

###Alternate solution

Alternatively, tcpdump and grep can be used. 

tcpdump -A -r data.pcap | grep -i 'user-agent'

which quite elegantly gives the list of User-Agents as displayed above.
