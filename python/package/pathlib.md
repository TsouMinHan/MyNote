# pathlib

在每個作業系統上路徑的寫法都不一樣 為了避免這個問題，盡量不要用下面這樣子的方法寫

```python
path = 'folder/' + 'fileName'
```

可以用 `os.path.join`，但是很長一串，懶得用 ...  
所以可以用 `pathlib` 這個套件

```python
from pathlib import Path

data_folder = Path("source_data/text_files/")

file_to_open = data_folder / "raw_data.txt"

f = open(file_to_open)

print(f.read())

# 不用open也可讀檔
print(file_to_open.read_text())
```

## 一些屬性跟方法

```python
from pathlib import Path

filename = Path("source_data/text_files/raw_data.txt")

print(filename.name)
# prints "raw_data.txt"

print(filename.suffix)
# prints "txt"

print(filename.stem)
# prints "raw_data"

if not filename.exists():
    print("Oops, file doesn't exist!")
else:
    print("Yay, the file exists!")
```

