# AE — Assistant for an Engineer

[![Version](https://img.shields.io/badge/version-0.7.0--beta-yellow)]()
[![License: MIT](https://img.shields.io/badge/license-MIT-blue)]()
[![Platform](https://img.shields.io/badge/platform-Windows%2010%2B-lightgrey)]()
[![Language](https://img.shields.io/badge/interface-%D1%80%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9-red)]()
[![Offline](https://img.shields.io/badge/offline-100%25-green)]()

> 🧪 **Бета-версия 0.7.0.** Функционал стабилен, но структура базы
> статей, API и формат профилей судов могут меняться до релиза 1.0.0.

**AE** — портативный офлайн-справочник для судовых механиков, электриков
и инженеров. База статей, формулы с расчётом и калькулятор в одном окне.
Работает полностью автономно — без интернета, регистрации и телеметрии.

> _English: AE is a portable offline reference for marine engineers —
> articles, formulas and a calculator in one window. Runs fully offline,
> no telemetry. Interface is currently Russian; English UI is planned._

---

## Возможности

- **Поиск по базе** — 355+ статей в 12 разделах (морские термины,
  электротехника, физика, геометрия, расчёты, справочные материалы,
  СЭУ, судовые системы, электроэнергетика, сокращения, материалы,
  прикладные расчёты).
- **Полнотекстовый поиск** на SQLite FTS5: работает по названию,
  алиасам, английским названиям и ключевым словам.
- **Калькулятор формул**: `найти ток если U=220 В, R=10 Ом` → `I = 22 А`.
- **Конвертер единиц**: `5 метров в футы` → `16.404 м`.
- **Арифметика**: `2+2`, `2^10`, `(2+3)*4`.
- **Справочные таблицы** с фильтрацией по запросу: «плотность стали»
  покажет строку «Сталь — 7800» из таблицы плотностей.
- **Профили судов** — карточки судов с сохранением в JSON рядом с
  программой (переносимы между компьютерами).
- **Мета-вопросы**: «сколько времени», «какая версия», «заряд батареи»,
  «диагностика».
- **Темная и светлая темы**, история запросов, избранное.

## Скриншоты

_Появятся в ближайших релизах. Пока — соберите и запустите._

## Требования к системе

- **Windows 10** (версия 1809 или новее) или **Windows 11**, 64-бит.
- **Microsoft Edge WebView2 Runtime.** На Windows 11 и большинстве
  обновлённых Windows 10 предустановлен. Если нет — установщик идёт
  в комплекте с релизом, либо скачайте по ссылке
  [Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=2124703).
- Свободное место: **~100 МБ** (программа + база статей).
- **Интернет не требуется.**

## Установка и запуск

### Готовая сборка

1. Скачайте `AE-v0.7.0-win64.zip` из раздела
   [Releases](https://github.com/SantidioEsanti/ae/releases).
2. Распакуйте архив целиком в любую папку (например, на флешку).
3. Запустите `AE.exe`.
4. При первом запуске рядом появится папка `userdata/` — настройки,
   профили судов, история и избранное.

> ⚠️ Не запускайте `AE.exe` прямо из архива — распакуйте сначала.
> На старых Windows может потребоваться установить WebView2 Runtime —
> запустите `MicrosoftEdgeWebView2RuntimeInstallerX64.exe` из папки
> с программой.

### Сборка из исходников

```bat
:: 1) Клонировать
git clone https://github.com/SantidioEsanti/ae.git
cd ae

:: 2) Виртуальное окружение (Python 3.11 / 3.12 / 3.13)
py -3.12 -m venv .venv
.venv\Scripts\activate

:: 3) Зависимости
pip install -r requirements.txt
pip install pyinstaller pythonnet

:: 4) Патч main.py (переход на WebView2) + README.txt
python patch_to_edge.py

:: 5) Сборка
python build.py --download-webview2
