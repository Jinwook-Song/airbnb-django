# Airbnb with Django

| 프로젝트 기간 | 22.08.20 ~ |
| ------------- | ---------- |
| 프로젝트 목적 | Django     |
| Github        | ‣          |

---

`pip install Django==2.2.5`

`django-admin startproject config`

config 폴더 내의 config 폴더와 manage.py 파일을 루트 경로로 바꾼다.

lint: flake8

formmater: black

[Django documentation](https://docs.djangoproject.com/en/2.2/ref/settings/)

---

`python manage.py runserver`

`python manga.py migrate`

---

project: group of application

application: group of function

application의 기준은 한 문장으로 설명 할 수 있어야 한다.

예를들어 room에 대한 기능을 갖는다면, 그 룸의 소유자 등의 기능은 별개의 application

---

## Applications Setup

- Application LIst
  - Users
  - Rooms
  - Conversations
  - Reviews
  - Reservations
  - Withlists

application이름은 복수형으로 한다

`django-admin startapp <application-name>`
