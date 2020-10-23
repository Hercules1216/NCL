# Netflow (Easy)

### The NetFlow log was collected by an Internet Service Provider (ISP) in the city, analyze the log and give some feedback.

1. How many total NetFlow records are there?
1. How many unique client IP addresses are there?
1. What is the most frequent client IP address?
1. What IP address appeared exactly 10 times?
1. What does the S in the flags column stand for?
1. How many total S flags were there?

---

###
1. `wc -l netflow.txt`
1. `cut -d ':' -f3 netflow.txt | cut -d 'P' -f2 | tr -d ' '| sort -n | uniq | wc -l`
1. `cut -d ':' -f3 netflow.txt | cut -d 'P' -f2 | tr -d ' '| sort -n | uniq -c | sort -nr | head`
1. `cut -d ':' -f3 netflow.txt | cut -d 'P' -f2 | tr -d ' '| sort -n | uniq -c | sort -nr | head -20`
1. `[Wilder Security](https://www.wilderssecurity.com/threads/tcp-flags-s-whats-this.41583/)  AND` 
`[Firewall](http://www.firewall.cx/networking-topics/protocols/tcp/136-tcp-flag-options.html)`
1. `cat netflow.txt | awk '{print $8}' | grep S | wc -l`
