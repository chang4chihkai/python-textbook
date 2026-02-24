# 第 15 章｜函式式程式設計

## 學習目標

- 理解函式式程式設計的概念
- 掌握 lambda 匿名函式
- 學會使用 map、filter、reduce
- 能夠使用列表推導式

---

## 15.1 什麼是函式式程式設計？

> **📝 Note（說明）**：**函式式程式設計（Functional Programming）** 是一種強調使用函式進行計算的程式設計範式。其核心思想是將計算視為函式的求值，避免改變資料狀態。

**函式式程式設計（Functional Programming）** 是一種強調使用函式進行計算的程式設計範式。

特點：
- 不改變原始資料
- 函式沒有副作用
- 資料不可變

### 與傳統方式比較

```python
# 傳統方式
numbers = [1, 2, 3, 4, 5]
result = []
for n in numbers:
    result.append(n * 2)
print(result)  # [2, 4, 6, 8, 10]

# 函式式方式
numbers = [1, 2, 3, 4, 5]
result = list(map(lambda x: x * 2, numbers))
print(result)  # [2, 4, 6, 8, 10]
```

---

## 15.2 lambda 匿名函式

> **⚠️ Caution（注意）**：lambda 函式應該保持簡單，如果邏輯太複雜，建議使用正規的 def 函式來定義，這樣程式碼會更易讀和維護。

### 基本語法

```python
# lambda 參數: 運算式
square = lambda x: x ** 2
print(square(5))  # 25

add = lambda a, b: a + b
print(add(3, 5))  # 8
```

### 使用時機

```python
# 當作參數傳遞
numbers = [1, 2, 3, 4, 5]

# 使用在排序
sorted_numbers = sorted(numbers, key=lambda x: -x)
print(sorted_numbers)  # [5, 4, 3, 2, 1]
```

---

## 15.3 map - 對每個元素操作

> **💡 Tip（小技巧）**：`map()` 會返回一個 map 物件（迭代器），需要用 `list()` 轉換為列表。使用 map 可以讓程式碼更簡潔，特別是處理大量資料時。

### 基本語法

```python
# map(函式, 序列)
numbers = [1, 2, 3, 4, 5]

# 計算平方
squares = list(map(lambda x: x ** 2, numbers))
print(squares)  # [1, 4, 9, 16, 25]

# 轉為字串
strings = list(map(str, numbers))
print(strings)  # ['1', '2', '3', '4', '5']
```

---

## 15.4 filter - 篩選元素

> **📝 Note（說明）**：`filter()` 函式會根據指定的條件篩選元素，返回符合條件的元素。與 `map()` 类似，返回的是一個迭代器，需要用 `list()` 轉換。

### 基本語法

```python
# filter(條件函式, 序列)
numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

# 找出偶數
evens = list(filter(lambda x: x % 2 == 0, numbers))
print(evens)  # [2, 4, 6, 8, 10]

# 找出大於 5 的數
over_five = list(filter(lambda x: x > 5, numbers))
print(over_five)  # [6, 7, 8, 9, 10]
```

---

## 15.5 reduce - 聚合運算

> **⚠️ Caution（注意）**：`reduce()` 在 Python 3 中需要從 `functools` 模組匯入。這個函式會將元素序列聚合成單一值，適合用於計算總和、乘積等操作。

### 基本語法

```python
from functools import reduce

# reduce(函式, 序列)
numbers = [1, 2, 3, 4, 5]

# 計算總和
total = reduce(lambda a, b: a + b, numbers)
print(total)  # 15

# 計算乘積
product = reduce(lambda a, b: a * b, numbers)
print(product)  # 120
```

---

## 15.6 列表推導式

> **💡 Tip（小技巧）**：列表推導式是 Python 的特色語法，可以在一行內建立新的列表。與傳統迴圈相比，列表推導式通常更簡潔且執行效率更高。

### 基本語法

```python
# [運算式 for 項目 in 串列]
numbers = [1, 2, 3, 4, 5]

squares = [x ** 2 for x in numbers]
print(squares)  # [1, 4, 9, 16, 25]

# 加上條件
evens = [x for x in numbers if x % 2 == 0]
print(evens)  # [2, 4]
```

