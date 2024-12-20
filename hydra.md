# Hydra

### Overview:
- [Hydra's Types](#hydras-types)
- [Hydra's Style](#hydras-style)
- [Syntax Breakdown](#syntax-breakdown)
- [Options](#options)
- [SSH Brute-force](#ssh-brute-force)
- [MySQL Brute-force](#mysql-brute-force)
- [FTP Brute-force](#ftp-brute-force)
- [Login Page Brute-force](#login-page-brute-force)
- [Key Point](#key-point)


### Hydra's Types
- CLI Based
- GUI Based

## Hydra's Style

New Style
- hydra [some command line options] ` PROTOCOL://TARGET:PORT/MODULE-OPTION`

``` 
hydra ftp://192.168.0.2:2221 -I admin -P list.txt 
```
Old Style
- hydra [some command line options] `[-s PORT] TARGET PROTOCOL [MODULE-OPTIONS]`
``` 
hydra 192.168.0.2 ftp -I admin -P list.txt -S 2221
```

## Syntax Breakdown
`hydra ftp://192.168.0.2:2221 -I admin -P list.txt` 

### <u> Select your Target </u>

- Single Target
    - Single Target
        - 192.168.0.102
    - Subnet
        - 192.168.2.0/24
- A Network Range
- List 01 Hosts in d Text File

### List
`
192.168.0.2,
192.168.0.5,
192.168.0.6,
192.168.0.7,
`
`
192.168.0.2:221,
192.168.0.5:2221,
192.168.0.6:22222,
192.168.0.7:222,
`

- Find a Protocol
- Check for Destination Port

- Check for Module Options

    E.g. http-get

    - A auth-type
    - H = User Defined Header
    - S - Check for Text in HTTP Response

## Options
- I Single User Name
- L List of User Names
- p Single User Password
- P List of Passwords
- V Show Output on the Screen
- t Tasks [default:- 16]
- o Output File
- m Module Options
- f -when you got uname & pass then stop the hydra

### Module Syntax
LOGIN, PLAIN, CRAM-MD5, CRAM-SHAI, CRAM-SHAZ56, DIGEST-MD5, NTLM

`hydra -l test -p test -m PLAIN 1?7.0.0.1 imap` old style

`hydra -l test -p test 127,010.1 imap PLAIN` old style

`hydra -l test -p test imap://lZ7.0.0.l/PLAlN` new style

## SSH Brute-force
```
hydra ssh://target-ip -L path/to/username -P /path/to/passwords.txt -f -v
```

## MySQL Brute-force
```
hydra mysql://192.168.1.100 -l root -P /home/user/passwords.txt -v -f
```

## FTP Brute-force
### Password Options
<u>  Use -e </u>
- s - try the login as password
- n - try an empty password
- r - reverse the login and try it as password
```
hydra ftp://target-ip -l username -P /path/to/passwords.txt -v -f
```
## Login Page Brute-force
```
hydra TARGET_URL http-post-form "/login:username=^USER^&password=^PASS^:Invalid login" -L path/to/username -P /path/to/passwordlist.txt -s 80 -f -V
```

### Key Point
`hydra [some command line options] -6 smtp://[2001:db8::1]/NTLM`

if you use ip version 6 then you must write -6.