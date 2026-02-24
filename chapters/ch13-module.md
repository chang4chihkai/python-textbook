# 第 13 章｜模組與套件

## 學習目標

- 理解模組的概念
- 掌握 import 的使用方法
- 學會建立自己的模組
- 了解 Python 標準庫的使用
- 掌握 pip 套件管理

---

## 13.1 什麼是模組？

> **📝 Note（說明）**：**模組（Module）** 是一個 Python 檔案（.py），裡面包含變數、函式、類別等，可以被其他程式引用。模組幫助我們組織程式碼，讓程式更容易維護和重用。

**模組（Module）** 是一個 Python 檔案（.py），裡面包含變數、函式、類別等，可以被其他程式引用。

```
my_module.py  →  import my_module
game.py        →  import game
utils.py       →  import utils
```

---

## 13.2 import 使用方法

> **💡 Tip（小技巧）**：建議使用 `import module` 或 `from module import specific_item` 的方式匯入，這樣可以避免命名空間污染，也讓程式碼更易讀。

### 基本 import

```python
# 匯入整個模組
import math

print(math.pi)         # 3.141592653589793
print(math.sqrt(16))   # 4.0
print(math.floor(3.7)) # 3
```

### 匯入特定項目

```python
# 從模組匯入特定函式或類別
from math import sqrt, pi
print(sqrt(16))  # 4.0
print(pi)        # 3.14159...

# 使用 alias（別名）
from math import sqrt as s
print(s(25))     # 5.0

# 匯入所有項目（不推薦）
from math import *
```

---

## 13.3 建立自己的模組

> **📝 Note（說明）**：自訂模組的檔名不能以數字開頭，也不能與 Python 內建模組名稱衝突。建議使用有意義的名稱，如 `my_utils.py`、`data_processor.py` 等。

### 建立 my_utils.py

```python
# my_utils.py

def greet(name):
    return f"你好，{name}！"

def add(a, b):
    return a + b

def is_even(n):
    return n % 2 == 0

PI = 3.14159
```

### 使用自訂模組

```python
import my_utils

print(my_utils.greet("小明"))
print(my_utils.add(3, 5))
print(my_utils.is_even(10))
print(my_utils.PI)
```

### __name__ 屬性

```python
# my_module.py
def test():
    print("這是 test 函式")

if __name__ == "__main__":
    # 當直接執行此檔案時執行
    test()
```

---

## 13.4 Python 標準庫

Python 內建豐富的標準庫：

### 常用模組

```python
import random    # 隨機數
import datetime  # 日期時間
import os        # 作業系統
import sys       # 系統
import json      # JSON 處理
import re        # 正規表達式
```

### random 模組

```python
import random

print(random.random())        # 0.0-1.0 之間的隨機數
print(random.randint(1, 10))  # 1-10 之間的整數
print(random.choice(["a", "b", "c"]))  # 隨機選擇
print(random.shuffle([1, 2, 3, 4, 5])) # 隨機排列
```

### datetime 模組

```python
import datetime

now = datetime.datetime.now()
print(now)                   # 2024-01-15 10:30:45.123456

print(now.year)              # 2024
print(now.month)             # 1
print(now.day)               # 15

# 格式化
print(now.strftime("%Y-%m-%d %H:%M:%S"))  # 2024-01-15 10:30:45
```

### os 模組

```python
import os

print(os.getcwd())          # 取得目前目錄
print(os.listdir("."))      # 列出目錄內容
os.mkdir("new_folder")      # 建立資料夾
os.rename("old", "new")     # 重新命名
os.remove("file.txt")       # 刪除檔案
```

---

## 13.5 套件管理 pip

> **⚠️ Caution（注意）**：安裝套件時要注意版本相容性，有些套件可能與特定版本的 Python 不相容。建議使用虛擬環境來隔離不同專案的依賴。

### 基本指令

```bash
# 安裝套件
pip install requests

# 解除安裝
pip uninstall requests

# 列出已安裝的套件
pip list

# 檢查需要更新的套件
pip list --outdated

# 升級套件
pip install --upgrade package_name
```

