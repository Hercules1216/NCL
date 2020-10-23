# VSFTPD (Easy)

### Analyze a VSFTPD log file that we obtained.

1. What IP address did "ftpuser" first log in from?
1. What is the first directory that ftpuser created?
1. What is the last directory that ftpuser created?
1. What file extension was the most commonly used by ftpuser?
1. What is the username of the other user in this log?
1. What is the IP address did this other user log in from?
1. How many total bytes did this other user upload?
1. How many total bytes did ftpuser upload?
1. How many total bytes did ftpuser download?
1. Identify the suspicious (login with no activity) login IP address in this log.

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
1. head vsftpd.log
    + `10.0.0.123`
2. grep MKDIR vsftpd.log
    + `TreeSizeFree`
3. grep MKDIR vsftpd.log
    + `110D300S`
4. grep UPLOAD vsftpd.log | cut -d '"' -f4 | rev | cut -d '/' -f1 | rev | cut -d '.' -f2 | sort | uniq -c | sort -nr
    + `JPG`
5. awk '{print $8}' vsftpd.log| sort | uniq
    + `jimmy`
6. grep 'jimmy' vsftpd.log | head
    + `10.0.0.214`
7. grep 'jimmy' vsftpd.log | grep UPLOAD | awk ' {print $15}' [Sum Calculator](https://miniwebtool.com/sum-calculator/)
    + `105750628`
8. grep 'ftpuser' vsftpd.log | grep UPLOAD | rev | awk '{print $3}' | rev  > output.txt [Sum Calculator](https://miniwebtool.com/sum-calculator/)
    + `13980839165`
9. grep 'ftpuser' vsftpd.log | grep DOWNLOAD | rev | awk '{print $3}' | rev  > output2.txt [Sum Calculator](https://miniwebtool.com/sum-calculator/)
    + `6008032`
10. grep LOGIN vsftpd.log  | rev | awk '{print $1}' | rev | uniq -c <br>
  a. grep '\.0\.6' vsftpd.log
    + `10.3.0.6`
