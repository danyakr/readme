## Документация фреймворка для автотестирования

### Оглавление

* [1. Введение](#1-введение)
* [2. Установка и настройка](#2-установка-и-настройка)
* [3. Структура проекта (POM)](#3-структура-проекта-pom)
* [4. API Reference (Справочник по API)](#4-api-reference)
    * [4.1 Класс LoginPage](#4.1-класс-loginpage)
* [5. Примеры использования](#5-примеры-использования)
* [6. Файлы констант](#6-файлы-констант)
* [7. Тестирование с pytest](#7-тестирование-с-pytest)
* [8. Запуск тестов](#8-запуск-тестов)


 
### 1. Введение <a name="1-введение"></a>

#### 1.1 Описание фреймворка

Этот фреймворк предназначен для автоматизации тестирования системы InstallPlan. Он предоставляет набор классов и методов для взаимодействия с элементами страниц системы. Предоставляя готовые инструменты он  упрощает и ускоряет процесс написания тестовых сценариев. А также обеспечивает эффективную поддержку и модификацию сценариев, за счет подробного наименования выполняемых действий, что улучшает читаемость написанных тестов.


<br>

#### 1.2 Предназначение документации

Данная документация предназначена для разработчиков и тестировщиков, которые хотят использовать фреймворк для автоматизации тестирования, а также для тех, кто хочет разобраться в работе фреймворка. Она предоставляет информацию о том, как развернуть фреймворк локально, а также о классах, методах, функциях и о том, как их использовать.

<br>

#### 1.3 Требования к системе
После клонирования проекта необходимо установить зависимости используемые в нем. Перед установкой библиотек необходимо установить виртуальное окружение (описано в пункте `2.1 Создание виртуального окружения`).
* Python 3.7 или выше
* Playwright (устанавливается с помощью pip install playwright)
* pyperclip (устанавливается с помощью pip install pyperclip)

 
### 2. Установка и настройка <a name="2-установка-и-настройка"></a>

#### 2.1 Создание виртуального окружения

1. Откройте терминал или командную строку.
2. Перейдите в директорию проекта.
3. Создайте виртуальное окружение: `python -m venv .venv`

Для активации виртуального окружения используйте следующие команды:
* **Windows:**
`.venv\Scripts\activate`

* **macOS/Linux:**
`source .venv/bin/activate`

Для выхода из виртуального окружения и возврата к глобальному окружению Python введите следующую команду: `deactivate`

<br>

#### 2.2 Установка необходимых библиотек
После активации виртуального окружения установите необходимые библиотеки. Возможна либо установка вручную, с помощью команды:
`pip install pytest-playwright pyperclip`

Либо используя файл requirements.txt (описано в пункте `2.3 Установка зависимостей с помощью requirements.txt`).

<br>

#### 2.3 Установка зависимостей с помощью requirements.txt
Файл `requirements.txt` содержит список необходимых библиотек для работы фреймворка. Вы можете использовать его для установки всех зависимостей одновременно.

Установите библиотеки, используя команду:
`pip install -r requirements.txt`

После выполнения команды все необходимые библиотеки будут установлены в вашем виртуальном окружении.

<br>

#### 2.4 Настройка конфигурации
Фреймворк не требует настройки конфигурационных файлов. Однако, для работы с Playwright необходимо скачать требуемые браузеры. Это можно сделать, запустив команду:
`playwright install`

 
### 3. Структура проекта (POM) <a name="3-структура-проекта-pom"></a>
Применяется модель Page Object Model (POM) для организации кода.

Структура:

* ip_automation: Корневая директория проекта.
  * const: Директория, где хранятся файлы с константами.
    * error_const.py: Файл с константами ошибок.
    * other_const.py: Файл с другими константами.
  * pages: Директория, где хранятся классы, представляющие страницы приложения (Page Objects).
    * login_page.py: Файл, содержащий класс, представляющий функциональность для тестирования страницы авторизации.
  * tests: Директория, где хранятся файлы с тестовыми сценариями для страниц.
    * test_login_page.py: Файл с тестовыми сценариями для страницы авторизации.
  * pytest.ini: Конфигурационный файл pytest.
  * conftest.py: Файл с фикстурами для pytest.

Новые Page Objects добавляются в директорию pages, а соответствующие тестовые сценарии для этих страниц - в директорию tests. Файлы с константами пополняются по мере необходимости.

 
### 4. API Reference (Справочник по API) <a name="4-api-reference"></a>

#### 4.1 Класс LoginPage <a name="4.1-класс-loginpage"></a>

Класс `LoginPage`, находящийся в файле `login_page.py` предоставляет набор методов для работы с элементами страницы авторизации.

<br>

Атрибуты, определенные в конструкторе класса `LoginPage`:

* `page`: Объект страницы Playwright, представляющий страницу авторизации.
* `login_button`: Элемент кнопки "Войти".
* `confirm_button`: Элемент кнопки "Подтвердить" (используется при двухфакторной аутентификации).
* `email_field`: Элемент поля для ввода логина (email).
* `pwd_field`: Элемент поля для ввода пароля.
* `verification_code_field`: Элемент поля для ввода проверочного кода.
* `forgot_pwd_link`: Элемент ссылки "Забыли пароль?".
* `sms_verification_code_field`: Элемент поля для ввода SMS-кода (используется при двухфакторной аутентификации).
* `email_verification_code_field`: Элемент поля для ввода email-кода (используется при двухфакторной аутентификации).

<br>

Методы, определенные в конструкторе класса `LoginPage`:

##### 4.1.1 Метод для перехода на страницу авторизации

* `navigate()`: Переход на страницу авторизации.

##### 4.1.2 Методы для работы с кнопкой "Войти"

* `check_login_btn_exists()`: Проверка, что кнопка "Войти" отображается на странице.
* `check_login_btn_not_exists()`: Проверка, что кнопка "Войти" не отображается на странице.
* `click_login_btn()`: Нажатие на кнопку "Войти".
* `check_login_btn_disabled()`: Проверка, что кнопка "Войти" отключена.
* `check_login_btn_cursor()`: Проверка, что курсор над кнопкой "Войти" меняется на указатель.
* `check_login_btn_hover_color_change()`: Проверка, кнопка "Войти" имеет стандартный цвет фона (DEFAULT_COLOR), а при наведении курсора меняет цвет на заданный (HOVER_COLOR).

##### 4.1.3 Методы для работы с кнопкой "Подтвердить"

* `check_confirm_btn_exists()`: Проверка, что кнопка "Подтвердить" отображается на странице.
* `check_confirm_btn_not_exists()`: Проверка, что кнопка "Подтвердить" не отображается на странице.
* `click_confirm_btn()`: Нажатие на кнопку "Подтвердить".
* `check_confirm_btn_disabled()`: Проверка, что кнопка "Подтвердить" отключена.
* `check_confirm_btn_cursor()`: Проверка, что курсор над кнопкой "Подтвердить" меняется на указатель.
* `check_confirm_btn_hover_color_change()`: Проверка, что кнопка "Подтвердить" имеет стандартный цвет фона (DEFAULT_COLOR), а при наведении курсора меняет цвет на заданный (HOVER_COLOR).

##### 4.1.4 Методы для работы с полем логина (email)

* `check_email_field_exists()`: Проверка, что поле логина (email) отображается на странице.
* `click_email_field()`: Нажатие на поле логина (email).
* `fill_email_field(text: str)`: Ввод текста в поле логина (email).
* `check_email_field_cursor()`: Проверка, что тип курсора над полем логина (email) меняется на ввод текстовый.

##### 4.1.5 Методы для работы с полем пароля

* `check_pwd_field_exists()`: Проверка, что поле пароля отображается на странице.
* `check_pwd_field_hidden()`: Проверка, что поле пароля скрыто.
* `click_pwd_field()`: Нажатие на поле пароля.
* `fill_pwd_field(text: str)`: Ввод текста в поле пароля.
* `check_pwd_field_cursor()`: Проверка, что тип курсор над полем пароля меняется на текстовый.
* `check_pwd_field_type()`: Проверка, что тип поля пароля - "password".

##### 4.1.6 Методы для работы с полем проверочного кода

* `check_verification_code_field_exists()`: Проверка, что поле проверочного кода отображается на странице.
* `check_verification_code_field_not_exists()`: Проверка, что поле проверочного кода не отображается на странице.
* `click_verification_code_field()`: Нажатие на поле проверочного кода.
* `fill_verification_code_field(text: str)`: Ввод текста в поле проверочного кода.
* `check_verification_code_field_cursor()`: Проверка, что тип курсора над полем проверочного кода меняется на текстовый.

##### 4.1.7 Методы для нажатия Enter

* `press_enter_login_btn()`: Нажатие Enter для кнопки "Войти".
* `press_enter_confirm_btn()`: Нажатие Enter для кнопки "Подтвердить".
* `press_enter_btn_from_login()`: Нажатие Enter в поле логина (email).
* `press_enter_btn_from_pwd()`: Нажатие Enter в поле пароля.
* `press_enter_btn_from_code()`: Нажатие Enter в поле проверочного кода.

##### 4.1.8 Методы для проверки ошибок

* `check_error_text(error: str)`: Проверка, что текст ошибки отображается на странице.

`error`: Текст ошибки, в качестве аргумента передается константа, определенные в файле error_const.py

##### 4.1.9 Методы для вставки текста из буфера обмена

* `paste_text_from_buffer(text: str, type_field: Literal['email', 'password', 'code'])`:

Вставляет текст из буфера обмена в указанное поле на странице авторизации. 

Параметры:
* `text`: Текст, который нужно вставить.
* `type_field`: Тип поля, в которое нужно вставить текст. Допустимые значения:
    * 'email': Поле логина (email)
    * 'password': Поле пароля
    * 'code': Поле проверочного кода

##### 4.1.10 Методы для работы со ссылкой "Забыли пароль?"

* `check_forgot_pwd_link_exists()`: Проверка, что ссылка "Забыли пароль?" отображается на странице.
* `click_forgot_pwd_link()`: Нажатие на ссылку "Забыли пароль?".
* `check_forgot_pwd_link_cursor()`: Проверка, что курсор над ссылкой "Забыли пароль?" меняется на указатель.

##### 4.1.11 Методы для работы с полем SMS-кода

* `check_sms_verification_code_field_exists()`: Проверка, что поле SMS-кода отображается на странице.
* `check_sms_verification_code_field_not_exists()`: Проверка, что поле SMS-кода не отображается на странице.
* `click_sms_verification_code_field()`: Нажатие на поле SMS-кода.
* `fill_sms_verification_code_field(text: str)`: Ввод текста в поле SMS-кода.
* `check_sms_verification_code_field_cursor()`: Проверка, что тип курсора над полем SMS-кода меняется на текстовый.

##### 4.1.12 Методы для работы с полем email-кода

* `check_email_verification_code_field_exists()`: Проверка, что поле email-кода отображается на странице.
* `check_email_verification_code_field_not_exists()`: Проверка, что поле email-кода не отображается на странице.
* `click_email_verification_code_field()`: Нажатие на поле email-кода.
* `fill_email_verification_code_field(text: str)`: Ввод текста в поле email-кода.
* `check_email_verification_code_field_cursor()`: Проверка, что тип курсора над полем email-кода меняется на текстовый.

 
### 5. Примеры использования <a name="5-примеры-использования"></a>

#### 5.1 Базовый сценарий авторизации

```python
from playwright.sync_api import sync_playwright
from pages.login_page import LoginPage

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()
    login_page = LoginPage(page)

    login_page.navigate()
    login_page.fill_email_field("test@example.com")
    login_page.fill_pwd_field("password123")
    login_page.click_login_btn()
```

#### 5.2 Сценарий с двухфакторной аутентификацией

```python
from playwright.sync_api import sync_playwright
from pages.login_page import LoginPage

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()
    login_page = LoginPage(page)

    login_page.navigate()
    login_page.fill_email_field("test@example.com")
    login_page.fill_pwd_field("password123")
    login_page.click_login_btn()

    # Проверка двухфакторной аутентификации
    login_page.check_verification_code_field_exists()
    login_page.fill_verification_code_field("1234")
    login_page.click_confirm_btn()
```

#### 5.3 Сценарий с проверкой ошибок

```python
from playwright.sync_api import sync_playwright
from pages.login_page import LoginPage

from const.error_const import USER_NOT_FOUND

with sync_playwright() as p:
    browser = p.chromium.launch(headless=False)
    page = browser.new_page()
    login_page = LoginPage(page)

    login_page.navigate()
    login_page.fill_email_field("invalid@gmail.com")
    login_page.fill_pwd_field("wrong_password")
    login_page.click_login_btn()

    # Проверка ошибки
    login_page.check_error_text(USER_NOT_FOUND)
```
 
### 6. Файлы констант <a name="6-файлы-констант"></a>

##### 6.1 Файл error_const.py

Содержит константы, представляющие тексты ошибок, которые могут возникать на странице авторизации.
В нем определены следующие константы:
  * USER_NOT_FOUND: Текст ошибки для случая, когда введен неверный логин. Пользователь с таким логином незарегистрирован. 
  * USER_DELETED_OR_BLOCKED: Текст ошибки для случая, когда введен логин, принадлежащий удаленному или заблокированному пользователю.
  * INVALID_CREDENTIALS: Текст ошибки для случая, когда введен неверный пароль.
  * CODE_ALREADY_SENT: Текст ошибки для случая когда код запрашивается повторно, но он уже был отправлен пользователю. 
  * INVALID_CODE: Текст ошибки для случая, когда введен неверный код при двухфакторной аутентификации. 
  * CAPTCHA_MISSING: Текст ошибки для случая, когда производится попытка входа без прохождения CAPTCHA.

##### 6.2 Файл other_const.py

Содержит константы, представляющие различные ограничения и настройки, используемые в коде.
  * MIN_LOGIN_LENGTH: Минимальная допустимая длина логина.
  * MAX_LOGIN_LENGTH: Максимальная допустимая длина логина.
  * MIN_PASSWORD_LENGTH: Минимальная допустимая длина пароля.
  * MAX_PASSWORD_LENGTH: Максимальная допустимая длина пароля.
  * VERIFICATION_CODE_LENGTH: Длина проверочного кода.
  * SMS_CODE_LENGTH: Длина SMS-кода.
  * EMAIL_CODE_LENGTH: Длина email-кода.
  * DEFAULT_COLOR: Цвет фона кнопки до наведения.
  * HOVER_COLOR: Цвет фона кнопки после наведения.

 
### 7. Тестирование с pytest <a name="7-тестирование-с-pytest"></a>

#### 7.1 Теггирование pytest
Pytest предоставляет маркеры для того, чтобы пометить некоторые тесты. Это необходимо для различных целей, например, пропустить выполнение теста по некоторой причине, запустить только те тесты, которые помечены определенным маркером, параметризировать тесты и т.д.
В коде используются следующие маркеры pytest:

• @pytest.mark.skip (встроенный): отмечает тест, который должен быть пропущен. Используются для тестов, функциональность которых еще не реализована.
• @pytest.mark.smoke (кастомный): отмечает тест как дымовой, проверяющий основную функциональность приложения. 

#### 7.2 Фикстуры
В представленных примерах кода виден повторяющийся код, что затрудняет его поддержку и читаемость. Для решения этой проблемы pytest предоставляет механизм фикстур. Фикстуры, которые определяются в файле conftest.py, позволяют извлекать повторяющиеся действия или данные в отдельные функции. Эти функции затем передаются в качестве аргументов в функции тестов и используются для различных целей: создания экземпляров объектов, подготовки тестовой среды, открытия веб-страниц и так далее.

##### 7.2.1 Фикстура login_page

Создает экземпляр класса LoginPage для каждого теста, которому требуются поля и методы этого класса.
• Использование: необходимо передать как аргумент функции теста, например, def test_login_btn_exists(self, login_page). После передачи этой фикстуры будут доступны все методы для взаимодействия с элементами страницы класса.

##### 7.2.2 Фикстура open_page

• Описание: выполняет перемещение на страницу авторизации перед запуском каждого теста, где эта фикстура используется.
• Использование: Используется как параметр функции теста, например, def test_login_btn_exists(self, login_page, open_page).

 
#### 8. Запуск тестов <a name="8-запуск-тестов"></a>

#### 8.1 Запуск тестов

##### 8.1.1 Запуск всех тестов

* **pytest**:  Запускает все тесты по умолчанию на Chromium в headless режиме.
* **pytest --headed**:  Запускает все тесты в режиме headed (с графическим интерфейсом).

##### 8.1.2 Запуск тестов в конкретном модуле

* **pytest test_login.py**:  Запускает тесты только в файле test_login.py.

##### 8.1.3 Запуск набора модулей с тестами

* **pytest tests/test_todo_page.py tests/test_landing_page.py**: Запускает тесты в файлах tests/test_todo_page.py и tests/test_landing_page.py.

##### 8.1.4 Запуск конкретного теста

* **pytest -k test**: Запускает только тесты, чье имя содержит строку "test".

Тесты группируются в классы для улучшения структуры и организации кода. Это позволяет логически разбить тесты по тестируемому элементу, процессу или функциональности, что делает код более читаемым и поддерживаемым.
Для запуска таких тестов в группе или конкретного теста из группы используются команды:

##### 8.1.5 Запуск тестов, объединенных в класс:

pytest tests/test_login_page.py::TestLoginBtn

##### 8.1.6 Запуск конкретного теста из группы:

pytest tests/test_login_page.py::TestLoginBtn::test_login_btn_exists


##### 8.1.7 Вывод подробной информации

* **pytest -v**: Выводит подробную информацию о каждом тесте, включая его имя, метки и результат.

##### 8.1.8 Фильтрация по меткам

* **pytest -m smoke**: Запускает только тесты, отмеченные тегом smoke.
* **pytest -m "not smoke"**: Запускает все тесты, кроме отмеченных тегом smoke.

#### 8.2 Настройка запуска

##### 8.2.1 Выбор браузера

* **pytest --browser chromium**: Запускает тесты на Chromium (по умолчанию).
* **pytest --browser firefox**: Запускает тесты на Firefox.
* **pytest --browser webkit**: Запускает тесты на WebKit.
* **pytest --browser chromium firefox webkit**: Запускает тесты на всех трех браузерах.

##### 8.2.2 Эмуляция устройств

* **pytest --device 'iPhone 13'**: Запускает тесты в режиме эмуляции устройства iPhone 13. 

##### 8.2.3 Замедление выполнения

* **pytest --slowmo 500**: Замедляет операции Playwright на 500 миллисекунд для удобного просмотра выполнения тестов.

#### 8.3 Отладка

##### 8.3.1 Отладка всех тестов


Для отладки всех тестов используется playwright inspector, который вызывается командами:
$env:PWDEBUG=1
pytest -s

##### 8.3.2 Отладка тестов в конкретном модуле

Чтобы отладить один тестовый файл, необходимо выполнить команды, указав за ними имя тестового файла:
$env:PWDEBUG=1
pytest -s test_example.py

##### 8.3.3 Отладка конкретного теста

Для отладки конкретного теста необходим указать флаг -k
$env:PWDEBUG=1
pytest -s -k function