### 常用第三方套件

| 套件 | 用途 |
|------|------|
| `requests` | HTTP 請求 |
| `numpy` | 數值計算 |
| `pandas` | 資料分析 |
| `matplotlib` | 資料視覺化 |
| `flask` | 網頁框架 |
| `django` | 網站框架 |

---

## 13.6 虛擬環境

> **💡 Tip（小技巧）**：虛擬環境可以讓每個專案有獨立的依賴套件，避免不同專案之間的套件版本衝突。這是 Python 專案管理的最佳實踐。

### 為什麼需要虛擬環境？

不同專案可能需要不同版本的套件，虛擬環境可以隔離各專案的環境。

### 建立虛擬環境

```bash
# 建立
python -m venv myenv

# 啟動（Windows）
myenv\Scripts\activate

# 啟動（Mac/Linux）
source myenv/bin/activate

# 停用
deactivate
```

### 使用 requirements.txt

```bash
# 匯出環境
pip freeze > requirements.txt

# 安裝環境
pip install -r requirements.txt
```

---

## 13.7 Turtle 繪圖：使用模組增強功能

學會了模組，我們可以使用更多 Turtle 的功能來畫出更複雜的圖案！

### 使用 turtle 模組的更多功能

```python
import turtle
import math

# 設定畫布大小
turtle.setup(800, 600)

# 設定背景顏色
turtle.bgcolor("black")

# 設定烏龜速度
turtle.speed(0)

# 畫出美麗的圓舞曲
for i in range(100):
    # 根據角度計算位置
    angle = i * 0.1
    x = 200 * math.cos(angle)
    y = 200 * math.sin(angle)
    
    turtle.penup()
    turtle.goto(x, y)
    turtle.pendown()
    
    # 畫小圓
    turtle.color("cyan")
    turtle.circle(10 + i * 0.5)

turtle.done()
```

### 練習：畫出彩色螺旋

```python
import turtle
import colorsys

turtle.speed(0)
turtle.bgcolor("black")

# 使用 HSV 色彩空間
for i in range(360):
    # 轉換 HSV 到 RGB
    color = colorsys.hsv_to_rgb(i / 360, 1.0, 1.0)
    turtle.color(color)
    
    turtle.forward(i * 0.5)
    turtle.right(59)
    turtle.circle(10)

turtle.done()
```

---

## 13.8 實用範例

### 範例1：隨機密碼產生器

```python
import random
import string

def generate_password(length=8):
    """產生隨機密碼"""
    chars = string.ascii_letters + string.digits
    password = "".join(random.choice(chars) for _ in range(length))
    return password

# 產生 5 個密碼
for i in range(5):
    print(f"密碼 {i+1}: {generate_password(12)}")
```

### 範例2：檔案備份程式

```python
import os
import shutil
import datetime

def backup_file(source):
    """備份檔案"""
    # 產生備份檔名
    timestamp = datetime.datetime.now().strftime("%Y%m%d_%H%M%S")
    filename, ext = os.path.splitext(source)
    backup_name = f"{filename}_backup_{timestamp}{ext}"
    
    # 複製檔案
    shutil.copy2(source, backup_name)
    print(f"已備份為：{backup_name}")

# 使用
backup_file("important.txt")
```

### 範例3：簡單計時器

```python
import time

def countdown(seconds):
    """倒數計時"""
    while seconds > 0:
        print(f"\r倒數：{seconds} 秒", end="")
        time.sleep(1)
        seconds -= 1
    print("\r時間到！")

countdown(5)
```

---

## 本章小結

| 語法 | 說明 |
|------|------|
| `import module` | 匯入模組 |
| `from module import func` | 匯入特定項目 |
| `import module as alias` | 使用別名 |
| `pip install package` | 安裝套件 |
| `python -m venv` | 建立虛擬環境 |

---

## 練習題

### 基礎題

