# 第 16 章｜實用工具與技巧

## 學習目標

- 掌握 Git 版本控制基礎
- 學會使用除錯技巧
- 了解程式碼風格與規範
- 能夠撰寫簡易文件

---

## 16.1 Git 版本控制

> **💡 Tip（小技巧）**：養成經常提交（commit）的習慣，每次提交應該只包含一個相關的修改，這樣可以更容易追蹤問題和還原程式碼。

### 什麼是 Git？

**Git** 是一個分散式版本控制系統，用來追蹤程式碼的修改歷史。

```
未使用 Git：只能覆蓋存檔
使用 Git：可以查看修改歷史、還原版本、多人協作
```

### 基本指令

```bash
# 初始化儲存庫
git init

# 檢視狀態
git status

# 新增檔案到暫存區
git add filename.py
git add .   # 新增所有檔案

# 提交更改
git commit -m "提交訊息"

# 查看歷史
git log

# 查看修改
git diff
```

### 工作流程

```
工作目錄 → 暫存區 → 儲存庫
  git add  →  git commit
```

---

## 16.2 除錯技巧

> **📝 Note（說明）**：除錯（Debugging）是程式設計的重要技能。常見的除錯方法包括：使用 print 輸出、使用 assert 斷言、使用 IDE 的除錯工具等。

### 使用 print 除錯

```python
def divide(a, b):
    print(f"除法：{a} / {b}")  # 除錯輸出
    result = a / b
    print(f"結果：{result}")  # 除錯輸出
    return result
```

### 使用 assert 斷言

```python
def withdraw(balance, amount):
    assert amount > 0, "提款金額必須為正數"
    assert amount <= balance, "餘額不足"
    return balance - amount
```

### 使用 try-except 除錯

```python
try:
    result = risky_operation()
except Exception as e:
    print(f"發生錯誤：{e}")
    import traceback
    traceback.print_exc()
```

### IDE 除錯工具

大多數 IDE（如 VS Code、PyCharm）都有：
- 設定中斷點（Breakpoint）
- 逐步執行（Step by Step）
- 檢視變數（Watch Variables）

---

## 16.3 程式碼風格

> **⚠️ Caution（注意）**：一致的程式碼風格可以讓程式碼更容易閱讀和維護。建議使用 PEP 8 規範，並使用自動化工具（如 flake8、black）來檢查和格式化程式碼。

### Python 風格指南（PEP 8）

```python
# ✅ 好：清晰的命名
def calculate_total_price(items, tax_rate):
    subtotal = sum(item.price for item in items)
    return subtotal * (1 + tax_rate)

# ❌ 差：模糊的命名
def calc(p, t):
    s = sum(x.price for x in p)
    return s * (1 + t)
```

### 縮排

```python
# 使用 4 個空格（不要用 Tab）
if x > 0:
    print("Positive")
```

### 行長限制

```python
# 建議每行不超過 80-100 字元
# 可以用反斜線或括號換行
result = some_function(arg1, arg2, arg3,
                       arg4, arg5)

# 或使用括號隱性換行
result = (some_function(arg1, arg2, arg3)
          + another_function(arg4, arg5))
```

### 註解

```python
# 單行註解

def calculate_bmi(weight, height):
    """計算 BMI 值。
    
    Args:
        weight: 體重（公斤）
        height: 身高（公尺）
    
    Returns:
        BMI 值
    """
    return weight / (height ** 2)
```

---

## 16.4 文件字串（Docstring）

> **💡 Tip（小技巧）**：為函式和類別撰寫清晰的 docstring 可以幫助他人（甚至是自己）理解程式碼的用途和用法。建議使用 Google 風格或 NumPy 風格的 docstring。

### Google 風格

```python
def function(param1, param2):
    """函式說明。
    
    Args:
        param1: 參數1說明
        param2: 參數2說明
    
    Returns:
        回傳值說明
    
    Raises:
        ValueError: 當參數無效時
    """
    pass
```

