# 第 9 章｜檔案操作

## 學習目標

- 理解檔案操作的概念
- 掌握文字檔的讀寫方法
- 學會使用 JSON 格式
- 能夠處理二進制檔案

---

> **⚠️ Caution（注意）**：使用完檔案後務必關閉檔案，或者使用 `with` 語句自動管理，這樣可以確保資料正確寫入並釋放系統資源。

## 9.1 檔案操作基礎

### 開啟檔案

```python
# 開啟檔案
file = open("file.txt", "r")  # r = 讀取模式
# 使用檔案...
file.close()

# 較好的方式：with 語句（自動關閉）
with open("file.txt", "r") as file:
    # 使用檔案
    pass  # 執行完會自動關閉
```

### 檔案模式

| 模式 | 說明 |
|------|------|
| `r` | 讀取（預設） |
| `w` | 寫入（覆蓋） |
| `a` | 附加（末尾新增） |
| `x` | 創建（新檔案） |
| `r+` | 讀寫 |
| `b` | 二進制模式（如 `rb`, `wb`） |

---

## 9.2 讀取檔案

### 讀取全部內容

```python
with open("file.txt", "r", encoding="utf-8") as file:
    content = file.read()
    print(content)
```

### 讀取一行

```python
with open("file.txt", "r", encoding="utf-8") as file:
    line = file.readline()
    print(line)
```

### 讀取所有行

```python
with open("file.txt", "r", encoding="utf-8") as file:
    lines = file.readlines()
    for i, line in enumerate(lines, 1):
        print(f"{i}: {line.strip()}")
```

### 迴圈逐行讀取

```python
with open("file.txt", "r", encoding="utf-8") as file:
    for line in file:
        print(line.strip())
```

---

## 9.3 寫入檔案

### 寫入文字

```python
# 覆蓋寫入
with open("output.txt", "w", encoding="utf-8") as file:
    file.write("第一行\n")
    file.write("第二行\n")

# 附加寫入
with open("output.txt", "a", encoding="utf-8") as file:
    file.write("第三行\n")
```

### 寫入多行

```python
lines = ["第一行", "第二行", "第三行"]

with open("output.txt", "w", encoding="utf-8") as file:
    for line in lines:
        file.write(line + "\n")

# 或使用 writelines
with open("output.txt", "w", encoding="utf-8") as file:
    file.writelines(line + "\n" for line in lines)
```

---

## 9.4 JSON 格式

### 什麼是 JSON？

**JSON（JavaScript Object Notation）** 是一種輕量級的資料交換格式，廣泛用於 API 和資料儲存。

```json
{
    "name": "小明",
    "age": 20,
    "scores": [85, 90, 78],
    "passed": true
}
```

### 使用 JSON

```python
import json

# Python 物件轉 JSON
data = {
    "name": "小明",
    "age": 20,
    "scores": [85, 90, 78],
    "passed": True
}

# 轉為 JSON 字串
json_str = json.dumps(data, ensure_ascii=False, indent=2)
print(json_str)

# 寫入檔案
with open("data.json", "w", encoding="utf-8") as f:
    json.dump(data, f, ensure_ascii=False, indent=2)
```

### 讀取 JSON

```python
# 從字串讀取
json_str = '{"name": "小明", "age": 20}'
data = json.loads(json_str)
print(data["name"])  # 小明

# 從檔案讀取
with open("data.json", "r", encoding="utf-8") as f:
    data = json.load(f)
    print(data)
```

---

## 9.5 CSV 檔案

### 讀取 CSV

```python
import csv

with open("data.csv", "r", encoding="utf-8") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)  # 每行是一個串列

# 讀取為字典
with open("data.csv", "r", encoding="utf-8") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row["name"], row["age"])
```

### 寫入 CSV

