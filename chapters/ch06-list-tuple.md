# 第 6 章｜串列與元組

## 學習目標

- 理解串列（List）的概念與使用
- 掌握串列的基本操作：新增、刪除、修改、存取
- 學會切片（Slicing）操作
- 理解元組（Tuple）與串列的差異
- 能夠運用串列處理批量資料

---

## 6.1 什麼是串列？

> **⚠️ Caution（注意）**：串列中的元素是有序的，你可以透過索引（index）來存取。索引從 0 開始，而非從 1 開始。嘗試存取超出範圍的索引會導致 `IndexError` 錯誤。

**串列（List）** 是 Python 中最常用的資料結構，用來儲存多個有序的元素。

```
串列：[元素1, 元素2, 元素3, ...]
      ↓   ↓    ↓    ↓
     索引 0   1    2    3
```

### 建立串列

```python
# 建立串列
fruits = ["apple", "banana", "cherry"]
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", True, 3.14]

print(fruits)    # ['apple', 'banana', 'cherry']
print(numbers)   # [1, 2, 3, 4, 5]
print(mixed)    # [1, 'hello', True, 3.14]
```

### 空串列

```python
empty_list = []
empty_list2 = list()
```

---

## 6.2 存取串列元素

### 使用索引

```python
fruits = ["apple", "banana", "cherry", "date"]

print(fruits[0])   # apple（第一個元素）
print(fruits[1])   # banana
print(fruits[3])   # date（第四個元素）
print(fruits[-1])  # date（倒數第一個）
print(fruits[-2])  # cherry（倒數第二個）
```

### 索引範圍

```python
numbers = [0, 1, 2, 3, 4, 5]

print(numbers[0:3])   # [0, 1, 2]（索引 0 到 2）
print(numbers[:3])    # [0, 1, 2]（從開頭）
print(numbers[3:])    # [3, 4, 5]（從索引 3 到結束）
print(numbers[:])     # [0, 1, 2, 3, 4, 5]（拷貝整個串列）
print(numbers[::2])  # [0, 2, 4]（間隔 2）
print(numbers[::-1])  # [5, 4, 3, 2, 1, 0]（反轉）
```

---

## 6.3 修改串列

### 新增元素

```python
fruits = ["apple", "banana"]

fruits.append("cherry")      # 新增到末尾
print(fruits)                # ['apple', 'banana', 'cherry']

fruits.insert(1, "orange")  # 插入到指定位置
print(fruits)                # ['apple', 'orange', 'banana', 'cherry']

fruits.extend(["grape", "melon"])  # 新增多個元素
print(fruits)                # ['apple', 'orange', 'banana', 'cherry', 'grape', 'melon']
```

### 刪除元素

```python
fruits = ["apple", "banana", "cherry", "banana"]

fruits.remove("banana")      # 移除第一個找到的元素
print(fruits)                # ['apple', 'cherry', 'banana']

fruits.pop()                 # 移除最後一個元素
print(fruits)                # ['apple', 'cherry']

fruits.pop(0)                # 移除指定索引的元素
print(fruits)                # ['cherry']

del fruits[0]                # 也可以用 del 刪除
print(fruits)                # []

fruits.clear()               # 清空串列
print(fruits)                # []
```

### 修改元素

```python
fruits = ["apple", "banana", "cherry"]
fruits[1] = "orange"         # 修改指定索引的元素
print(fruits)                # ['apple', 'orange', 'cherry']
```

---

## 6.4 串列操作

### 常用函式

```python
numbers = [3, 1, 4, 1, 5, 9, 2, 6]

print(len(numbers))          # 8（串列長度）
print(max(numbers))           # 9（最大值）
print(min(numbers))           # 1（最小值）
print(sum(numbers))           # 31（總和）
print(sorted(numbers))        # [1, 1, 2, 3, 4, 5, 6, 9]（排序）
print(numbers.count(1))      # 2（計算元素出現次數）
print(numbers.index(4))      # 2（找到元素索引）
```

### 檢查元素是否存在

```python
fruits = ["apple", "banana", "cherry"]

print("banana" in fruits)    # True
print("orange" in fruits)    # False
```

---

## 6.5 串列與迴圈

### 遍歷串列

```python
fruits = ["apple", "banana", "cherry"]

# 方法1：直接遍歷
for fruit in fruits:
    print(fruit)

# 方法2：使用索引
for i in range(len(fruits)):
    print(i, fruits[i])
```

### 列表推導式

```python
# 基本語法：[運算式 for 項目 in 串列]

# 計算每個數的平方
squares = [x**2 for x in range(1, 6)]
print(squares)   # [1, 4, 9, 16, 25]

# 篩選條件
evens = [x for x in range(10) if x % 2 == 0]
print(evens)     # [0, 2, 4, 6, 8]
```

