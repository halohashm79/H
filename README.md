### scan sub domain 
>tool subfinder automatic 
```
subfinder -d example.com >res.txt
```
>gobuster for wordlists
```
gobuster dns -d example.com -w wordlits.txt
```
### passive scan httpx
> httpx
```
httpx -l res.txt -o res2.txt
```

>next step install tool 
* [subzy](https://github.com/PentestPad/subzy)
>next
```
subzy run --targets res2.txt > res3.txt

```

### scan parampeter
> old parameter ,1-gau 2-paramspider
* [gau](https://github.com/lc/gau)
```
cat res3.txt |gau |tee res4.txt
```
>next 
```
paramspider -l domains.txt
paramspider -d exam.com
```
> new parampeter
```
ffuf -u exam.com/FUZZ.php -w wordlist.txt

dirsearch -u exam.com 
```
### Bruteforce parameters
* [Sh1Yo/x8](https://github.com/Sh1Yo/x8) 

* Use wordlists of common parameters and send them, look for unexpected behavior from the backend. 
    ```ps1
    x8 -u "https://example.com/" -w <wordlist>
    x8 -u "https://example.com/" -X POST -w <wordlist>
    ```