```python
import csv

# 寫入資料
data = [
    ["姓名", "年齡", "科系"],
    ["小明", "20", "資工系"],
    ["小華", "21", "電機系"]
]

with open("output.csv", "w", encoding="utf-8", newline="") as f:
    writer = csv.writer(f)
    writer.writerows(data)
```

---

## 9.6 Turtle 繪圖：儲存和讀取圖形

學會了檔案操作，我們可以把畫好的圖形儲存到檔案中，也可以從檔案讀取圖形資料來畫圖！

### 將座標儲存到檔案

```python
import turtle
import json

# 畫一個正方形，把座標記錄下來
points = []
turtle.speed(0)

# 紀錄移動過的路徑
def record_position():
    x, y = turtle.pos()
    points.append((round(x, 2), round(y, 2)))

# 畫正方形並記錄
for i in range(4):
    turtle.forward(100)
    turtle.right(90)
    record_position()

# 把座標存到檔案
with open("square.json", "w", encoding="utf-8") as f:
    json.dump(points, f)

print(f"已儲存 {len(points)} 個座標點到 square.json")

turtle.done()
```

### 從檔案讀取座標畫圖

```python
import turtle
import json

# 從檔案讀取座標
with open("square.json", "r", encoding="utf-8") as f:
    points = json.load(f)

# 依序移動到每個點
turtle.penup()
turtle.goto(points[0])
turtle.pendown()

for point in points:
    turtle.goto(point)

# 連回起點
turtle.goto(points[0])

turtle.done()
```

### 儲存多個圖形

```python
import turtle
import json

shapes = []

# 畫第一個圖形 - 三角形
turtle.begin_fill()
for i in range(3):
    turtle.forward(80)
    turtle.right(120)
turtle.end_fill()
temp_shapes = {
    "type": "triangle",
    "color": "red",
    "position": list(turtle.pos())
}
shapes.append(temp_shapes)

# 畫第二個圖形 - 圓形
turtle.penup()
turtle.goto(150, 0)
turtle.pendown()
turtle.begin_fill()
turtle.circle(40)
turtle.end_fill()
temp_shapes = {
    "type": "circle",
    "color": "blue",
    "position": list(turtle.pos())
}
shapes.append(temp_shapes)

# 儲存到檔案
with open("shapes.json", "w", encoding="utf-8") as f:
    json.dump(shapes, f, indent=2)

print("圖形資料已儲存！")

turtle.done()
```

### 練習：畫圖產生器

```python
import turtle

# 讓使用者輸入圖形參數
shape = input("你要畫什麼？(circle/square/triangle): ")
x = int(input("X 座標："))
y = int(input("Y 座標："))
color = input("顏色：")

# 存到檔案
data = {
    "shape": shape,
    "position": [x, y],
    "color": color
}

with open("my_shape.json", "w") as f:
    json.dump(data, f)

# 讀取並畫圖
with open("my_shape.json", "r") as f:
    data = json.load(f)

turtle.penup()
turtle.goto(data["position"][0], data["position"][1])
turtle.pendown()
turtle.color(data["color"])

if data["shape"] == "circle":
    turtle.circle(50)
elif data["shape"] == "square":
    for i in range(4):
        turtle.forward(100)
        turtle.right(90)
elif data["shape"] == "triangle":
    for i in range(3):
        turtle.forward(100)
        turtle.right(120)

turtle.done()
```

---

## 9.7 實用範例

### 範例1：記事本

```python
filename = "note.txt"

# 讀取現有內容
try:
    with open(filename, "r", encoding="utf-8") as f:
        content = f.read()
except FileNotFoundError:
    content = ""

# 顯示目前內容
print("目前的記事：")
print(content)

# 新增內容
new_note = input("\n請輸入新記事：")
with open(filename, "a", encoding="utf-8") as f:
    f.write(new_note + "\n")

print("已儲存！")
```

### 範例2：成績登錄系統