1. **math 模組**：使用 math 模組計算圓面積和球體積。
2. **random 模組**：從列表中隨機選擇項目。
3. **datetime 模組**：顯示今天的日期和時間。
4. **os 模組**：取得目前工作目錄。
5. **建立自訂模組**：建立包含加法和減法函式的模組。
6. **import 練習**：使用不同的 import 方式匯入模組。
7. **字串模組**：使用 string 模組產生字母序列。
8. **時間模組**：使用 time 模組測量程式執行時間。
9. **路徑處理**：使用 os.path 處理檔案路徑。
10. **資料夾操作**：建立、刪除資料夾。

### 進階題

1. **密碼產生器**：參考範例 1，產生包含特殊字元的密碼。
2. **建立工具模組**：建立包含多個實用函式的模組。
3. **檔案管理**：使用 os 模組列出目錄中的所有檔案。
4. **天氣查詢**：使用 requests 套件查詢天氣 API。
5. **自動化備份**：建立一個自動備份腳本。
6. **建立套件**：建立一個包含多個模組的套件。
7. **版本號比對**：使用 distutils 比較套件版本。
8. **日誌記錄**：使用 logging 模組設定日誌。

### 挑戰題

1. **HTTP 伺服器**：使用 http.server 建立簡單網頁伺服器。
2. **自動更新**：檢查並自動更新已安裝的套件。
3. **專案打包**：將自己寫的程式打包成可安裝的套件。

---

## 13.9 實用範例 - 小遊戲

### 遊戲 1：幸運抽獎系統

使用多個模組設計的抽獎系統！

```python
# 幸運抽獎系統
# 學習重點：random, datetime, time 等模組

import random
import datetime
import time

print("=" * 50)
print("        🎰 幸運抽獎系統 🎰")
print("=" * 50)
print()

# 獎品列表
prizes = [
    "特獎：Nintendo Switch",
    "頭獎：PS5 主機",
    "二獎：iPhone 15",
    "三獎：AirPods Pro",
    "四獎：500 元禮券",
    "五獎：100 元禮券",
    "六獎：50 元禮券",
    "七獎：10 元硬幣"
]

# 參加者
participants = []

print("請輸入參與者姓名（輸入 '結束' 停止）：")
while True:
    name = input("姓名：")
    if name == "結束":
        break
    participants.append(name)

print(f"\n共有 {len(participants)} 位參與者")

# 顯示獎品
print("\n" + "-" * 40)
print("獎品列表：")
for i, prize in enumerate(prizes, 1):
    print(f"  {i}. {prize}")
print("-" * 40)

# 抽獎
print("\n🎉 開始抽獎！")
time.sleep(1)

# 記錄結果
results = {}

for i, prize in enumerate(prizes):
    if not participants:
        print("沒有更多參與者了！")
        break
    
    print(f"\n抽獎中：{prize}...")
    time.sleep(1.5)  # 增加緊張感
    
    # 抽出幸運者
    winner_idx = random.randint(0, len(participants) - 1)
    winner = participants.pop(winner_idx)
    
    results[prize] = winner
    print(f"🎊 幸運得主：{winner}！")

# 顯示結果
print("\n" + "=" * 50)
print("        抽獎結果公佈！")
print("=" * 50)

for prize, winner in results.items():
    print(f"{prize} → {winner}")

# 記錄時間
now = datetime.datetime.now()
print(f"\n抽獎時間：{now.strftime('%Y-%m-%d %H:%M:%S')}")
print("=" * 50)
```

---

## 13.10 遊戲 2：每日幸運星

使用多個模組的幸運預測遊戲！

