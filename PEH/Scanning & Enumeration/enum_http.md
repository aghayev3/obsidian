# Enumerating HTTP/HTTPS

## Go to the website 

- First step, go to the website if there is one

![[Pasted image 20251120165029.png]]

---
## Default web page 

- Default web page like this is a finding, because it gives us information about the server and about the client's hygiene
- 80/443 - 192.168.0.134 - timestamp - default webpage - apache 

---
## Information Disclosure

![[Pasted image 20251120170129.png]]
- disclosure, a little more info than we should be getting
- we get server version and hostname out of this

---
## nikto

- web vulnerability scanner
- it might get auto blocked if the owner has good security
```
nikto -h https://192.168.0.134
```
---
## directory busting
- dirbuster
- gobuster
- dirb
