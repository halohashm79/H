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
> old parameter ,1-gau 
```
cat res3.txt |gau |tee res4.txt
```