```python
import json

def load_scores():
    try:
        with open("scores.json", "r", encoding="utf-8") as f:
            return json.load(f)
    except FileNotFoundError:
        return {}

def save_scores(scores):
    with open("scores.json", "w", encoding="utf-8") as f:
        json.dump(scores, f, ensure_ascii=False, indent=2)

def add_score():
    scores = load_scores()
    name = input("學生姓名：")
    score = input("成績：")
    scores[name] = score
    save_scores(scores)
    print(f"已儲存 {name} 的成績")

def show_scores():
    scores = load_scores()
    print("\n=== 成績單 ===")
    for name, score in scores.items():
        print(f"{name}: {score} 分")

# 主程式
while True:
    print("\n1. 新增成績 2. 顯示成績 3. 離開")
    choice = input("請選擇：")
    
    if choice == "1":
        add_score()
    elif choice == "2":
        show_scores()
    elif choice == "3":
        break
```

---

## 本章小結

| 語法 | 說明 |
|------|------|
| `open("file", "r")` | 開啟檔案讀取 |
| `open("file", "w")` | 開啟檔案寫入（覆蓋） |
| `open("file", "a")` | 開啟檔案附加 |
| `file.read()` | 讀取全部 |
| `file.readline()` | 讀取一行 |
| `json.dump()` | 寫入 JSON |
| `json.load()` | 讀取 JSON |

---

## 9.7 實用範例 - 小遊戲

### 遊戲 1：日記系統

使用檔案儲存的日記程式！

```python
# 日記系統
# 學習重點：檔案讀寫、JSON 儲存

import json
import os
from datetime import datetime

DIARY_FILE = "my_diary.json"

def load_diary():
    """載入日記"""
    if os.path.exists(DIARY_FILE):
        with open(DIARY_FILE, "r", encoding="utf-8") as f:
            return json.load(f)
    return {}

def save_diary(diary):
    """儲存日記"""
    with open(DIARY_FILE, "w", encoding="utf-8") as f:
        json.dump(diary, f, ensure_ascii=False, indent=2)

def write_diary(diary):
    """寫入日記"""
    date = datetime.now().strftime("%Y-%m-%d")
    print(f"日期：{date}")
    
    content = input("今天發生什麼事？\n")
    
    diary[date] = content
    save_diary(diary)
    print("✅ 日記已儲存！")

def read_diary(diary):
    """閱讀日記"""
    if not diary:
        print("日記是空的！")
        return
    
    print("\n===== 你的日記 =====")
    for date, content in sorted(diary.items(), reverse=True):
        print(f"\n【{date}】")
        print(content)
    print("\n===================")

def search_diary(diary):
    """搜尋日記"""
    keyword = input("輸入搜尋關鍵字：")
    
    found = False
    for date, content in diary.items():
        if keyword in content:
            print(f"\n【{date}】")
            print(content)
            found = True
    
    if not found:
        print("沒有找到符合的日記！")

def delete_diary(diary):
    """刪除日記"""
    date = input("輸入要刪除的日期 (YYYY-MM-DD)：")
    
    if date in diary:
        confirm = input(f"確定要刪除 {date} 的日記嗎？(y/n)：")
        if confirm.lower() == "y":
            del diary[date]
            save_diary(diary)
            print("✅ 已刪除！")
    else:
        print("找不到該日期的日記！")

# 主程式
print("=" * 50)
print("        📔 我的日記系統 📔")
print("=" * 50)

diary = load_diary()

while True:
    print("\n選項：")
    print("1. 寫日記")
    print("2. 閱讀日記")
    print("3. 搜尋日記")
    print("4. 刪除日記")
    print("0. 離開")
    
    choice = input("選擇：")
    
    if choice == "1":
        write_diary(diary)
    elif choice == "2":
        read_diary(diary)
    elif choice == "3":
        search_diary(diary)
    elif choice == "4":
        delete_diary(diary)
    elif choice == "0":
        print("感謝使用！")
        break
    else:
        print("無效的選擇！")
```

