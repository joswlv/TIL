#MySQL DB연동 정보입력

기본적으로 설치되어 있는 MySQLDB어댑터가 Django1.8버전에서 제대로 동작하지 않는다고 한다. 그래서 PyMySQL어댑터를 사용한다.

`settings.py`에서

```python
import pymysql
pymysql.install_as_MySQLdb()

DATABASES = {
		'default':{
			'ENGINE': 'django.db.backends.mysql',
			'NAME': '{Database}',
			'USER': '{Username}',
			'PASSWORD': '{Password}',
			'HOST': 'localhost',
			'PORT': '3306',
	}
			
```

`python manage.py makemigrations`와 `python manage.py migrate`를 실행하면 끝~~!

쉘에 DB와 MysqlDB의 sync를 맞추려면 `python manage.py syncdb` 라고 하면 됨
