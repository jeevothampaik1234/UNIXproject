# UNIXproject
#first create a demo log file if there is a log file present it can be used
grep -Eo '([0-9]{1,3}\.){3}[0-9]{1,3}' filename.log 
#can use 
grep -Eo '([0-9]{1,3}\.){3}[0-9]{1,3}' filename.log | sort | uniq -c |sort -nr
#this is one of the ways to find IPs

#next way to find the IP 