### NumPy 風格

```python
def function(param1, param2):
    """
    函式說明。
    
    Parameters
    ----------
    param1 : type
        參數1說明
    param2 : type
        參數2說明
    
    Returns
    -------
    type
        回傳值說明
    """
    pass
```

---

## 16.5 虛擬環境

### 使用 venv

```bash
# 建立虛擬環境
python -m venv myenv

# 啟動（Windows）
myenv\Scripts\activate

# 啟動（Mac/Linux）
source myenv/bin/activate

# 停用
deactivate

# 刪除
rm -rf myenv
```

---

## 16.6 常用開發工具

### 格式化工具

```bash
# Black - 自動格式化
pip install black
black filename.py

# isort - 排序 import
pip install isort
isort filename.py
```

### 程式碼檢查

```bash
# Flake8 - 程式碼風格檢查
pip install flake8
flake8 filename.py

# Pylint - 更嚴格的檢查
pip install pylint
pylint filename.py
```

### 類型檢查

```bash
# mypy - 靜態類型檢查
pip install mypy
mypy filename.py
```

---

## 16.7 Turtle 繪圖：除錯與測試

學會了除錯技巧，我們可以讓 Turtle 程式更加穩定！

### 用 assert 檢查參數

```python
import turtle

def draw_polygon(sides, length):
    """畫多邊形，加入參數檢查"""
    assert sides >= 3, "邊數必須 >= 3"
    assert length > 0, "長度必須 > 0"
    
    angle = 360 / sides
    for i in range(sides):
        turtle.forward(length)
        turtle.right(angle)

# 測試各種參數
try:
    draw_polygon(5, 80)   # 正常
    draw_polygon(3, 60)   # 正常
    draw_polygon(0, 50)   # 會失敗！
except AssertionError as e:
    print(f"參數錯誤：{e}")

turtle.done()
```

### 用 print 除錯畫圖過程

```python
import turtle

def draw_with_debug(sides, length):
    """畫圖並顯示除錯資訊"""
    print(f"開始畫 {sides} 邊形，邊長 {length}")
    
    angle = 360 / sides
    print(f"每個角度：{angle}")
    
    for i in range(sides):
        print(f"畫第 {i+1} 邊...")
        turtle.forward(length)
        turtle.right(angle)
    
    print("畫圖完成！")

draw_with_debug(4, 100)
turtle.done()
```

### 練習：安全的畫圖函式

```python
import turtle

def safe_draw(shape_type, size):
    """安全的畫圖函式"""
    # 參數驗證
    valid_shapes = ["circle", "square", "triangle"]
    
    if shape_type not in valid_shapes:
        raise ValueError(f"不支援的形狀：{shape_type}")
    
    if size <= 0 or size > 500:
        raise ValueError("大小必須在 1-500 之間")
    
    # 畫圖
    if shape_type == "circle":
        turtle.circle(size)
    elif shape_type == "square":
        for i in range(4):
            turtle.forward(size)
            turtle.right(90)
    elif shape_type == "triangle":
        for i in range(3):
            turtle.forward(size)
            turtle.right(120)

# 測試
try:
    safe_draw("circle", 50)
    safe_draw("square", 80)
    safe_draw("star", 50)  # 會失敗
except ValueError as e:
    print(f"錯誤：{e}")

turtle.done()
```

---

## 16.8 實用技巧

### 計時效能

```python
import time

start = time.time()
# 執行的程式碼
result = sum(range(1000000))
end = time.time()
print(f"花費時間：{end - start:.4f} 秒")
```

### 記憶體使用

```python
import sys

# 查看變數大小
x = 100
print(sys.getsizeof(x))

# 查看物件大小
data = [1, 2, 3, 4, 5]
print(sys.getsizeof(data))
```

### 複製物件

```python
import copy

# 淺拷貝
list1 = [[1, 2], [3, 4]]
list2 = list1.copy()

# 深拷貝
list3 = copy.deepcopy(list1)
```

