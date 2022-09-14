On your server (A):

nc -l -p 1234 -q 1 > something.zip < /dev/null

On your "sender client" (B):

cat something.zip | netcat server.ip.here 1234