---

## 6.6 元組（Tuple）

### 什麼是元組？

**元組（Tuple）** 與串列類似，但建立後不能修改（不可變）。

```python
# 建立元組
point = (10, 20)
print(point)        # (10, 20)

# 單元素元組需要逗號
single = (5,)
print(single)      # (5,)

# 也可以不加括號
coordinates = 10, 20, 30
print(coordinates)  # (10, 20, 30)
```

### 存取元組

```python
point = (10, 20, 30)

print(point[0])    # 10
print(point[-1])   # 30
print(point[0:2]) # (10, 20)
```

### 元組與串列的比較

| 特性 | 串列 | 元組 |
|------|------|------|
| 語法 | [1, 2, 3] | (1, 2, 3) |
| 可修改 | 是 | 否 |
| 效能 | 較慢 | 較快 |
| 用途 | 需要修改的資料 | 固定資料 |

### 元組常用場合

```python
# 函式回傳多個值
def get_stats(numbers):
    return min(numbers), max(numbers), sum(numbers)

min_val, max_val, total = get_stats([1, 2, 3, 4, 5])
print(min_val, max_val, total)   # 1 5 15

# 交換變數（巧妙用法）
a, b = 1, 2
a, b = b, a    # 不用暫時變數就能交換
print(a, b)    # 2 1
```

---

## 6.7 Turtle 繪圖：用串列儲存圖形資料

學會了串列，我們可以用串列來儲存座標、顏色等資料，讓畫圖變得更靈活！

### 用串列儲存座標畫圖

```python
import turtle

# 用串列儲存座標點
points = [
    (0, 0),
    (100, 0),
    (100, 100),
    (0, 100)
]

# 依序移動到每個點
turtle.penup()
turtle.goto(points[0])
turtle.pendown()

for point in points:
    turtle.goto(point)# 連回起點
turtle.goto(points[0])

turtle.done()
```

### 用串列畫出多重圖案

```python
import turtle

# 用串列定義多個位置
positions = [
    (-150, 100),
    (0, 100),
    (150, 100),
    (-150, -50),
    (0, -50),
    (150, -50)
]

# 在每個位置畫圓
for pos in positions:
    turtle.penup()
    turtle.goto(pos)
    turtle.pendown()
    turtle.circle(30)

turtle.done()
```

### 用串列儲存顏色

```python
import turtle

# 用串列儲存顏色
colors = ["red", "orange", "yellow", "green", "blue", "purple"]

# 用不同顏色畫出六個正方形
for i, color in enumerate(colors):
    turtle.color(color)
    for j in range(4):
        turtle.forward(80)
        turtle.right(90)
    # 移到下一個位置
    turtle.penup()
    turtle.goto(-150 + i * 60, -150)
    turtle.pendown()

turtle.done()
```

### 用元組定義圖形

```python
import turtle

# 用元組定義正方形的頂點
square = ((0, 0), (100, 0), (100, 100), (0, 100))

# 畫出來
turtle.penup()
turtle.goto(square[0])
turtle.pendown()

for point in square[1:]:
    turtle.goto(point)

turtle.goto(square[0])

turtle.done()
```

### 練習：畫出彩色的圓

```python
import turtle

# 定義顏色串列
colors = ["red", "orange", "yellow", "green", "blue", "indigo", "violet"]

# 用迴圈畫彩虹圈
for i, color in enumerate(colors):
    turtle.color(color)
    turtle.circle(50 + i * 20)  # 半徑越來越大

turtle.done()
```

---

## 6.8 實用範例

### 範例1：成績管理系統

```python
# 建立學生成績串列
scores = []

# 新增成績
scores.append(85)
scores.append(90)
scores.append(78)
scores.append(92)
scores.append(88)

# 計算平均
average = sum(scores) / len(scores)
print(f"平均成績：{average:.1f}")

# 找出最高和最低分
print(f"最高分：{max(scores)}")
print(f"最低分：{min(scores)}")

# 排序
sorted_scores = sorted(scores, reverse=True)
print(f"排名：{sorted_scores}")
```

### 範例2：購物清單

```python
shopping = []

# 新增項目
shopping.append("牛奶")
shopping.append("麵包")
shopping.append("雞蛋")

# 顯示清單
print("購物清單：")
for i, item in enumerate(shopping, 1):
    print(f"{i}. {item}")

# 移除已購買的項目
shopping.remove("麵包")
print("\n購買後：", shopping)
```

---

## 6.7 實用範例 - 小遊戲

