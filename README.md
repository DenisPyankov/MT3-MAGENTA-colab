1. Что использовано 
  - pretty_midi — основная работа с MIDI                 
  - mido — fallback для битых файлов 
  - symusic (опционально) — доп. проверка загрузки                    
  - стандартные библиотеки (os, csv, и т.д.)                            

2. Зачем использовано
  - pretty_midi → удобно читать/редактировать ноты
  - mido → спасает, если MIDI повреждён
  - symusic → дополнительная устойчивость
  - остальное → обход файлов и запись отчёта

3. Как использовано
  - загрузка MIDI (с fallback)
  - проход по всем инструментам и нотам
  очистка:
    - квантование времени
    - удаление дублей
    - исправление длительности
    - устранение overlap
    - нормализация pitch/velocity
    - чистка CC и pitch bend
    - удаление пустых треков
    - сохранение нового MIDI

4. Какой продукт на выходе
  очищенные MIDI:
  - *_script_clean.mid
  CSV-отчёт:
  - статистика всех исправлений

## 🔧 Постобработка midi после МТ3 с помощью скрипта

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](
https://colab.research.google.com/github/DenisPyankov/MT3-MAGENTA-colab/blob/denkuls/MT3_batch_plus_script_postprocessing.ipynb
)

