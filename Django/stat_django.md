#Django Start

##Django install

- 가상환경 만들기 --> `phton3 -m venv myvenv`
- 가상환경 실행 --> `source myvenv/bin/activate`
- Django 설치 --> `pip install django==1.8`

##Django 프로젝트 생성
- 가상환경에서 `django-admin startproject mysite .`라고 침
- `mysite/settings.py`에서 프로젝트 시간, DB설저을 함
- 서버 실행 `python manage.py runserver 0:8000`

##Model 만들기
- `python manage.py startapp blog`
- myseite/settings.py에서 INSTALLED_APPS에 `blog`모델 추가하기

##슈퍼유저 생성
- `python manage.py createsuperuser`

##정적파일 자동관리
- `pip install django whitenoise`로 `whitenoise` 설치
- `python manage.py collectstatic`실행

###References
- [장고 걸스 튜토리얼 (Django Girls Tutorial)](http://tutorial.djangogirls.org/ko/)
- [CRUD실습한 결과](http://wsj7932.pythonanywhere.com)