### 巢狀列表推導

```python
# 二維矩陣轉一維
matrix = [[1, 2], [3, 4], [5, 6]]
flat = [num for row in matrix for num in row]
print(flat)  # [1, 2, 3, 4, 5, 6]
```

---

## 15.7 字典推導式

```python
# 字典推導式
names = ["小明", "小華", "小美"]
ages = [20, 22, 19]

# 建立姓名到年齡的映射
name_to_age = {name: age for name, age in zip(names, ages)}
print(name_to_age)  # {'小明': 20, '小華': 22, '小美': 19}

# 反轉字典
age_to_name = {age: name for name, age in name_to_age.items()}
print(age_to_name)  # {20: '小明', 22: '小華', 19: '小美'}
```

---

## 15.8 Turtle 繪圖：用函式式程式設計畫圖

學會了函式式程式設計，我們可以用 map、filter、列表推導式來畫圖！

### 用列表推導式畫多個圓

```python
import turtle

# 用列表推導式產生多個圓的半徑
radii = [20, 40, 60, 80, 100]

turtle.speed(0)
turtle.penup()
turtle.goto(-200, 0)
turtle.pendown()

# 用列表推導式畫所有圓
for radius in radii:
    turtle.circle(radius)
    turtle.penup()
    turtle.forward(radius * 2 + 20)
    turtle.pendown()

turtle.done()
```

### 用 map 產生座標

```python
import turtle

# 用 map 產生座標點
def draw_point(x):
    turtle.penup()
    turtle.goto(x, 0)
    turtle.pendown()
    turtle.circle(10)

# 產生 -150 到 150 的 x 座標
x_coords = list(range(-150, 151, 50))

# 用 map 畫出所有點
list(map(draw_point, x_coords))

turtle.done()
```

### 用 filter 篩選要畫的圖

```python
import turtle

# 定義要畫的圖形資料
shapes = [
    {"type": "circle", "size": 50},
    {"type": "square", "size": 30},
    {"type": "circle", "size": 80},
    {"type": "triangle", "size": 40},
    {"type": "circle", "size": 60}
]

# 只畫圓形
circles = filter(lambda s: s["type"] == "circle", shapes)

turtle.speed(0)
for i, shape in enumerate(circles):
    x = -150 + i * 100
    turtle.penup()
    turtle.goto(x, 0)
    turtle.pendown()
    turtle.circle(shape["size"])

turtle.done()
```

---

## 15.9 實用範例

### 範例1：資料處理流程

```python
# 模擬處理學生分數
scores = [85, 90, 78, 92, 65, 88, 95, 70]

# 1. 過濾不及格的
passed = list(filter(lambda x: x >= 60, scores))
print(f"及格：{passed}")

# 2. 加分 5 分
adjusted = list(map(lambda x: min(100, x + 5), passed))
print(f"調整後：{adjusted}")

# 3. 計算平均
from functools import reduce
average = reduce(lambda a, b: a + b, adjusted) / len(adjusted)
print(f"平均：{average:.1f}")
```

### 範例2：文字處理

```python
words = ["hello", "world", "python", "programming"]

# 全部轉大寫
upper = [word.upper() for word in words]
print(upper)  # ['HELLO', 'WORLD', 'PYTHON', 'PROGRAMMING']

# 找長度 >= 6 的
long_words = [word for word in words if len(word) >= 6]
print(long_words)  # ['python', 'programming']

# 產生 (字, 長度) 元組列表
lengths = [(word, len(word)) for word in words]
print(lengths)  # [('hello', 5), ('world', 5), ('python', 6), ('programming', 11)]
```

---

## 本章小結

| 函式 | 用途 |
|------|------|
| `lambda` | 匿名函式 |
| `map()` | 對每個元素操作 |
| `filter()` | 篩選元素 |
| `reduce()` | 聚合運算 |
| 列表推導式 | 快速建立串列 |

---

## 15.7 實用範例 - 小遊戲

### 遊戲 1：資料處理Pipeline遊戲

使用函式式設計的資料處理遊戲！

