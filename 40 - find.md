```bash
find / -perm -g=w ! -path '/proc/*' ! -path '/sys/*' -group $(groups) -exec ls -lLd {} +  2>/dev/null
```