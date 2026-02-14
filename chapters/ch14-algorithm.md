# 第 14 章｜演算法基礎

## 學習目標

- 理解演算法的概念
- 掌握時間複雜度與空間複雜度
- 學會基礎排序演算法
- 學會基礎搜尋演算法

---

## 14.1 什麼是演算法？

> **📝 Note（說明）**：**演算法（Algorithm）** 是解決問題的具體步驟，就像食譜告訴你如何一步步做出美味的菜餚，演算法告訴電腦如何一步步解決問題。

**演算法（Algorithm）** 是解決問題的具體步驟，就像食譜：
```
食譜：如何做一道菜
演算法：如何解決一個問題
```

### 好演算法的特點

| 特點 | 說明 |
|------|------|
| 正確性 | 能正確解決問題 |
| 效率 | 執行時間合理 |
| 可讀性 | 程式碼容易理解 |
| 資源節省 | 佔用記憶體少 |

---

## 14.2 時間複雜度

> **💡 Tip（小技巧）**：在設計演算法時，應該盡量選擇時間複雜度較低的方案。O(n log n) 通常是實際應用中的理想選擇，而 O(n²) 適用於小規模資料。

### 什麼是 Big O？

**時間複雜度** 用 Big O 表示法描述：

| 複雜度 | 名稱 | 範例 |
|--------|------|------|
| O(1) | 常數 | 陣列存取 |
| O(log n) | 對數 | 二分搜尋 |
| O(n) | 線性 | 迴圈遍歷 |
| O(n log n) | 線性對數 | 快速排序 |
| O(n²) | 平方 | 巢狀迴圈 |
| O(2ⁿ) | 指數 | 暴力搜尋 |

### 常見複雜度比較

```
       O(2ⁿ)
       O(n²)      **
       O(n log n)   *   *
       O(n)         *   *   *
       O(log n)       *   *   *
       O(1)           *   *   *   *
                 1    10   100  1000
```

---

## 14.3 排序演算法

> **📝 Note（說明）**：氣泡排序是最簡單的排序演算法，但效率較低，時間複雜度為 O(n²)。適合用於教學和小規模資料排序。

### 氣泡排序（Bubble Sort）

```python
def bubble_sort(arr):
    """氣泡排序"""
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                # 交換
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

# 測試
numbers = [64, 34, 25, 12, 22, 11, 90]
print(bubble_sort(numbers))  # [11, 12, 22, 25, 34, 64, 90]
```

- 時間複雜度：O(n²)
- 空間複雜度：O(1)

### 選擇排序（Selection Sort）

```python
def selection_sort(arr):
    """選擇排序"""
    n = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr
```

### 插入排序（Insertion Sort）

```python
def insertion_sort(arr):
    """插入排序"""
    for i in range(1, len(arr)):
        key = arr[i]
        j = i - 1
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
    return arr
```

### 使用 Python 內建排序

```python
# Python 內建的排序（使用 Timsort）
numbers = [64, 34, 25, 12, 22, 11, 90]

sorted_list = sorted(numbers)    # 返回新串列
numbers.sort()                   # 原地排序

print(sorted_list)  # [11, 12, 22, 25, 34, 64, 90]
```

---

## 14.4 搜尋演算法

> **⚠️ Caution（注意）**：二分搜尋要求資料已經排序好，這是使用二分搜尋的重要前提。如果資料未排序，需要先進行排序。

### 線性搜尋（Linear Search）

```python
def linear_search(arr, target):
    """線性搜尋"""
    for i, value in enumerate(arr):
        if value == target:
            return i
    return -1

# 測試
numbers = [10, 20, 30, 40, 50]
print(linear_search(numbers, 30))  # 2
print(linear_search(numbers, 60))  # -1
```

- 時間複雜度：O(n)

### 二分搜尋（Binary Search）

```python
def binary_search(arr, target):
    """二分搜尋（需要已排序陣列）"""
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return -1

# 測試
numbers = [1, 3, 5, 7, 9, 11, 13, 15]
print(binary_search(numbers, 7))   # 3
print(binary_search(numbers, 6))   # -1
```

