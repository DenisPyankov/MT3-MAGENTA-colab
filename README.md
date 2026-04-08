1. Что использовано                                                  2. Зачем использовано
  pretty_midi — основная работа с MIDI                                 - pretty_midi → удобно читать/редактировать ноты                     
  mido — fallback для битых файлов                                     - mido → спасает, если MIDI повреждён
  symusic (опционально) — доп. проверка загрузки                       - symusic → дополнительная устойчивость
  стандартные библиотеки (os, csv, и т.д.)                             - остальное → обход файлов и запись отчёта

3. Как использовано                                                  4. Какой продукт на выходе
  - загрузка MIDI (с fallback)                                       очищенные MIDI:
  - проход по всем инструментам и нотам                                - *_script_clean.mid
  очистка:                                                           CSV-отчёт:
    - квантование времени                                              - статистика всех исправлений
    - удаление дублей
    - исправление длительности
    - устранение overlap
    - нормализация pitch/velocity
    - чистка CC и pitch bend
    - удаление пустых треков
    - сохранение нового MIDI

## 🔧 Постобработка midi после МТ3 с помощью скрипта

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](
https://colab.research.google.com/github/DenisPyankov/MT3-MAGENTA-colab/blob/denkuls/MT3_batch_plus_script_postprocessing.ipynb
)

