On your server (A):


```
nc -l -p 1234 -q 1 > something.zip < /dev/null
```

On your "sender client" (B):

```
cat lin.log | netcat 10.10.16.5 1234
```