#Apache2웹서버와 Node.js어플리케이션을 함께 사용하기!

###순서
1. 내부적으로 다른 포트에 nodejs기반의 서버를 실행한다.
2. apache의 VirtualHosts 설정에서 ProxyPass를 설정한다.
3. 특정 url로 접근식 1번으로 갈 수 있게 설정한다.

###과정
1. mod_proxy, mod_proxy_http가 필요하다. (ubuntu apache서버는 기본적으로 설치되어있음. `/etc/apache2/mods-available`안에 있음 `a2enmod proxy`,`a2enmod proxy_http`로 설정함
2. 가상호스트를 설정함 ./sites-available 내부에 기존파일 또는 신규파일을 추가한다.

```powershell
<VirtualHost *:80>
	DocumentRoot /var/www/example.com/public_html
	ServerName  www.example.com
		
	# Index file and Document Root (where the public files are located)
	DirectoryIndex index.html index.php

	# Log file locations 
	LogLevel warn
	ErrorLog  /var/www/amazeapp.com/log/error.log
	CustomLog /var/www/amazeapp.com/log/access.log combined


	# 아래가 핵심이다.

	ProxyRequests off
	
	<Proxy *>
	    Order deny,allow    # 이부분의 경우, 콤마(,) 사이에 공백 없어야 함!
	    Allow from all
	</Proxy>
	
	<Location /> # 내부적으로 접속 노드를 늘리고 싶다면 여기에 추가.
	    ProxyPass http://localhost:3000/
	    ProxyPassReverse http://localhost:3000/
	</Location>
		
</VirtualHost>
```

3. 아파치 재시작 

끝~

###Reference
[https://github.com/sindresorhus/guides/blob/master/run-node-server-alongside-apache.md](https://github.com/sindresorhus/guides/blob/master/run-node-server-alongside-apache.md)