- 時間複雜度：O(log n)

---

## 14.5 遞迴基礎

> **💡 Tip（小技巧）**：遞迴函式必須有一個明確的終止條件（base case），否則會造成無限遞迴，導致程式崩潰（Stack Overflow）。

### 什麼是遞迴？

**遞迴（Recursion）** 是函式呼叫自己的技術。

```python
def factorial(n):
    """計算階乘"""
    if n <= 1:
        return 1
    return n * factorial(n - 1)

# 5! = 5 * 4 * 3 * 2 * 1 = 120
print(factorial(5))  # 120
```

### 費波那契數列

```python
def fibonacci(n):
    """費波那契數列"""
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

# 0, 1, 1, 2, 3, 5, 8, 13, 21...
for i in range(10):
    print(fibonacci(i), end=" ")
# 0 1 1 2 3 5 8 13 21 34
```

---

## 14.6 Turtle 繪圖：用遞迴畫出美麗圖案

遞迴是畫出美麗幾何圖案的好幫手！我們可以用遞迴來畫出分形圖案。

### 畫出雪花圖案

```python
import turtle

def draw_branch(length):
    """畫出樹枝"""
    if length < 5:
        return
    
    # 畫主幹
    turtle.forward(length)
    turtle.right(20)
    
    # 遞迴畫右側
    draw_branch(length * 0.7)
    
    # 畫左側
    turtle.left(40)
    draw_branch(length * 0.7)
    
    # 回到原點
    turtle.right(20)
    turtle.backward(length)

# 畫出聖誕樹
turtle.speed(0)
turtle.left(90)
draw_branch(100)

turtle.done()
```

### 畫出科赫雪花

```python
import turtle

def koch_curve(length, depth):
    """畫出科赫曲線"""
    if depth == 0:
        turtle.forward(length)
    else:
        length /= 3
        koch_curve(length, depth - 1)
        turtle.left(60)
        koch_curve(length, depth - 1)
        turtle.right(120)
        koch_curve(length, depth - 1)
        turtle.left(60)
        koch_curve(length, depth - 1)

# 畫出雪花
turtle.speed(0)
turtle.penup()
turtle.goto(-150, 100)
turtle.pendown()

for i in range(3):
    koch_curve(300, 3)
    turtle.right(120)

turtle.done()
```

### 練習：畫出圓形分形

```python
import turtle

def draw_circles(size, count):
    """遞迴畫圓"""
    if count == 0:
        return
    
    turtle.circle(size)
    turtle.penup()
    turtle.forward(size * 2)
    turtle.pendown()
    
    draw_circles(size * 0.8, count - 1)

turtle.speed(0)
draw_circles(50, 10)

turtle.done()
```

---

## 14.7 實用範例

### 範例1：找最大值

```python
def find_max(arr):
    """找最大值"""
    if not arr:
        return None
    
    max_val = arr[0]
    for num in arr:
        if num > max_val:
            max_val = num
    return max_val

print(find_max([3, 1, 4, 1, 5, 9, 2, 6]))  # 9
```

### 範例2：計算次數

```python
def count_vowels(text):
    """計算母音數量"""
    vowels = "aeiouAEIOU"
    count = 0
    for char in text:
        if char in vowels:
            count += 1
    return count

print(count_vowels("Hello World"))  # 3
```

### 範例3：反轉字串

```python
def reverse_string(s):
    """反轉字串"""
    return s[::-1]

def reverse_string_manual(s):
    """手動反轉"""
    result = ""
    for char in s:
        result = char + result
    return result

print(reverse_string("hello"))  # olleh
```

---

## 本章小結

| 演算法 | 時間複雜度 | 空間複雜度 |
|--------|------------|------------|
| 氣泡排序 | O(n²) | O(1) |
| 選擇排序 | O(n²) | O(1) |
| 插入排序 | O(n²) | O(1) |
| 快速排序 | O(n log n) | O(log n) |
| 線性搜尋 | O(n) | O(1) |
| 二分搜尋 | O(log n) | O(1) |