---

## 本章小結

| 工具 | 用途 |
|------|------|
| Git | 版本控制 |
| print/assert | 除錯 |
| Black/isort | 程式碼格式化 |
| Flake8/Pylint | 程式碼檢查 |
| mypy | 型別檢查 |
| venv | 虛擬環境 |

---

## 16.7 實用範例 - 小遊戲

### 遊戲 1：效能測試遊戲

比較不同排序演算法的效能！

```python
# 效能測試遊戲
# 學習重點：time 模組、效能測量

import time
import random

def bubble_sort(arr):
    """氣泡排序"""
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]

def selection_sort(arr):
    """選擇排序"""
    n = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]

def python_sort(arr):
    """Python 內建排序"""
    return sorted(arr)

print("=" * 50)
print("        ⏱️ 排序效能大賽 ⏱️")
print("=" * 50)
print()

# 選擇測試規模
print("選擇測試規模：")
print("1. 小 (1000 個數字)")
print("2. 中 (5000 個數字)")
print("3. 大 (10000 個數字)")

choice = input("選擇：")
if choice == "1":
    size = 1000
elif choice == "2":
    size = 5000
else:
    size = 10000

print(f"\n產生 {size} 個隨機數字...")

# 準備測試資料
data = [random.randint(1, 100000) for _ in range(size)]

print("=" * 50)

# 測試氣泡排序
test_data = data.copy()
start = time.time()
bubble_sort(test_data)
bubble_time = time.time() - start
print(f"氣泡排序：{bubble_time:.4f} 秒")

# 測試選擇排序
test_data = data.copy()
start = time.time()
selection_sort(test_data)
selection_time = time.time() - start
print(f"選擇排序：{selection_time:.4f} 秒")

# 測試 Python 內建排序
test_data = data.copy()
start = time.time()
python_sort(test_data)
python_time = time.time() - start
print(f"Python 內建排序：{python_time:.4f} 秒")

print("=" * 50)
print("\n結論：")
print(f"Python 內建排序是最快的！")
print(f"比氣泡排序快 {bubble_time/python_time:.1f} 倍")
```

---

### 遊戲 2：除錯挑戰賽

練習使用 assert 和 print 除錯！

```python
# 除錯挑戰賽
# 學習重點：assert 斷言、print 除錯

def calculate_score(correct, wrong, empty):
    """計算考試分數"""
    # 遊戲規則：答對 +10 分，答錯 -3 分，空白 0 分
    
    assert correct >= 0, "答對題數不能為負數"
    assert wrong >= 0, "答錯題數不能為負數"
    assert empty >= 0, "空白題數不能為負數"
    assert correct + wrong + empty > 0, "總題數必須大於 0"
    
    score = correct * 10 - wrong * 3
    
    # 分數不能為負
    if score < 0:
        score = 0
    
    # 答對率
    total = correct + wrong + empty
    correct_rate = (correct / total) * 100
    
    return {
        "score": score,
        "correct": correct,
        "wrong": wrong,
        "empty": empty,
        "correct_rate": correct_rate
    }

print("=" * 50)
print("        📝 除錯挑戰賽 📝")
print("=" * 50)
print()

print("考試分數計算機")
print("規則：答對 +10 分，答錯 -3 分，空白 0 分")
print()

# 測試案例
test_cases = [
    (10, 5, 5),    # 正常
    (15, 0, 5),     # 全對
    (0, 10, 10),    # 全錯
    (-1, 5, 5),     # 錯誤：負數
    (5, -2, 5),     # 錯誤：負數
]

for i, (correct, wrong, empty) in enumerate(test_cases):
    print(f"\n測試案例 {i+1}：答對 {correct}，答錯 {wrong}，空白 {empty}")
    try:
        result = calculate_score(correct, wrong, empty)
        print(f"✓ 分數：{result['score']} 分")
        print(f"  答對率：{result['correct_rate']:.1f}%")
    except AssertionError as e:
        print(f"✗ 錯誤：{e}")
    except Exception as e:
        print(f"✗ 未預期錯誤：{e}")

print()
print("=" * 50)
print("除錯挑戰完成！")
```