### 遊戲 1：幸運抽獎系統

使用串列設計的抽獎系統！

```python
# 幸運抽獎系統
# 學習重點：串列操作、隨機選擇、切片

import random

print("=" * 50)
print("        🎰 幸運抽獎系統 🎰")
print("=" * 50)
print()

# 獎品列表
prizes = [
    "特別獎：Nintendo Switch OLED",
    "頭獎：PS5 主機",
    "二獎：iPhone 15",
    "三獎：AirPods Pro",
    "四獎：500 元禮券",
    "五獎：100 元禮券",
    "六獎：50 元禮券",
    "七獎：精美小禮物",
    "八獎：下次再接再厲",
    "九獎：安慰獎：10 元硬幣"
]

# 參與者列表
participants = []

# 輸入參與者
print("請輸入參與者姓名（輸入 '完成' 結束）：")
while True:
    name = input("姓名：")
    if name == "完成":
        break
    participants.append(name)
    print(f"已加入：{name}")

print()
print(f"共有 {len(participants)} 位參與者")

# 顯示獎品
print()
print("-" * 50)
print("獎品列表：")
for i, prize in enumerate(prizes, 1):
    print(f"  {i}. {prize}")
print("-" * 50)
print()

# 開始抽獎
print("🎉 開始抽獎！")
print()

# 抽特別獎
print("特別獎抽獎中...")
random.shuffle(prizes)
special_winner = random.choice(participants)
print(f"🎊 特別獎得主：{special_winner}！")
print(f"獲得：{prizes[0]}")
print()

# 移除已獲獎者
participants.remove(special_winner)

# 抽出其他獎項
print("-" * 50)
print("其他獎項開獎：")
print("-" * 50)

for i in range(1, len(prizes)):
    if len(participants) == 0:
        print("沒有更多參與者了！")
        break
    
    winner = random.choice(participants)
    participants.remove(winner)
    print(f"  {prizes[i]} → {winner}")

print()
print("=" * 50)
print("抽獎結束！")
print("=" * 50)
```

---

### 遊戲 2：記憶力大考驗

經典的記憶力遊戲，記住數字序列！

```python
# 記憶力大考驗
# 學習重點：串列操作、隨機選擇、enumerate

import random
import time

print("=" * 50)
print("        🧠 記憶力大考驗 🧠")
print("=" * 50)
print()
print("遊戲規則：")
print("  1. 電腦會顯示一串數字")
print("  2. 你有 3 秒鐘記憶")
print("  3. 然後輸入你記住的數字")
print("  4. 正確就能進入下一關")
print()

# 選擇難度
print("選擇難度：")
print("  1. 簡單 (3-5 位數字)")
print("  2. 普通 (4-7 位數字)")
print("  3. 困難 (6-10 位數字)")

difficulty = input("請選擇 (1/2/3)：")

if difficulty == "1":
    min_len, max_len = 3, 5
elif difficulty == "2":
    min_len, max_len = 4, 7
else:
    min_len, max_len = 6, 10

# 遊戲主迴圈
level = 1
score = 0

while True:
    print()
    print("-" * 50)
    print(f"第 {level} 關")
    print("-" * 50)
    
    # 產生隨機數字序列
    sequence_length = min_len + level - 1
    if sequence_length > max_len:
        sequence_length = max_len
    
    sequence = [random.randint(0, 9) for _ in range(sequence_length)]
    
    # 顯示數字序列
    print("請記住以下數字：")
    for num in sequence:
        print(num, end=" ")
    print()
    
    # 倒數計時
    print("3 秒後消失...")
    time.sleep(3)
    
    # 清除畫面（印出多行換行）
    print("\n" * 50)
    
    # 玩家輸入
    print("請輸入你記住的數字（相連輸入，如 1234）：")
    player_input = input()
    
    # 檢查答案
    player_sequence = list(player_input)
    
    # 轉換為數字串列
    try:
        player_sequence = [int(x) for x in player_input]
    except ValueError:
        print("輸入無效！")
        continue
    
    if player_sequence == sequence:
        print()
        print("🎉 正確！進入下一關！")
        score = score + level * 10
        level = level + 1
    else:
        print()
        print("❌ 錯誤！")
        print(f"正確答案是：{''.join(map(str, sequence))}")
        print(f"你輸入的是：{player_input}")
        print()
        print("=" * 50)
        print("        遊戲結束！")
        print("=" * 50)
        print(f"\n你的得分：{score}")
        print(f"通過關卡數：{level - 1}")
        break
    
    time.sleep(1)

print()
print("感謝遊玩！")
```

---

## 6.8 本章小結