```python
# 資料處理Pipeline遊戲
# 學習重點：map, filter, reduce, lambda, 列表推導式

from functools import reduce

print("=" * 50)
print("        📊 資料處理Pipeline 📊")
print("=" * 50)
print()

# 玩家資料
players = [
    {"name": "小明", "score": 85, "level": 5},
    {"name": "小華", "score": 92, "level": 7},
    {"name": "小美", "score": 78, "level": 4},
    {"name": "小強", "score": 95, "level": 8},
    {"name": "小李", "score": 67, "level": 3},
    {"name": "小王", "score": 88, "level": 6},
    {"name": "小張", "score": 45, "level": 2},
]

print(f"共有 {len(players)} 位玩家")

# 使用 map 計算每個玩家的總分
def calc_total(player):
    return player["score"] + player["level"] * 10

total_scores = list(map(calc_total, players))

print("\n=== 步驟1：計算總分 ===")
for p, ts in zip(players, total_scores):
    print(f"{p['name']}: 積分{p['score']}+等級{p['level']}*10 = {ts}")

# 使用 filter 篩選高分玩家
high_scorers = list(filter(lambda p: p["score"] >= 80, players))

print("\n=== 步驟2：篩選高分玩家 (>=80) ===")
for p in high_scorers:
    print(f"{p['name']}: {p['score']} 分")

# 使用 map 轉換資料
def to_badge(player):
    if player["score"] >= 90:
        return f"{player['name']} 🌟金牌"
    elif player["score"] >= 80:
        return f"{player['name']} 🥈銀牌"
    else:
        return f"{player['name']} 🥉銅牌"

badges = list(map(to_badge, players))

print("\n=== 步驟3：頒發獎牌 ===")
for badge in badges:
    print(badge)

# 使用 reduce 計算總分
total = reduce(lambda acc, p: acc + p["score"], players, 0)
avg = total / len(players)

print("\n=== 統計資料 ===")
print(f"總分：{total}")
print(f"平均：{avg:.1f}")

# 使用列表推導式
power_players = [p["name"] for p in players if p["level"] >= 5]

print("\n=== 列表推導式：高等級玩家 ===")
print(f"高等級玩家 (level >= 5): {power_players}")
```

---

### 遊戲 2：函數冒險遊戲

使用lambda和函式式的文字冒險！

```python
# 函數冒險遊戲
# 學習重點：lambda, map, filter, reduce

from functools import reduce

print("=" * 50)
print("        🗡️ 函數冒險 🗡️")
print("=" * 50)
print()

# 怪物資料
monsters = [
    {"name": "哥布林", "hp": 30, "attack": 10, "exp": 20},
    {"name": "狼", "hp": 40, "attack": 15, "exp": 30},
    {"name": "史萊姆", "hp": 20, "attack": 5, "exp": 10},
    {"name": "獸人", "hp": 50, "attack": 20, "exp": 40},
    {"name": "龍", "hp": 100, "attack": 30, "exp": 100},
]

print("=== 怪物列表 ===")
for m in monsters:
    print(f"{m['name']}: HP {m['hp']}, ATK {m['attack']}, EXP {m['exp']}")

# 使用 filter 篩選強敵
strong_monsters = list(filter(lambda m: m["attack"] >= 15, monsters))

print("\n=== 強敵 (ATK >= 15) ===")
for m in strong_monsters:
    print(m["name"])

# 使用 map 計算經驗值
def calc_exp_reward(monster, player_level):
    return monster["exp"] * (1 + player_level * 0.1)

player_level = 5
exp_rewards = list(map(lambda m: calc_exp_reward(m, player_level), monsters))

print(f"\n=== 等級 {player_level} 的經驗獎勵 ===")
for m, exp in zip(monsters, exp_rewards):
    print(f"{m['name']}: {int(exp)} EXP")

# 使用 reduce 計算總戰力
total_power = reduce(lambda acc, m: acc + m["hp"] + m["attack"], monsters, 0)

print(f"\n=== 總戰力 ===")
print(f"所有怪物總戰力：{total_power}")

# 列表推導式
high_exp_monsters = [{"name": m["name"], "exp": m["exp"]} for m in monsters if m["exp"] >= 30]

print(f"\n=== 高經驗怪物 (EXP >= 30) ===")
for m in high_exp_monsters:
    print(f"{m['name']}: {m['exp']} EXP")
```

