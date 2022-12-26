On your server (A):

nc -l -p 1234 -q 1 > linlog < /dev/null

On your "sender client" (B):

cat linlog | netcat 10.10.16.3 1234