---

### 遊戲 2：成績管理系統

使用 CSV 儲存的學生成績系統！

```python
# 成績管理系統
# 學習重點：CSV 讀寫、JSON 備份

import csv
import json
import os
from datetime import datetime

SCORES_FILE = "scores.csv"
BACKUP_FILE = "scores_backup.json"

def load_scores():
    """載入成績"""
    scores = {}
    if os.path.exists(SCORES_FILE):
        with open(SCORES_FILE, "r", encoding="utf-8") as f:
            reader = csv.reader(f)
            next(reader)  # 跳過標題
            for row in reader:
                if len(row) >= 3:
                    scores[row[0]] = {
                        "name": row[1],
                        "score": int(row[2])
                    }
    return scores

def save_scores(scores):
    """儲存成績"""
    with open(SCORES_FILE, "w", encoding="utf-8", newline="") as f:
        writer = csv.writer(f)
        writer.writerow(["學號", "姓名", "成績"])
        for sid, data in scores.items():
            writer.writerow([sid, data["name"], data["score"]])

def backup_scores(scores):
    """備份到 JSON"""
    backup_data = {
        "timestamp": datetime.now().isoformat(),
        "scores": scores
    }
    with open(BACKUP_FILE, "w", encoding="utf-8") as f:
        json.dump(backup_data, f, ensure_ascii=False, indent=2)
    print("✅ 備份完成！")

def add_score(scores):
    """新增成績"""
    sid = input("學號：")
    name = input("姓名：")
    score = int(input("成績："))
    
    scores[sid] = {"name": name, "score": score}
    save_scores(scores)
    print("✅ 新增成功！")

def show_scores(scores):
    """顯示成績"""
    if not scores:
        print("沒有成績資料！")
        return
    
    print("\n===== 成績單 =====")
    print(f"{'學號':<10} {'姓名':<15} {'成績':<10}")
    print("-" * 35)
    
    # 排序顯示
    sorted_scores = sorted(scores.values(), key=lambda x: x["score"], reverse=True)
    
    for i, data in enumerate(sorted_scores, 1):
        print(f"{i:<10} {data['name']:<15} {data['score']:<10}")
    
    # 統計
    scores_list = [data["score"] for data in scores.values()]
    avg = sum(scores_list) / len(scores_list)
    print("-" * 35)
    print(f"平均：{avg:.1f} 分")
    print("===================")

def search_score(scores):
    """查詢成績"""
    keyword = input("輸入學號或姓名：")
    
    for sid, data in scores.items():
        if keyword == sid or keyword in data["name"]:
            print(f"學號：{sid}，姓名：{data['name']}，成績：{data['score']}")

def delete_score(scores):
    """刪除成績"""
    sid = input("輸入學號：")
    
    if sid in scores:
        confirm = input(f"確定要刪除 {scores[sid]['name']} 的成績嗎？(y/n)：")
        if confirm.lower() == "y":
            del scores[sid]
            save_scores(scores)
            print("✅ 刪除成功！")
    else:
        print("找不到該學號！")

# 主程式
print("=" * 50)
print("     📊 成績管理系統 📊")
print("=" * 50)

scores = load_scores()

while True:
    print("\n選項：")
    print("1. 新增成績")
    print("2. 顯示成績")
    print("3. 查詢成績")
    print("4. 刪除成績")
    print("5. 備份資料")
    print("0. 離開")
    
    choice = input("選擇：")
    
    if choice == "1":
        add_score(scores)
    elif choice == "2":
        show_scores(scores)
    elif choice == "3":
        search_score(scores)
    elif choice == "4":
        delete_score(scores)
    elif choice == "5":
        backup_scores(scores)
    elif choice == "0":
        print("感謝使用！")
        break
    else:
        print("無效的選擇！")
```

---

## 9.8 本章小結

### 基礎題