| 操作 | 語法 |
|------|------|
| 建立串列 | `list = [1, 2, 3]` |
| 存取元素 | `list[0]`, `list[-1]` |
| 新增元素 | `list.append()`, `list.insert()` |
| 刪除元素 | `list.remove()`, `list.pop()` |
| 切片 | `list[0:3]`, `list[::2]` |
| 建立元組 | `tuple = (1, 2, 3)` |
| 列長推導式 | `[x*2 for x in list]` |

---

## 練習題

### 基礎題

1. **成績串列**：建立包含 5 個成績的串列，計算平均分數。
2. **清單操作**：練習 append、insert、remove、pop 操作。
3. **元組應用**：使用元組回傳座標 x, y 的和與差。
4. **串列切片**：有串列 [0,1,2,3,4,5,6,7,8,9]，取出前5個元素。
5. **元素搜尋**：在串列 [3, 1, 4, 1, 5, 9, 2, 6] 中找出最大值和最小值。
6. **串列反轉**：將串列 [1, 2, 3, 4, 5] 反轉。
7. **計算總和**：使用 sum() 函式計算串列 [10, 20, 30, 40, 50] 的總和。
8. **元素個數**：計算串列 [1, 2, 3, 2, 4, 2, 5] 中數字 2 出現的次數。
9. **清單拷貝**：複製一個串列到另一個串列。
10. **字元轉數字**：將字串 "12345" 轉換為數字串列 [1, 2, 3, 4, 5]。

### 進階題

1. **移除重複**：將串列 [1, 2, 2, 3, 3, 3, 4] 移除重複元素。
2. **名次排列**：輸入 5 個學生姓名與成績，按成績排序輸出名次。
3. **二維串列**：建立 3x3 矩陣並計算總和。
4. **撲克牌遊戲**：建立一副撲克牌（52張），洗牌後發給 4 位玩家。
5. **矩陣乘法**：實作兩個 2x2 矩陣的乘法運算。
6. **列表推導式**：使用列表推導式產生 1 到 100 的平方數。
7. **篩選偶數**：使用列表推導式從串列中篩選偶數。
8. **找中位數**：計算串列 [5, 2, 8, 1, 9] 的中位數。

### 挑戰題

1. **矩陣轉置**：將 3x3 矩陣轉置。
2. **數獨驗證**：檢查 9x9 數獨矩陣是否有效。
3. **楊輝三角**：生成楊輝三角的前 n 行。

---

## 進一步閱讀

### 串列常用方法

```python
fruits = ['apple', 'banana', 'cherry']

fruits.append('orange')      # 末端加入
fruits.insert(1, 'mango')    # 指定位置插入
fruits.remove('banana')      # 移除指定元素
fruits.pop()                 # 移除末端元素
fruits.pop(0)                # 移除指定位置
fruits.clear()              # 清空串列

fruits.sort()                # 原地排序
fruits.reverse()            # 原地反轉
fruits.copy()               # 淺拷貝
fruits.count('apple')       # 計算元素個數
fruits.index('cherry')      # 取得索引位置
```

### 元組常用方法

```python
point = (1, 2, 3)

point.count(2)   # 計算元素個數 → 1
point.index(3)   # 取得索引位置 → 2

# 元組拆包
x, y, z = (1, 2, 3)
a, *b = (1, 2, 3, 4, 5)  # a=1, b=[2, 3, 4, 5]
```

### 切片進階用法

```python
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

numbers[::2]        # [0, 2, 4, 6, 8]  - 偶數索引
numbers[1::2]       # [1, 3, 5, 7, 9]  - 奇數索引
numbers[::-1]       # [9, 8, 7, 6, 5, 4, 3, 2, 1, 0] - 反向
numbers[2:8:2]      # [2, 4, 6] - 切片跳躍
```

### 序列通用函式

```python
numbers = [3, 1, 4, 1, 5, 9, 2, 6]

len(numbers)           # 長度 → 8
max(numbers)           # 最大值 → 9
min(numbers)           # 最小值 → 1
sum(numbers)           # 總和 → 31

sorted(numbers)        # 回傳新排序串列
reversed(numbers)      # 回傳反向迭代器
enumerate(numbers)     # 回傳索引和值的迭代器
```

### Python 官方文件

- [序列類型](https://docs.python.org/3/library/stdtypes.html#sequence-types-list-tuple-range) - 序列完整說明
- [lists](https://docs.python.org/3/library/stdtypes.html#list) - 串列方法
- [tuples](https://docs.python.org/3/library/stdtypes.html#tuple) - 元組說明

---

*下一章節，我們將學習字典與集合，這是 Python 中另外兩個重要的資料結構。*
