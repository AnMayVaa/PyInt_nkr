# PyInt — Intermediate Python Course

Teaching materials for a 2-day **Intermediate Python** class. Each topic has three Jupyter notebooks, plus a Markdown export of each:

- **content**: the lesson and examples
- **practice**: guided practice
- **exercise**: problems to solve on your own

## Syllabus

### Day 1

| # | Topic | Folder |
|---|---|---|
| 01 | Exceptions & error handling (`try` / `except` / `else` / `finally`, raising errors) | `day1/01_PyInt_ErrorExceptHand` |
| 02–03 | File handling (text files, JSON) | `day1/02n03_PyInt_FileHand` |

### Day 2

| # | Topic | Folder |
|---|---|---|
| 04 | OOP basics: classes & objects | `day2/04_PyInt_ClsObj` |
| 05 | OOP: inheritance | `day2/05_PyInt_Inher` |
| 06 | **Workshop: MMORPG text adventure.** Build a terminal game with a character creator plus two of: save/load, inventory & shop, monster battle, quest log | `day2/06_PyInt_MMOworkshop` |
| 07 | **Python in the Wild.** A run-only demo of pandas data analysis, matplotlib charts and MediaPipe/OpenCV computer vision | `day2/07_PyInt_PyInWild` |

## Getting started

```bash
pip install jupyter
jupyter notebook
```

Notebook 07 also needs:

```bash
pip install pandas matplotlib mediapipe opencv-python
```

Sample data files (`contacts.json`, `scores.txt`, `save.json`, and others) sit next to the notebooks that use them.