1. **檔案讀取**：讀取一個文字檔並顯示內容。
2. **檔案寫入**：將字串寫入新檔案。
3. **JSON 練習**：將字典轉換為 JSON 並儲存。
4. **讀取行數**：計算文字檔的行數。
5. **附加寫入**：在不覆蓋檔案的情況下新增內容。
6. **檔案是否存在**：檢查檔案是否存在。
7. **建立資料夾**：使用 os 模組建立新資料夾。
8. **列出檔案**：列出目前目錄的所有檔案。
9. **複製檔案**：複製圖片或文字檔。
10. **刪除檔案**：刪除指定的檔案。

### 進階題

1. **通訊錄**：使用 JSON 實作通訊錄的儲存和讀取。
2. **CSV 處理**：讀取 CSV 檔案並計算總平均。
3. **檔案複製**：複製一個檔案到另一個位置。
4. **日誌系統**：實作一個簡單的日誌系統，記錄程式執行過程。
5. **批次處理**：將多個 CSV 檔案合併成一個。
6. **設定檔管理**：使用 JSON 讀寫程式設定。
7. **學生資料庫**：使用 JSON 儲存和讀取多位學生資料。
8. **資料備份**：自動備份指定資料夾的檔案。

### 挑戰題

1. **INI 檔案解析**：解析 Windows INI 格式的設定檔。
2. **XML 轉 JSON**：將 XML 格式轉換為 JSON。
3. **簡易檔案總管**：實作可以瀏覽、複製、刪除檔案的程式。

---

## 進一步閱讀

### 路徑處理 (pathlib)

```python
from pathlib import Path

p = Path("/home/user/documents")

# 路徑操作
p.exists()          # 檢查是否存在
p.is_file()        # 是否為檔案
p.is_dir()         # 是否為目錄
p.parent           # 父目錄
p.name             # 檔名
p.stem             # 不含副檔名
p.suffix           # 副檔名
p.iterdir()        # 迭代目錄內容

# 建立路徑
Path("dir") / "file.txt"  # 路徑連接
```

### os 模組

```python
import os

# 檔案操作
os.rename("old.txt", "new.txt")  # 重新命名
os.remove("file.txt")            # 刪除檔案
os.copy("src.txt", "dst.txt")    # 複製檔案

# 目錄操作
os.mkdir("new_dir")              # 建立目錄
os.makedirs("a/b/c")             # 建立多層目錄
os.rmdir("empty_dir")            # 刪除空目錄
os.removedirs("a/b/c")           # 刪除多層空目錄

# 資訊取得
os.listdir(".")                  # 列出目錄內容
os.getcwd()                     # 取得目前目錄
os.path.getsize("file.txt")     # 取得檔案大小
```

### JSON 格式處理

```python
import json

data = {"name": "Alice", "age": 25, "skills": ["Python", "Java"]}

# 寫入 JSON
with open("data.json", "w", encoding="utf-8") as f:
    json.dump(data, f, ensure_ascii=False, indent=2)

# 讀取 JSON
with open("data.json", "r", encoding="utf-8") as f:
    data = json.load(f)
```

### CSV 檔案處理

```python
import csv

# 寫入 CSV
with open("output.csv", "w", newline="", encoding="utf-8") as f:
    writer = csv.writer(f)
    writer.writerow(["Name", "Age"])
    writer.writerow(["Alice", "25"])

# 讀取 CSV
with open("input.csv", "r", encoding="utf-8") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)
```

### Python 官方文件

- [pathlib](https://docs.python.org/3/library/pathlib.html) - 物件導向路徑處理
- [os](https://docs.python.org/3/library/os.html) - OS 介面
- [json](https://docs.python.org/3/library/json.html) - JSON 編碼解碼
- [csv](https://docs.python.org/3/library/csv.html) - CSV 檔案處理

---

*下一章節，我們將學習第 10 章 Tkinter GUI 程式設計，建立圖形使用者介面。*
