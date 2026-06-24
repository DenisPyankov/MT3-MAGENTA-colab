
# 🎹 Фортепианная транскрипция из любого аудио

Превратите любую песню или запись в фортепианную MIDI‑партитуру одной кнопкой – всё происходит в облаке, вам не нужно ничего устанавливать.

<a href="https://colab.research.google.com/github/DenisPyankov/MT3-MAGENTA-colab/blob/main/colab/PIANO_TRANSCRIPTION.ipynb" target="_blank">
  <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab" width="400" height="auto">
</a>

## 📥 Как пользоваться

1. **Нажмите на большую кнопку выше** – откроется Google Colab.  
2. Запустите **ПЕРВУЮ ячейку** `«УСТАНОВКА»`: нажмите кнопку ▶ слева от неё.  
   *Идёт установка и загрузка модели – это займёт 5‑7 минут. Дождитесь зелёной галочки.*  
3. Запустите **ВТОРУЮ ячейку** `«ПУСК»`: нажмите ▶.  
   *Появится кнопка для выбора файла с вашего компьютера.*  
4. Загрузите аудиофайл (MP3 или WAV) – всё остальное произойдёт автоматически.
5. Через несколько минут браузер сохранит готовый MIDI‑файл.  
6. **Готово!**


------
------
------

# ***ДЛЯ РАЗРАБОТЧИКОВ***

---


## GRADIO

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/DenisPyankov/MT3-MAGENTA-colab/blob/main/colab/GRADIO.ipynb)

- запустить блоки по порядку
- в последнем блоке ссылка с фронтендом

----

## 🔧 Public fixed version (MT3 only)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/DenisPyankov/MT3-MAGENTA-colab/blob/MT3_only-(colab_fix)/Music_Transcription_with_Transformers.ipynb)

Создатели: https://github.com/magenta/mt3

---

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

## [**БЕНЧМАРК**](https://disk.yandex.ru/d/Qh9SlqF_sS_c3g)


собранный [**датасет для сравнения моделей**](https://disk.yandex.ru/d/Qh9SlqF_sS_c3g/%D0%A2%D0%B0%D0%B1%D0%BB%D0%B8%D1%86%D0%B0%201%20-%20%D0%A1%D1%80%D0%B0%D0%B2%D0%BD%D0%B8%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D0%B0%D1%8F%20%D1%85%D0%B0%D1%80%D0%B0%D0%BA%D1%82%D0%B5%D1%80%D0%B8%D1%81%D1%82%D0%B8%D0%BA%D0%B0%20%D0%BC%D0%BE%D0%B4%D0%B5%D0%BB%D0%B5%D0%B9) – 10 audio;

готовые датасеты: 
- [**midi вокал**](https://disk.yandex.ru/d/Qh9SlqF_sS_c3g/Midi%20%D0%B2%D0%BE%D0%BA%D0%B0%D0%BB) 20,
- [**оркестр**](https://disk.yandex.ru/d/Qh9SlqF_sS_c3g/Midi%20%D1%81%20%D0%BE%D1%80%D0%BA%D0%B5%D1%81%D1%82%D1%80%D0%BE%D0%BC) 40+,
-  [**solo piano**](https://disk.yandex.ru/d/Qh9SlqF_sS_c3g/Solo%20piano) 120+ (audio+GT midi),
-  [**оркестр без фортепиано**](https://disk.yandex.ru/d/Qh9SlqF_sS_c3g/%D0%9E%D1%80%D0%BA%D0%B5%D1%81%D1%82%D1%80%20%D0%B1%D0%B5%D0%B7%20%D0%BF%D0%B8%D0%B0%D0%BD%D0%B8%D0%BD%D0%BE%20) 20;

[**синтетика Suno**](https://disk.yandex.ru/d/Qh9SlqF_sS_c3g/%D0%A1%D0%B8%D0%BD%D1%82%D0%B5%D1%82%D0%B8%D0%BA%D0%B0%20Suno%20) – 256 audio;

[**midi фортепиано и вариации**](https://disk.yandex.ru/d/1iAZdbDoF_pAfQ/piano) (reverb, telephone, noise_clipping, reverb_gating, codec_dropout, distortion, chorus) – 30 audio (по 8 вариаций);

[**песни и вариации**](https://disk.yandex.ru/d/1iAZdbDoF_pAfQ/songs) – 10 audio (по 8 вариаций);

[**набор нот**](https://disk.yandex.ru/d/1iAZdbDoF_pAfQ/random) (midi + wav) – 10 пар;

аудиофрагменты [**поп-музыка**](https://disk.yandex.ru/d/WPkTokZTosJ74g), [**вокал с фортепиано**](https://disk.yandex.ru/d/ai1KK9yWEp3oKA/%D0%92%D0%BE%D0%BA%D0%B0%D0%BB), [**оркестр**](https://disk.yandex.ru/d/ai1KK9yWEp3oKA/%D0%A1%D0%BB%D0%BE%D0%B6%D0%BD%D1%8B%D0%B5) – 60+ audio.

**Итог:** более 500 файлов, каждый набор предназначен под определенный ряд проверок

[**ТАБЛИЦЫ С АНАЛИЗОМ**](https://docs.google.com/spreadsheets/d/1qiju_Q1Xj7APl7R3Ri5ewP2bYcmp1dgCHuN8-_sx1_w/edit?gid=1447608768#gid=1447608768)