---

## 14.7 實用範例 - 小遊戲

### 遊戲 1：數字猜測（使用二分搜尋）

使用二分搜尋演算法的猜數字遊戲！

```python
# 數字猜測遊戲（使用二分搜尋）
# 學習重點：二分搜尋演算法

import random

def binary_search_hint(secret, low, high, guesses):
    """二分搜尋提示"""
    if low > high:
        return None
    
    mid = (low + high) // 2
    
    if mid == secret:
        return mid
    elif mid < secret:
        return mid + 1
    else:
        return mid - 1

print("=" * 50)
print("    🔍 智慧猜數字（提示版）🔍")
print("=" * 50)
print()
print("規則：電腦想一個 1-100 的數字")
print("      你猜測數字，電腦會提示方向")
print("      使用智慧搜尋，最快 7 次猜到！")

secret = random.randint(1, 100)
low, high = 1, 100
guess_count = 0

while True:
    guess_count += 1
    
    # 使用二分搜尋給出建議
    hint_num = binary_search_hint(secret, low, high, guess_count)
    
    print(f"\n範圍：{low} - {high}")
    guess = int(input(f"第 {guess_count} 次猜測（電腦建議 {hint_num}）："))
    
    if guess == secret:
        print(f"\n🎉 猜對了！數字是 {secret}！")
        print(f"你總共猜了 {guess_count} 次")
        break
    elif guess < secret:
        print("📈 太大了！")
        low = max(low, guess + 1)
    else:
        print("📉太小了！")
        high = min(high, guess - 1)
    
    if guess_count >= 10:
        print(f"\n😢 超過 10 次了！數字是 {secret}")
        break
```

---

### 遊戲 2：排序視覺化遊戲

視覺化各種排序演算法！

```python
# 排序視覺化遊戲
# 學習重點：氣泡排序、選擇排序

def bubble_sort_visual(arr):
    """氣泡排序（視覺化）"""
    n = len(arr)
    steps = []
    
    for i in range(n):
        for j in range(0, n - i - 1):
            steps.append((j, j+1, "比較"))
            if arr[j] > arr[j+1]:
                arr[j], arr[j+1] = arr[j+1], arr[j]
                steps.append((j, j+1, "交換"))
    
    return steps

def selection_sort_visual(arr):
    """選擇排序（視覺化）"""
    n = len(arr)
    steps = []
    
    for i in range(n):
        min_idx = i
        for j in range(i+1, n):
            steps.append((min_idx, j, "比較"))
            if arr[j] < arr[min_idx]:
                min_idx = j
        
        if min_idx != i:
            arr[i], arr[min_idx] = arr[min_idx], arr[i]
            steps.append((i, min_idx, "交換"))
    
    return steps

def print_array(arr, highlight=None):
    """顯示陣列"""
    print("|", end="")
    for i, num in enumerate(arr):
        if highlight and i in highlight:
            print(f"*{num}*", end="|")
        else:
            print(f" {num} ", end="|")
    print()

# 遊戲
print("=" * 60)
print("        📊 排序視覺化遊戲 📊")
print("=" * 60)
print()

# 選擇陣列大小
print("選擇難度：")
print("1. 簡單 (5 個數字)")
print("2. 普通 (10 個數字)")
print("3. 困難 (15 數字)")

choice = input("選擇：")

if choice == "1":
    size = 5
elif choice == "2":
    size = 10
else:
    size = 15

import random
numbers = [random.randint(1, 50) for _ in range(size)]
original = numbers.copy()

print(f"\n原始陣列：")
print_array(numbers)

print("\n選擇排序演算法：")
print("1. 氣泡排序")
print("2. 選擇排序")

sort_choice = input("選擇：")

if sort_choice == "1":
    print("\n=== 氣泡排序 ===")
    bubble_sort_visual(numbers)
else:
    print("\n=== 選擇排序 ===")
    selection_sort_visual(numbers)

print(f"\n排序後：")
print_array(numbers)
print()
print(f"原始：{original}")
print(f"排序後：{sorted(original)}")
print("=" * 60)
```

