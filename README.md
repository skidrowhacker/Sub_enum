# Sub_enum_Advanced 
# Yasser_Alenazi
# Twitter : @firfox20
# Single Liners to Sub_Enum live_Subs from crt.sh and save it to file , Scan Ports , DirFuzzing, XSS Hunting 
# apt install pup  before you Lanuch !
# Change Target Name before you start Hunting Good Luck !


curl -fsSL "https://crt.sh/?q=msi.com&exclude=expired" | pup 'td :contains(".msi.com") text{}' | sort -n | uniq -c | sort -rn | column -t |> msi.txt ;cat msi.txt | awk -F " " '{print $2 }'  > msi1.txt ;cat msi1.txt | httpx -mc 200  > live_msi.txt ;cat live_msi.txt | cut -d"/" -f3 | cut -d"/" -f5 > done_msi.txt

# if you would like to add nmap -List Scan 


curl -fsSL "https://crt.sh/?q=msi.com&exclude=expired" | pup 'td :contains(".msi.com") text{}' | sort -n | uniq -c | sort -rn | column -t |> msi.txt ;cat msi.txt | awk -F " " '{print $2 }'  > msi1.txt ;cat msi1.txt | httpx -mc 200  > live_msi.txt ;cat live_msi.txt | cut -d"/" -f3 | cut -d"/" -f5 > done_msi.txt ; nmap -iL done_msi.txt --open -vv



# if you would like to add ffuff Fuzzing 

curl -fsSL "https://crt.sh/?q=msi.com&exclude=expired" | pup 'td :contains(".msi.com") text{}' | sort -n | uniq -c | sort -rn | column -t |> msi.txt ;cat msi.txt | awk -F " " '{print $2 }'  > msi1.txt ;cat msi1.txt | httpx -mc 200  > live_msi.txt ;cat live_msi.txt | cut -d"/" -f3 | cut -d"/" -f5 > done_msi.txt ; for URL in $(<done_msi.txt); do ( ffuf -u "${URL}/FUZZ" -w /usr/share/wordlists/dirbuster/directory-list-2.3-small.txt -mc 200 -ac ); done  



# if you would like to add XSS Hunting for Unfilterd < > 



curl -fsSL "https://crt.sh/?q=msi.com&exclude=expired" | pup 'td :contains(".msi.com") text{}' | sort -n | uniq -c | sort -rn | column -t |> msi.txt ;cat msi.txt | awk -F " " '{print $2 }'  > msi1.txt ;cat msi1.txt | httpx -mc 200  > live_msi.txt ;cat /root/live_msi.txt | cut -d"/" -f3 | cut -d"/" -f5 > done_msi.txt ; cd paramspider/ ; paramspider -l /root/done_msi.txt ; cd /root/paramspider/results ; cat *.txt | kxss | grep '< >'



# Good Luck and Hack Ethically : ) 
