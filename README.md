# ctfchallenge_co_uk


# target: vulnerable website for ctf(ctfchallenge.co.uk)

## easy | vulnbegin | 9 flags

### cookie used during automation: ctfchallenge=eyJkYXRhIjoiZXlKMWMyVnlYMmhoYzJnaU9pSTRNWGd5WVdwMGRTSXNJbkJ5WlcxcGRXMGlPbVpoYkhObGZRPT0iLCJ2ZXJpZnkiOiJkMGE3MTE1NmMxYTY5YmM3NWRjN2QzZDg1ZjEwNzVkYiJ9


### 4-flag : 
robots.txt --> http://www.vulnbegin.co.uk/secret_d1rect0y/ -->[^FLAG^2B22E2CB70E218510802B0359488F6A2^FLAG^]

tools used and documentation:
#### nslookup -type=any vulnbegin.co.uk 8.8.8.8
The above command will query the DNS server for any default A,TXT,NS,SOA,SPF records. You will see from the results there is a TXT record with a flag.

### 1-flag: [^FLAG^BED649C4DB2DF265BD29419C13D82117^FLAG^]

sublist3r -d vulnbegin.co.uk

The above query uses OSINT to discover domain names from various search engines and other data resources, from the result you will find an obscure subdomain if you visit it this will show you a flag

result:
server.vulnbegin.co.uk

v64hss83.vulnbegin.co.uk

### 3-flag 
[^FLAG^E858ED9649E57BECE9ACD1A4C60D3446^FLAG^] on server.vulnbegin.co.uk
 
 ### 2-flag from sublister : [^FLAG^047524FE61AE6B5FD1D184994C7322FC^FLAG^]


dnsrecon for finding subdomains using brute force
dnsrecon -d vulnbegin.co.uk -D ~/wordlists/subdomains.txt -t brt


content discovery using ffuf:
ffuf -p 0.1 -t 1 -w ~/wordlists/content.txt -H "Cookie: ctfchallenge=eyJkYXRhIjoiZXlKMWMyVnlYMmhoYzJnaU9pSTRNWGd5WVdwMGRTSXNJbkJ5WlcxcGRXMGlPbVpoYkhObGZRPT0iLCJ2ZXJpZnkiOiJkMGE3MTE1NmMxYTY5YmM3NWRjN2QzZDg1ZjEwNzVkYiJ9" -u http://www.vulnbegin.co.uk/FUZZ
