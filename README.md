
## Инструкция по запуску тестов Playwright

Playwright тесно интегрирован с фреймворком pytest, поэтому для запуска тестов можно использовать классические команды pytest, а также некоторые дополнительные, определенные в плагине pytest.

### Основные консольные команды для Playwright

#### Установка и обновление

- **Установка плагина pytest и Playwright:**  
  `pip install pytest-playwright`
  
- **Установка необходимых браузеров:**  
  `playwright install`
  
- **Обновление Playwright до последней версии:**  
  `pip install pytest-playwright playwright -U`

#### Запуск тестов

- **Запуск всех тестов (по умолчанию на Chromium в headless режиме):**  
  `pytest`
  
- **Запуск тестов в конкретном модуле:**  
  `pytest test_login.py`
  
- **Запуск набора модулей с тестами:**  
  `pytest tests/test_todo_page.py tests/test_landing_page.py`
  
- **Запуск конкретного теста:**  
  `pytest -k function`

#### Флаги для плагина pytest

- **`--headed`:**  
  Запуск тестов в режиме headed (видимый браузер) (по умолчанию: headless).
  
- **`--browser`:**  
  Запуск тестов в другом браузере (chromium, firefox, или webkit). Можно указать несколько браузеров (по умолчанию: chromium).
  
- **`--slowmo`:**  
  Замедляет операции Playwright на указанное количество миллисекунд. Полезно для просмотра выполнения тестов (по умолчанию: 0).
  
- **`--device`:**  
  Устройство для эмуляции (доступен широкий выбор устройств, в том числе и мобильные).

**Пример:**

` pytest test_login.py --browser webkit --browser firefox --headed `

` pytest test_login.py --device='iPhone 13' `



### Отладка

Для отладки тестов используется Playwright Inspector, который вызывается командами:  

* Отладка всех тестов:
` $env:PWDEBUG=1

pytest -s `

* Отладка одного тестового файла:
` $env:PWDEBUG=1
pytest -s test_example.py `

* Отладка конкретного теста:
` $env:PWDEBUG=1
pytest -s -k function `
