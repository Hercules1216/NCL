# Scanner (Easy)

### Inspect this malware scan log file from an IDS on the police network.

1. How many files did the IDS process?
1. How many days does this log span (inclusive, round to nearest whole number)?
1. What is the URL (without any query parameters) of the file that the IDS rejected?
1. How many zip files did the IDS process?
1. How many unique server IP addresses were downloads made from?
1. What is the URL of the largest file downloaded?

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
1. wc -l ScanLog.csv (subtract 1 for the header)
    + `161`
2. head -2 ScanLog.csv AND tail -1 ScanLog.csv
    + `14`
3. rev ScanLog.csv | cut -d ',' -f1 | rev | sort | uniq THEN grep Rejected ScanLog.csv
    + `http://r8---sn-a8au-p5qs.gvt1.com`
4. rev ScanLog.csv | cut -d ',' -f3 | rev | sort | uniq -c (subtract 2)
    + `108`
5. cut -d ',' -f6 ScanLog.csv | sort | uniq -c | wc -l
    + `33`
6. rev ScanLog.csv | cut -d ',' -f2 | rev | sort -nr | head THEN grep 9747696 ScanLog.csv
    + `http://download-cdn.gfe.nvidia.com/packages/DAO/production/21376336/00009766/0.dat`
