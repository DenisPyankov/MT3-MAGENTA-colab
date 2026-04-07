


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

---

## Постобработка MIDI

aboba

---

## БЕНЧМАРК

разделы, для чего?









