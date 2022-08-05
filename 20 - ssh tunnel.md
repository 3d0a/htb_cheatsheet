# if u want to forward ports which are protected by firewall use command:
```bash
$ nohup ssh -i id_rsa patrick@10.10.11.118 -L 1337:localhost:8086 -N &
```
-L [localport]:localhost[port on host]