---

## 練習題

### 基礎題

1. **平方計算**：使用 map 計算 1-10 的平方。
2. **篩選**：使用 filter 找出 1-20 中的質數。
3. **加總**：使用 reduce 計算列表總和。
4. **列表推導式**：使用列表推導式產生 1-20 的偶數。
5. **Lambda 基本**：用 lambda 撰寫平方函式。
6. **Map 應用**：用 map 將串列中所有字串轉為大寫。
7. **Filter 應用**：用 filter 篩選長度大於 5 的單字。
8. **Reduce 應用**：用 reduce 找串列最大值。
9. **字典推導式**：將兩個串列合併為字典。
10. **雙重列表推導**：產生九九乘法表。

### 進階題

1. **資料處理流程**：模擬成績處理的完整流程。
2. **文字分析**：統計文章中每個詞的長度。
3. **重構**：將傳統 for 迴圈改為函式式写法。
4. **Pipeline**：建立一個簡單的資料處理 Pipeline。
5. **組合應用**：結合 map、filter、reduce 處理複雜問題。
6. **複雜資料轉換**：將嵌套資料結構進行轉換。
7. **多階段處理**：模擬 ETL 資料處理流程。
8. **自訂排序**：使用 lambda 進行多鍵排序。

### 挑戰題

1. **函式庫實作**：實作自己的簡易 map、filter、reduce。
2. **Pipeline 框架**：建立可擴充的資料處理 Pipeline 框架。
3. ** Lazy 評估**：實作產生器版本的函式式工具。

---

## 進一步閱讀

### 更多高階函式

```python
from functools import reduce, partial

# partial - 部分應用
def power(base, exponent):
    return base ** exponent

square = partial(power, exponent=2)
cube = partial(power, exponent=3)

square(5)   # → 25
cube(2)     # → 8

# reduce - 累積運算
reduce(lambda x, y: x + y, [1, 2, 3, 4, 5])  # → 15
reduce(lambda x, y: x * y, [1, 2, 3, 4, 5])  # → 120
```

### itertools 函式式工具

```python
import itertools

# accumulate - 累積
list(itertools.accumulate([1, 2, 3, 4, 5]))
# [1, 3, 6, 10, 15]

# starmap - 解包參數
list(itertools.starmap(pow, [(2, 3), (3, 2)]))
# [8, 9]

# takewhile, dropwhile
list(itertools.takewhile(lambda x: x < 5, [1, 4, 5, 6]))
# [1, 4]

list(itertools.dropwhile(lambda x: x < 5, [1, 4, 5, 6]))
# [5, 6]
```

### 裝飾器

```python
# 基本裝飾器
def timer(func):
    def wrapper(*args, **kwargs):
        import time
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} 執行時間: {end - start}")
        return result
    return wrapper

@timer
def slow_function():
    import time
    time.sleep(1)

# 帶參數的裝飾器
def retry(times=3):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for i in range(times):
                try:
                    return func(*args, **kwargs)
                except:
                    if i == times - 1:
                        raise
            return wrapper
        return decorator
    return decorator

@retry(times=5)
def unstable():
    pass
```

### 生成器與 yield

```python
# 基本生成器
def countdown(n):
    while n > 0:
        yield n
        n -= 1

# for x in countdown(5):  # 5, 4, 3, 2, 1

# 生成器表達式
gen = (x ** 2 for x in range(10) if x % 2 == 0)
# 0, 4, 16, 36, 64

# itertools 生成器
import itertools
list(itertools.filterfalse(lambda x: x % 2 == 0, range(10)))
# [1, 3, 5, 7, 9]
```

### Python 官方文件

- [functools](https://docs.python.org/3/library/functools.html) - 函式式工具
- [itertools](https://docs.python.org/3/library/itertools.html) - 迭代器工具
- [生成器](https://docs.python.org/3/howto/functional.html#generators) - 生成器教學

---

*下一章節，我們將學習第 16 章實用工具與技巧，提升開發效率。*
