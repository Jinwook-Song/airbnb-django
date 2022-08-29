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

`python manage.py migrate`

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

---

Django는 framework이다

1. admin.py는 어드민페이지에 해당 되며, 추후 model등을 등록할때 이용된다.

2. models.py는 우리가 데이터베이스를 정의 하는 곳 이다. 이렇게 SQL문을 직접 다루지 않고 파이썬 코드를 통해 간접적으로 구현하는 방식을 ORM 이라 부른다.

3. views.py는 웹서버 구동시 사용될 logic을 담당한다.

4. urls.py는 url과 view를 mapping 한다.

---

Replace Default User

```tsx
1. model == 데이터가 보여지는 모습 (데이터 테이블을 정의하는 것)

2. class User(AbstractUser):
admin 페이지 에서 보여준 user에 관한 정보를 상속하여 확장한다.
차후 추가적인 정보인 성별, 관심사 등등 확장해 나갈 수 있다.

3. app은 settings.py에 등록해야 사용가능

4. 기존에 Django에는 user 라는 app이 이미 존재함.
따라서 우리가 만든 users app과 충돌이 발생함
=> db.sqllite3를 제거후, AUTH_USER_MODEL 등록시 Django는 우리가 만든 users app을 인식하게 됨
```

---

`python [manage.py](http://manage.py/) makemigrations`

`python [manage.py](http://manage.py) migrate`

---

### Custom User Model

imageField는 Pillow 가 필요하다. `pip install Pillow`

```tsx
class User(AbstractUser):

    """Custom user model"""

    GENDER_MALE = "male"
    GENDER_FEMALE = "female"
    GENDER_OTHER = "other"

    GENDER_CHOICES = (
        (GENDER_MALE, "Male"),
        (GENDER_FEMALE, "Female"),
        (GENDER_OTHER, "Other"),
    )

    LANGUAGE_ENGLISH = "en"
    LANGUAGE_KOREAN = "kr"

    LANGUAGE_CHOICES = ((LANGUAGE_ENGLISH, "English"), (LANGUAGE_KOREAN, "Korean"))

    CURRENCY_USD = "usd"
    CURRENCY_KRW = "krw"

    CURRENCY_CHOICES = ((CURRENCY_USD, "USD"), (CURRENCY_KRW, "KRW"))

    avatar = models.ImageField(null=True, blank=True)
    gender = models.CharField(
        default=GENDER_MALE,
        choices=GENDER_CHOICES,
        max_length=10,
        null=True,
        blank=True,
    )
    bio = models.TextField(default="", blank=True)
    birthdate = models.DateField(null=True, blank=True)
    language = models.CharField(
        default=LANGUAGE_KOREAN,
        choices=LANGUAGE_CHOICES,
        max_length=2,
        null=True,
        blank=True,
    )
    currency = models.CharField(
        default=CURRENCY_KRW,
        choices=CURRENCY_CHOICES,
        max_length=3,
        null=True,
        blank=True,
    )
    superhost = models.BooleanField(default=False)
```

null은 데이터 베이스를 위해서, blank는 form을 위해 사용된다.

---

### Custom Admin Pannel

```tsx
@admin.register(models.User)
class CustomUserAdmin(admin.ModelAdmin):

    """Custom user admin"""

    list_display = ("username", "gender", "language", "currency", "superhost")
    list_filter = ("language", "superhost")
```
