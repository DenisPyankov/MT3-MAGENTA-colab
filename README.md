


## 🔧 Public fixed version (MT3 only)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/DenisPyankov/MT3-MAGENTA-colab/blob/MT3_only-(colab_fix)/Music_Transcription_with_Transformers.ipynb)

Создатели: https://github.com/magenta/mt3


## 🎹 Main project (piano transcription)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/DenisPyankov/MT3-MAGENTA-colab/blob/main/colab/Music_Transcription_with_Transformers.ipynb)

В основе проекта лежит модель **MT3 (Music Transcription with Transformers)** от Google Magenta для автоматической транскрипции аудио любой сложности в фортепианную партитуру (MIDI).

---

## Архитектура пайплайна

```mermaid
graph LR
    A[🎵 Входное аудио<br/>любой сложности] --> B[🔊 Предобработка<br/>Voice Separation]
    B -->|Demucs v4| C[🎹 Чистый инструментал]
    C --> D[🤖 MT3 Magenta<br/>Audio-to-MIDI]
    D --> E[🎼 Постобработка<br/>очистка, редукция]
    E --> F[📜 Выходной MIDI]
```

---

## Предобработка аудио (Preprocessing) 

Для повышения качества транскрипции в тестовой версии пайплайна реализован этап предварительной обработки аудио.

Перед подачей в MT3 исходный трек обрабатывается моделью **Demucs v4 (htdemucs)**.
- **Изоляция инструментала:** Из аудио вычленяется вокальная партия, на выходе получается чистая инструментальная дорожка.
- **Транскрипция:** Обработанное аудио передается в MT3, что упрощает анализ и повышает точность генерации фортепианной партитуры.

🔗 [Сравнение моделей разделения вокала](https://docs.google.com/spreadsheets/d/1iKQ7BKZoSfRc9aWAUW3QznHCmRQg3rtQk7b75PRZ3I8/edit?usp=sharing) 


---

## Основной модуль: MT3-Magenta

🔑 **Ключевая особенность:**

- **Работа с любым мультиинструментальным аудио** – в отличие от других моделей (Basic Pitch, Pop2Piano, ByteDance, IZMIR2021), которые **ограничены соло-фортепиано**, MT3 способна транскрибировать оркестровые записи, выделяя ноты разных инструментов.
- **Стабильно узнаваемый результат** – даже при неидеальной точности (ложные ноты) выходной MIDI сохраняет **мелодический и гармонический контур оригинала**, что делает его пригодным для постобработки и редукции в фортепианную партитуру.

🔗 [**Сравнение моделей Audio-to-MIDI**](https://docs.google.com/spreadsheets/d/1qiju_Q1Xj7APl7R3Ri5ewP2bYcmp1dgCHuN8-_sx1_w/edit?usp=sharing) - MT3 — единственная, кто «переваривает» сложное аудио и даёт узнаваемый результат.


📊 [**Скрипты оценки качества MIDI**](https://colab.research.google.com/drive/19Vvgum7gqxq_MubIR6oZqkWO8VGxqpWL?usp=sharing) - ноутбук с реализацией критериев сравнения предсказанного MIDI с эталоном (F1, Polyphony, Finger span и др.), а также вспомогательные утилиты для анализа MIDI-файлов.

🎵 [**Датасет для сравнения моделей**](https://disk.yandex.ru/d/Qh9SlqF_sS_c3g/%D0%A2%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0%201%20-%20%D0%A1%D1%80%D0%B0%D0%B2%D0%BD%D0%B8%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F%20%D1%85%D0%B0%D1%80%D0%B0%D0%BA%D1%82%D0%B5%D1%80%D0%B8%D1%81%D1%82%D0%B8%D0%BA%D0%B0%20%D0%BC%D0%BE%D0%B4%D0%B5%D0%BB%D0%B5%D0%B9) + включает предсказания MT3 и IZMIR2021 (и др.), а также сконвертированные в аудио версии предсказаний для удобного прослушивания и экспертной оценки.

---

## Постобработка MIDI

технологии: 

- pretty_midi — основная работа с MIDI
- mido — fallback для битых файлов
- symusic (опционально) — доп. проверка загрузки
- стандартные библиотеки (os, csv, и т.д.)

алгоритм:

1. загрузка MIDI (с fallback)
2. проход по всем инструментам и нотам
3. очистка:
    - квантование времени
    - удаление дублей
    - исправление длительности
    - устранение overlap
    - нормализация pitch/velocity
    - чистка CC и pitch bend
    - удаление пустых треков
4. сохранение нового MIDI

---

## БЕНЧМАРК [COMING SOON]

*TO DO*
- разделы, цели, ресурсы
- ссыль на бенч/архив
- ссыль на таблицу с резами 








