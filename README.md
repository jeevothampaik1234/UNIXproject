# UNIXproject
# first create a demo log file if there is a log file present it can be used
    grep -Eo '([0-9]{1,3}\.){3}[0-9]{1,3}' filename.log 
# can use 
    grep -Eo '([0-9]{1,3}\.){3}[0-9]{1,3}' filename.log | sort | uniq -c |sort -nr
#this is one of the ways to find IPs




#other way to find the IP 
#first creat a sh file (extract_ip.sh)
# open it with vi to write the code,the code is:


      
      #!/bin/bash
      # Script: extract_ips.sh
      # Description: Extracts unique IPs and counts frequency from a log file
      
      LOGFILE="demo.log"
      
      # Check if file exists
      if [ ! -f "$LOGFILE" ]; then
          echo "Log file '$LOGFILE' not found!"
          exit 1
      fi
      
      # Extract unique IPs
      grep -Eo '([0-9]{1,3}\.){3}[0-9]{1,3}' "$LOGFILE" | awk '!seen[$0]++' > unique_ips.txt
      
      # Count frequency
      grep -Eo '([0-9]{1,3}\.){3}[0-9]{1,3}' "$LOGFILE" | sort | uniq -c | sort -nr > ip_count.txt
      
      # Optional: Get geolocation info
      echo "Fetching geolocation info..."
      > ip_location.txt
      for ip in $(cat unique_ips.txt); do
          echo "---- $ip ----" >> ip_location.txt
          curl -s ipinfo.io/$ip | grep -E 'ip|country|city|org' >> ip_location.txt
          echo "" >> ip_location.txt
      done
      
      echo "1) Unique IPs saved in unique_ips.txt"
      echo "2) IP counts saved in ip_count.txt"
      echo "3) Geolocation saved in ip_location.txt"
# make the script executable with the code:
    chmod +x extract_ip.sh
# run the code:
    ./extract_ip.sh

# to get IP's(to view unique IP's):
    cat unique_ips.txt
# to number them:
    nl unique_ips.txt
# view IP counts (how many times each IP appeared):
    cat ip_count.txt
# to list which IPs were processed:
    file ip_location.txt
    head -3 ip_location.txt

