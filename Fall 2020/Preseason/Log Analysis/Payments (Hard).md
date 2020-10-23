# Payments (Hard)

### A payment transaction log has been compromised in a data breach. Find out what information it contains.

1. How many transactions are contained in the log?
1. What was the largest purchase made in the log?
1. Which state made the most number of purchases?

---

## Commands
- head - Gives the first 10 lines of a file
- grep - a searching function
- cut - splits up a file using a delimeter (-d) and then select the field you want (-f)
- rev - reverses the string
- sort - sorts the results 
- uniq - removes duplicates that are next to eachother
- awk - in this case it is used like the cut command
---
1. grep OrderTotal payments.log | wc -l
    + `192`
2. grep -o -P 'currencyID=.{0,6}' payments.log | sort | uniq THEN cat payments.log | grep -o -P 'USD.{0,10}' | cut -d '>' -f2 | cut -d '<' -f1 | sort -nr | head
    + `998.6`
3. grep --color=always -o -P '<ebl:StateOrProvince>.{0,6}' payments.log | sort | uniq -c | sort -nr | head
    + `MA`
