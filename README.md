


## 🔧 Public fixed version (MT3 only)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/DenisPyankov/MT3-MAGENTA-colab/blob/MT3_only-(colab_fix)/Music_Transcription_with_Transformers.ipynb)

Создатели: https://github.com/magenta/mt3


## 🎹 Main project (piano transcription)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/DenisPyankov/MT3-MAGENTA-colab/blob/main/colab/Music_Transcription_with_Transformers.ipynb)

В основе проекта лежит модель **MT3 (Music Transcription with Transformers)** от Google Magenta для автоматической транскрипции аудио любой сложности в фортепианную партитуру (MIDI).

---

## Архитектура пайплайна

graph LR
    A[🎵 Входное аудио<br/>любой сложности] --> B[🔊 Предобработка<br/>Voice Separation]
    B -->|Demucs v4| C[🎹 Чистый инструментал]
    C --> D[🤖 MT3 Magenta<br/>Audio-to-MIDI]
    D --> E[🎼 Постобработка<br/>очистка, редукция]
    E --> F[📜 Выходной MIDI]

---

## Предобработка аудио (Preprocessing) 

Для повышения качества транскрипции в тестовой версии пайплайна реализован этап предварительной обработки аудио.

Перед подачей в MT3 исходный трек обрабатывается моделью **Demucs v4 (htdemucs)**.
- **Изоляция инструментала:** Из аудио вычленяется вокальная партия, на выходе получается чистая инструментальная дорожка.
- **Транскрипция:** Обработанное аудио передается в MT3, что упрощает анализ и повышает точность генерации фортепианной партитуры.

🔗 [Сравнение моделей разделения вокала](https://docs.google.com/spreadsheets/d/1iKQ7BKZoSfRc9aWAUW3QznHCmRQg3rtQk7b75PRZ3I8/edit?usp=sharing) 