---

## 練習題

### 基礎題

1. **Git 練習**：初始化一個 Git 儲存庫並進行提交。
2. **除錯練習**：使用 print 找出程式錯誤。
3. **程式碼風格**：使用 Black 格式化程式碼。
4. **commit 練習**：建立一個包含多次提交的 Git 歷史。
5. **分支練習**：建立、切換、合併 Git 分支。
6. **除錯練習**：使用 assert 進行斷言檢查。
7. **Docstring 練習**：為函式加上說明文件。
8. **虛擬環境**：建立並啟動虛擬環境。
9. **requirements.txt**：建立專案的依賴檔案。
10. **IDE 除錯**：學習使用 VS Code 設定中斷點除錯。

### 進階題

1. **文件撰寫**：為自己寫的函式加上 docstring。
2. **虛擬環境**：建立並使用虛擬環境。
3. **效能分析**：測量不同排序演算法的執行時間。
4. **CI/CD 入門**：了解 GitHub Actions 的基本概念。
5. **測試入門**：使用 unittest 撰寫單元測試。
6. **程式碼檢查**：使用 Flake8 檢查程式碼問題。
7. **重構練習**：將混亂的程式碼重構成整潔的版本。
8. **版本標籤**：使用 Git 標籤管理版本。

### 挑戰題

1. **自動化部署**：使用 GitHub Actions 部署專案。
2. **單元測試框架**：為通訊錄系統撰寫完整的單元測試。
3. **程式碼品質分析**：使用工具分析程式碼覆蓋率。

---

## 進一步閱讀

### 更多常用第三方套件

| 套件 | 說明 | 用途 |
|------|------|------|
| `requests` | HTTP 客戶端 | 網路請求 |
| `numpy` | 數值計算 | 科學計算 |
| `pandas` | 資料分析 | 資料處理 |
| `matplotlib` | 繪圖 | 資料視覺化 |
| `pillow` | 影像處理 | 圖片操作 |
| `flask` | Web 框架 | 網站開發 |
| `django` | Web 框架 | 企業級網站 |
| `pytest` | 測試框架 | 單元測試 |
| `black` | 格式化 | 程式碼格式化 |
| `pylint` | Linter | 程式碼檢查 |

### requests 套件

```python
import requests

# GET 請求
response = requests.get("https://api.github.com")
print(response.status_code)
print(response.json())

# POST 請求
data = {"username": "test", "password": "123"}
response = requests.post("https://api.example.com/login", json=data)
```

### 環境變數管理

```python
import os
from dotenv import load_dotenv

# .env 檔案
# API_KEY=your_api_key_here
# DATABASE_URL=postgres://...

load_dotenv()  # 載入 .env 檔案

api_key = os.getenv("API_KEY")
db_url = os.getenv("DATABASE_URL")
```

### 測試框架 (pytest)

```python
# test_example.py
import pytest

def test_addition():
    assert 1 + 1 == 2

def test_list():
    assert len([1, 2, 3]) == 3

@pytest.fixture
def sample_data():
    return {"name": "test", "value": 100}

def test_with_fixture(sample_data):
    assert sample_data["value"] > 0
```

### 程式碼品質工具

```python
# black - 格式化
black myproject.py

# flake8 - 檢查
flake8 myproject.py

# mypy - 型別檢查
mypy myproject.py

# pytest - 測試
pytest tests/
pytest --cov=myproject  # 覆蓋率
```

### Python 官方文件

- [PyPI](https://pypi.org/) - Python 套件索引
- [requests 文件](https://docs.python-requests.org/) - HTTP 套件
- [pytest 文件](https://docs.pytest.org/) - 測試框架

---

*下一章節，我們將學習第 17 章專題實作，整合所學知識。*