```python
# 每日幸運星
# 學習重點：random, datetime, math 等模組

import random
import datetime
import math

print("=" * 50)
print("        ⭐ 每日幸運星 ⭐")
print("=" * 50)
print()

name = input("請輸入你的名字：")
birthday = input("請輸入你的生日 (YYYY-MM-DD)：")

# 幸運數計算
lucky_number = 0
for char in name + birthday:
    lucky_number += ord(char)

lucky_number = (lucky_number % 100) + 1

print()
print("-" * 40)
print(f"{name}，你的幸運數字是：{lucky_number}")
print("-" * 40)

# 幸運類型
luck_types = [
    "今天會遇到好事！",
    "適合學習新東西！",
    "運氣普通，平淡的一天",
    "小心可能有小麻煩",
    "會有意想不到的驚喜！"
]

today = datetime.datetime.now()
day_of_year = today.timetuple().tm_yday

luck_index = (lucky_number + day_of_year) % len(luck_types)

print(f"\n今日運勢：{luck_types[luck_index]}")

# 幸運色
colors = ["紅", "橙", "黃", "綠", "藍", "紫", "粉紅", "白"]
lucky_color = colors[(lucky_number - 1) % len(colors)]
print(f"幸運色：{lucky_color}")

# 幸運數字
lucky_nums = random.sample(range(1, 50), 5)
print(f"幸運號碼：{lucky_nums}")

# 幸運食物
foods = ["披薩", "壽司", "炸雞", "牛肉麵", "咖哩飯", "義大利麵"]
lucky_food = foods[(lucky_number + day_of_year) % len(foods)]
print(f"幸運食物：{lucky_food}")

print()
print(f"日期：{today.strftime('%Y-%m-%d')}")
print("=" * 50)
```

---

## 進一步閱讀

### 更多標準函式庫

| 模組 | 說明 |
|------|------|
| `datetime` | 日期和時間處理 |
| `collections` | 額外的資料結構（如 deque, Counter） |
| `itertools` | 迭代器工具 |
| `functools` | 函式式程式工具 |
| `random` | 隨機數生成 |
| `math` | 數學函式 |
| `re` | 正規表達式 |
| `json` | JSON 編碼解碼 |
| `sqlite3` | SQLite 資料庫 |
| `urllib` | URL 處理和網路請求 |

### collections 模組

```python
from collections import Counter, defaultdict, deque, OrderedDict

# Counter - 計數
Counter("abracadabra")  # Counter({'a': 5, 'b': 2, 'r': 2, 'c': 1, 'd': 1})

# defaultdict - 預設值字典
d = defaultdict(list)
d["fruits"].append("apple")

# deque - 雙端佇列
dq = deque([1, 2, 3])
dq.appendleft(0)
dq.extend([4, 5])
```

### itertools 模組

```python
import itertools

# 無限迭代器
count(10)        # 10, 11, 12, ...
cycle([1, 2])    # 1, 2, 1, 2, ...
repeat(5)        # 5, 5, 5, ...

# 有限迭代器
islice(count(0), 5)      # 0, 1, 2, 3, 4
combinations("ABC", 2)   # AB, AC, BC
permutations("ABC", 2)   # AB, AC, BA, BC, CA, CB
product([1,2], [3,4])    # (1,3), (1,4), (2,3), (2,4)
```

### datetime 模組

```python
from datetime import datetime, timedelta

now = datetime.now()
print(now)                  # 2024-01-15 10:30:00
print(now.year, now.month, now.day)

# 日期計算
tomorrow = now + timedelta(days=1)
last_week = now - timedelta(weeks=1)

# 格式化
now.strftime("%Y/%m/%d %H:%M")  # "2024/01/15 10:30"
datetime.strptime("2024-01-15", "%Y-%m-%d")
```

### 建立自己的模組

```python
# mymodule.py
"""這是我的模組"""

def greet(name):
    return f"Hello, {name}!"

__all__ = ['greet']  # 匯出列表

# 使用
import mymodule
mymodule.greet("Alice")
```

### Python 官方文件

- [標準函式庫](https://docs.python.org/3/library/) - 所有標準模組
- [模組搜尋路徑](https://docs.python.org/3/tutorial/modules.html#the-module-search-path) - import 機制說明
- [pip 文件](https://pip.pypa.io/) - 套件管理工具

---

*下一章節，我們將學習第 14 章演算法基礎，這是程式設計的核心技能。*