---

## 14.8 本章小結

### 基礎題

1. **最大值**：找出品列中的最大值。
2. **總和**：計算品列中所有元素的總和。
3. **線性搜尋**：實作線性搜尋。
4. **平均值**：計算串列的平均值。
5. **最小值**：找出串列中的最小值。
6. **計數器**：計算串列中某元素出現的次數。
7. **反轉串列**：不使用 reverse() 反轉串列。
8. **判斷是否已排序**：檢查串列是否已由小到大排序。
9. **陣列複製**：複製一個串列到另一個串列。
10. **找第二大數**：找出串列中第二大的數。

### 進階題

1. **二分搜尋**：實作二分搜尋。
2. **氣泡排序**：完成氣泡排序程式碼。
3. **費波那契**：使用遞迴計算費波那契數列。
4. **快速排序**：實作快速排序演算法。
5. **合併排序**：實作合併排序演算法。
6. **選擇排序**：實作選擇排序。
7. **插入排序**：實作插入排序。
8. **二元搜尋樹**：建立簡單的二元搜尋樹。

### 挑戰題

1. **河內塔**：實作河內塔問題的遞迴解法。
2. **動態規劃**：使用動態規劃解決最短路徑問題。
3. **貪心演算法**：實作找零錢的貪心演算法。

---

## 進一步閱讀

### 演算法複雜度

| 符號 | 名稱 | 範例 |
|------|------|------|
| O(1) | 常數時間 | 陣列存取 |
| O(log n) | 對數時間 | 二分搜尋 |
| O(n) | 線性時間 | 遍歷陣列 |
| O(n log n) | 線性對數時間 | 快速排序 |
| O(n²) | 平方時間 | 氣泡排序 |
| O(2ⁿ) | 指數時間 | 費波那契(遞迴) |

### time 模組 - 效能測量

```python
import time

# 測量執行時間
start = time.time()
# ... 執行你的程式 ...
end = time.time()
print(f"執行時間: {end - start} 秒")

# timeit - 精確測量小程式效能
import timeit
result = timeit.timeit("x = sum(range(1000))", number=10000)
print(f"平均時間: {result / 10000} 秒")
```

### functools.lru_cache - 記憶化

```python
from functools import lru_cache

@lru_cache(maxsize=None)
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

# 這個修飾器會快取結果，大幅提升效能
print(fibonacci(100))  # 瞬間完成！
```

### bisect 模組 - 二分搜尋

```python
import bisect

numbers = [1, 3, 5, 7, 9]

# 找插入位置
pos = bisect.bisect_left(numbers, 5)  # → 2
bisect.insort(numbers, 6)            # numbers → [1, 3, 5, 6, 7, 9]
```

### heapq 模組 - 堆積

```python
import heapq

# 建立最小堆
heap = [3, 1, 4, 1, 5, 9, 2, 6]
heapq.heapify(heap)          # 原地轉換為堆
heapq.heappush(heap, 0)      # 插入元素
smallest = heapq.heappop(heap)  # 取出最小值

# 最大堆（使用負數）
max_heap = [-x for x in heap]
heapq.heappush(max_heap, -10)
largest = -heapq.heappop(max_heap)
```

### Python 官方文件

- [排序 HOWTO](https://docs.python.org/3/howto/sorting.html) - 排序演算法教學
- [timeit](https://docs.python.org/3/library/timeit.html) - 效能測量
- [bisect](https://docs.python.org/3/library/bisect.html) - 二分搜尋
- [heapq](https://docs.python.org/3/library/heapq.html) - 堆積佇列

---

*下一章節，我們將學習第 15 章函式式程式設計，這是另一種重要的程式設計範式。*
