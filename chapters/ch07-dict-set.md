# 第 7 章｜字典與集合

## 學習目標

- 理解字典（Dictionary）的概念與使用
- 掌握字典的基本操作：新增、刪除、修改、查詢
- 理解集合（Set）的概念
- 學會集合的運算：聯集、交集、差集
- 能夠根據情境選擇合適的資料結構

---

## 7.1 什麼是字典？

> **📝 Note（說明）**：字典的鍵（Key）必須是不可變的資料型態，如字串、數字或元組。值（Value）可以是任何資料型態。

**字典（Dictionary）** 是一種鍵值對（Key-Value）的資料結構，就像現實生活中的字典：
- 查詢「蘋果」這個詞 → 得到解釋
- 查詢某個 key → 得到對應的 value

```
字典：{鍵1: 值1, 鍵2: 值2, 鍵3: 值3}
```

### 建立字典

```python
# 建立字典
student = {
    "name": "小明",
    "age": 20,
    "department": "資工系"
}

print(student)
print(student["name"])   # 小明
```

### 字典 vs 串列

| 特性 | 串列 | 字典 |
|------|------|------|
| 存取方式 | 索引（數字） | 鍵（可為字串、數字等） |
| 順序 | 有序 | Python 3.7+ 有序 |
| 用途 | 順序存放多筆資料 | 建立映射關係 |

---

## 7.2 字典基本操作

### 新增與修改

```python
person = {}

# 新增鍵值對
person["name"] = "小華"
person["age"] = 25
person["city"] = "台北"

print(person)  # {'name': '小華', 'age': 25, 'city': '台北'}

# 修改現有鍵的值
person["age"] = 26
print(person)  # {'name': '小華', 'age': 26, 'city': '台北'}
```

### 存取

```python
student = {"name": "小明", "age": 20, "score": 85}

# 方式1：直接存取（鍵不存在會錯誤）
print(student["name"])   # 小明

# 方式2：get 方法（鍵不存在回傳 None 或指定值）
print(student.get("name"))      # 小明
print(student.get("height"))    # None
print(student.get("height", 170))  # 170（預設值）
```

### 刪除

```python
person = {"name": "小明", "age": 20, "city": "台北"}

# 刪除指定鍵
del person["age"]
print(person)   # {'name': '小明', 'city': '台北'}

# pop - 刪除並取得值
city = person.pop("city")
print(city)     # 台北
print(person)   # {'name': '小明'}
```

---

## 7.3 字典遍歷

### 遍歷所有鍵值對

```python
student = {"name": "小明", "age": 20, "department": "資工系"}

# 遍歷鍵
for key in student:
    print(key)

# 遍歷值
for value in student.values():
    print(value)

# 遍歷鍵值對
for key, value in student.items():
    print(f"{key}: {value}")
```

### 常用方法

```python
student = {"name": "小明", "age": 20, "department": "資工系"}

print(len(student))           # 3（鍵值對數量）
print("name" in student)      # True（鍵是否存在）
print(list(student.keys()))   # ['name', 'age', 'department']
print(list(student.values())) # ['小明', 20, '資工系']
print(list(student.items()))   # [('name', '小明'), ('age', 20), ...]
```

---

## 7.4 什麼是集合？

**集合（Set）** 是不重複元素的無序集合。

```
集合：{元素1, 元素2, 元素3, ...}
```

### 建立集合

```python
# 建立集合
fruits = {"apple", "banana", "cherry"}
print(fruits)   # {'banana', 'apple', 'cherry'}（順序可能不同）

# 從串列建立（自動去除重複）
numbers = [1, 2, 2, 3, 3, 3, 4]
unique = set(numbers)
print(unique)   # {1, 2, 3, 4}

# 空集合
empty_set = set()   # 不能用 {}，那是空字典
empty_dict = {}
```

---

## 7.5 集合操作

### 新增與刪除

```python
fruits = {"apple", "banana"}

fruits.add("cherry")      # 新增元素
fruits.add("apple")      # 重複不會有作用
print(fruits)            # {'apple', 'banana', 'cherry'}

fruits.remove("banana")  # 移除元素（不存在會錯誤）
print(fruits)            # {'apple', 'cherry'}

fruits.discard("orange") # 移除元素（不存在不會錯誤）
print(fruits)            # {'apple', 'cherry'}

fruits.clear()           # 清空集合
print(fruits)            # set()
```

### 集合運算

```python
A = {1, 2, 3, 4}
B = {3, 4, 5, 6}

print(A | B)      # 聯集：{1, 2, 3, 4, 5, 6}
print(A & B)      # 交集：{3, 4}
print(A - B)      # 差集（A 有 B 沒有的）：{1, 2}
print(A ^ B)      # 對稱差集：{1, 2, 5, 6}
```

### 子集與超集

```python
A = {1, 2, 3}
B = {1, 2, 3, 4, 5}

print(A <= B)     # True（A 是 B 的子集）
print(A < B)      # True（A 是 B 的真子集）
print(B >= A)     # True（B 是 A 的超集）
```

---

## 7.6 Turtle 繪圖：用字典管理圖形樣式

字典可以幫我們儲存圖形的各種屬性，例如位置、顏色、大小等，讓我們能夠輕鬆管理複雜的圖形！

### 用字典描述圖形

```python
import turtle

# 用字典描述一個圓形
circle = {
    "type": "circle",
    "radius": 50,
    "color": "red",
    "position": (0, 0)
}

# 根據字典內容畫圖
turtle.penup()
turtle.goto(circle["position"])
turtle.pendown()
turtle.color(circle["color"])
turtle.circle(circle["radius"])

turtle.done()
```

### 用字典串列畫出多個圖案

```python
import turtle

# 用字典串列描述多個圖形
shapes = [
    {"type": "circle", "radius": 30, "color": "red", "pos": (-100, 0)},
    {"type": "square", "size": 60, "color": "green", "pos": (0, 0)},
    {"type": "triangle", "size": 60, "color": "blue", "pos": (100, 0)}
]

# 依序畫出每個圖形
for shape in shapes:
    turtle.penup()
    turtle.goto(shape["pos"])
    turtle.pendown()
    turtle.color(shape["color"])
    
    if shape["type"] == "circle":
        turtle.circle(shape["radius"])
    elif shape["type"] == "square":
        for i in range(4):
            turtle.forward(shape["size"])
            turtle.right(90)
    elif shape["type"] == "triangle":
        for i in range(3):
            turtle.forward(shape["size"])
            turtle.right(120)

turtle.done()
```

### 用集合去除重複的顏色

```python
import turtle

# 定義多個顏色（有些重複）
all_colors = ["red", "blue", "red", "green", "blue", "yellow", "green", "red"]

# 用集合去除重複
unique_colors = set(all_colors)
print(f"所有顏色: {all_colors}")
print(f"不重複的顏色: {unique_colors}")

# 用不重複的顏色畫圖
turtle.speed(0)
for i, color in enumerate(unique_colors):
    turtle.color(color)
    turtle.circle(30 + i * 10)

turtle.done()
```

### 練習：畫出角色家族

```python
import turtle

# 用字典描述每個角色
characters = [
    {"name": "爸爸", "size": 100, "color": "blue", "y": 50},
    {"name": "媽媽", "size": 90, "color": "pink", "y": -20},
    {"name": "小孩", "size": 60, "color": "yellow", "y": -80}
]

# 畫出每個角色（用圓形代表頭）
for char in characters:
    turtle.penup()
    turtle.goto(0, char["y"])
    turtle.pendown()
    turtle.color(char["color"])
    turtle.begin_fill()
    turtle.circle(char["size"] / 2)
    turtle.end_fill()

turtle.done()
```

---

## 7.7 實用範例

### 範例1：通訊錄系統

```python
# 通訊錄字典
contacts = {
    "小明": "0912345678",
    "小華": "0987654321",
    "小美": "0977123456"
}

# 新增聯絡人
contacts["老師"] = "0223456789"

# 查詢
name = input("請輸入姓名：")
if name in contacts:
    print(f"{name} 的電話：{contacts[name]}")
else:
    print("找不到此聯絡人")
```

### 範例2：統計字元出現次數

```python
# 統計字串中每個字元出現次數
text = "hello world"

counter = {}
for char in text:
    if char != " ":  # 忽略空格
        counter[char] = counter.get(char, 0) + 1

print(counter)  # {'h': 1, 'e': 1, 'l': 3, 'o': 2, 'w': 1, 'r': 1, 'd': 1}

# 排序輸出
for char, count in sorted(counter.items()):
    print(f"'{char}': {count} 次")
```

### 範例3：找出共同好友

```python
# 兩位使用者的好友名單
friends_A = {"小明", "小華", "小美", "小強", "小陳"}
friends_B = {"小美", "小強", "小王", "小張"}

# 共同好友
common = friends_A & friends_B
print("共同好友：", common)

# A 專屬好友
only_A = friends_A - friends_B
print("A 的專屬好友：", only_A)

# 合併所有好友
all_friends = friends_A | friends_B
print("所有好友：", all_friends)
```

### 範例4：成績查詢系統

```python
# 學生成績字典
scores = {
    "小明": 85,
    "小華": 92,
    "小美": 78,
    "小強": 90
}

# 查詢並顯示等第
name = input("請輸入學生姓名：")
if name in scores:
    score = scores[name]
    if score >= 90:
        grade = "A"
    elif score >= 80:
        grade = "B"
    elif score >= 70:
        grade = "C"
    elif score >= 60:
        grade = "D"
    else:
        grade = "F"
    print(f"{name} 的成績：{score} 分，等第：{grade}")
else:
    print("找不到此學生")
```

---

## 7.7 實用範例 - 小遊戲

### 遊戲 1：寶可夢戰鬥系統

使用字典設計的寶可夢戰鬥系統！

```python
# 寶可夢戰鬥系統
# 學習重點：字典操作、集合運算

import random
import time

print("=" * 50)
print("        ⚔️ 寶可夢戰鬥 ⚔️")
print("=" * 50)
print()

# 寶可夢資料庫（使用字典儲存）
pokemons = {
    "小火龍": {
        "屬性": "火",
        "HP": 100,
        "攻擊": 80,
        "防禦": 70,
        "技能": ["火花", "燃燒", "爆炸"]
    },
    "傑尼龜": {
        "屬性": "水",
        "HP": 110,
        "攻擊": 65,
        "防禦": 85,
        "技能": ["水槍", "泡沫", "水波"]
    },
    "妙蛙種子": {
        "屬性": "草",
        "HP": 105,
        "攻擊": 70,
        "防禦": 80,
        "技能": ["藤鞭", "寄生", "飛葉"]
    },
    "皮卡丘": {
        "屬性": "電",
        "HP": 90,
        "攻擊": 95,
        "防禦": 60,
        "技能": ["十萬伏特", "電光一閃", "打雷"]
    },
    "卡比獸": {
        "屬性": "一般",
        "HP": 150,
        "攻擊": 75,
        "防禦": 90,
        "技能": ["泰山壓頂", "睡覺", "破壞死光"]
    }
}

# 屬性相剋（使用字典）
type_effectiveness = {
    "火": {"草": 2.0, "水": 0.5, "火": 0.5},
    "水": {"火": 2.0, "草": 0.5, "水": 0.5},
    "草": {"水": 2.0, "火": 0.5, "草": 0.5},
    "電": {"水": 2.0, "草": 0.5, "電": 0.5},
    "一般": {"一般": 1.0}
}

def show_pokemons():
    """顯示可選的寶可夢"""
    print("可選的寶可夢：")
    for i, (name, data) in enumerate(pokemons.items(), 1):
        print(f"  {i}. {name} (HP:{data['HP']} 攻擊:{data['攻擊']} 防禦:{data['防禦']})")

def calculate_damage(attacker, defender, skill):
    """計算傷害"""
    attacker_data = pokemons[attacker]
    defender_data = pokemons[defender]
    
    # 基礎傷害
    base_damage = attacker_data["攻擊"]
    
    # 屬性相剋
    attacker_type = attacker_data["屬性"]
    defender_type = defender_data["屬性"]
    multiplier = type_effectiveness.get(attacker_type, {}).get(defender_type, 1.0)
    
    # 隨機變化
    random_factor = random.uniform(0.85, 1.0)
    
    # 計算最終傷害
    damage = int(base_damage * multiplier * random_factor)
    
    return damage, multiplier

# 選擇寶可夢
show_pokemons()
print()

player_pokemon = input("請選擇你的寶可夢（輸入名稱）：")

if player_pokemon not in pokemons:
    print("無效的選擇，預設選擇小火龍！")
    player_pokemon =小火龍"

# 電腦選擇（排除玩家選擇）
available_pokemons = [p for p in pokemons.keys() if p != player_pokemon]
computer_pokemon = random.choice(available_pokemons)

# 建立戰鬥用的副本
player_hp = pokemons[player_pokemon]["HP"]
computer_hp = pokemons[computer_pokemon]["HP"]

print()
print("=" * 50)
print(f"⚔️ 戰鬥開始！")
print(f"你選擇了 {player_pokemon}！")
print(f"電腦選擇了 {computer_pokemon}！")
print("=" * 50)
print()

# 戰鬥迴圈
round_num = 1
while player_hp > 0 and computer_hp > 0:
    print(f"=== 第 {round_num} 回合 ===")
    print(f"{player_pokemon}: {player_hp} HP | {computer_pokemon}: {computer_hp} HP")
    print()
    
    # 玩家選擇技能
    player_skills = pokemons[player_pokemon]["技能"]
    print("選擇技能：")
    for i, skill in enumerate(player_skills, 1):
        print(f"  {i}. {skill}")
    
    skill_choice = int(input("請選擇技能 (1-3)：")) - 1
    player_skill = player_skills[skill_choice]
    
    # 玩家攻擊
    damage, multiplier = calculate_damage(player_pokemon, computer_pokemon, player_skill)
    computer_hp = max(0, computer_hp - damage)
    
    print(f"\n{player_pokemon} 使用 {player_skill}！")
    if multiplier > 1:
        print(f"💥 屬性相剋！傷害 x{multiplier}！")
    print(f"造成 {damage} 傷害！")
    
    if computer_hp <= 0:
        break
    
    # 電腦攻擊
    computer_skills = pokemons[computer_pokemon]["技能"]
    computer_skill = random.choice(computer_skills)
    
    damage, multiplier = calculate_damage(computer_pokemon, player_pokemon, computer_skill)
    player_hp = max(0, player_hp - damage)
    
    print(f"\n{computer_pokemon} 使用 {computer_skill}！")
    if multiplier > 1:
        print(f"💥 屬性相剋！傷害 x{multiplier}！")
    print(f"造成 {damage} 傷害！")
    
    print()
    round_num = round_num + 1
    time.sleep(1)

# 結果
print()
print("=" * 50)
if player_hp > 0:
    print(f"🎉 你獲勝了！")
    print(f"{computer_pokemon} 被打敗了！")
else:
    print(f"😢 你輸了...")
    print(f"{player_pokemon} 被打敗了！")
print("=" * 50)

---

### 遊戲 2：會員資料管理系統

使用字典設計的會員系統！

```python
# 會員資料管理系統
# 學習重點：字典操作 CRUD、集合應用

# 會員資料庫
members = {}

def register():
    """註冊新會員"""
    print("\n--- 會員註冊 ---")
    member_id = input("請輸入會員編號：")
    
    if member_id in members:
        print("❌ 此編號已被使用！")
        return
    
    name = input("請輸入姓名：")
    age = input("請輸入年齡：")
    email = input("請輸入 Email：")
    
    # 建立會員資料
    members[member_id] = {
        "姓名": name,
        "年齡": age,
        "Email": email,
        "購物金": 0,
        "購買記錄": []
    }
    
    print(f"✅ 會員 {name} 註冊成功！")

def login():
    """會員登入"""
    print("\n--- 會員登入 ---")
    member_id = input("請輸入會員編號：")
    
    if member_id not in members:
        print("❌ 會員編號不存在！")
        return None
    
    print(f"✅ 歡迎回來，{members[member_id]['姓名']}！")
    return member_id

def show_info(member_id):
    """顯示會員資料"""
    member = members[member_id]
    print("\n--- 會員資料 ---")
    print(f"編號：{member_id}")
    print(f"姓名：{member['姓名']}")
    print(f"年齡：{member['年齡']}")
    print(f"Email：{member['Email']}")
    print(f"購物金：{member['購物金']} 元")
    print(f"購買次數：{len(member['購買記錄'])}")

def add_balance(member_id):
    """儲值"""
    print("\n--- 儲值 ---")
    amount = int(input("請輸入儲值金額："))
    
    if amount > 0:
        members[member_id]["購物金"] = members[member_id]["購物金"] + amount
        print(f"✅ 儲值成功！目前餘額：{members[member_id]['購物金']} 元")
    else:
        print("❌ 金額必須為正數！")

def purchase(member_id):
    """購物"""
    print("\n--- 購物 ---")
    product = input("請輸入商品名稱：")
    price = int(input("請輸入商品價格："))
    
    balance = members[member_id]["購物金"]
    
    if price > balance:
        print(f"❌ 餘額不足！需要 {price} 元，目前餘額 {balance} 元")
        return
    
    # 扣款並記錄
    members[member_id]["購物金"] = balance - price
    members[member_id]["購買記錄"].append({
        "商品名": product,
        "價格": price
    })
    
    print(f"✅ 購買成功！{product} - {price} 元")
    print(f"   剩餘餘額：{members[member_id]['購物金']} 元")

def show_purchase_history(member_id):
    """顯示購買記錄"""
    member = members[member_id]
    print("\n--- 購買記錄 ---")
    
    if not member["購買記錄"]:
        print("尚未購買任何商品！")
        return
    
    for i, record in enumerate(member["購買記錄"], 1):
        print(f"{i}. {record['商品名']} - {record['價格']} 元")

# 主程式
print("=" * 50)
print("     🛒 會員管理系統 🛒")
print("=" * 50)

while True:
    print("\n選項：")
    print("  1. 註冊會員")
    print("  2. 會員登入")
    print("  3. 顯示所有會員")
    print("  0. 離開")
    
    choice = input("請選擇：")
    
    if choice == "1":
        register()
    elif choice == "2":
        member_id = login()
        if member_id:
            while True:
                print("\n會員功能：")
                print("  1. 顯示資料")
                print("  2. 儲值")
                print("  3. 購物")
                print("  4. 購買記錄")
                print("  0. 登出")
                
                sub_choice = input("請選擇：")
                
                if sub_choice == "1":
                    show_info(member_id)
                elif sub_choice == "2":
                    add_balance(member_id)
                elif sub_choice == "3":
                    purchase(member_id)
                elif sub_choice == "4":
                    show_purchase_history(member_id)
                elif sub_choice == "0":
                    break
                else:
                    print("無效的選擇！")
    elif choice == "3":
        print("\n所有會員：")
        for id, data in members.items():
            print(f"  {id}: {data['姓名']}")
    elif choice == "0":
        print("感謝使用！")
        break
    else:
        print("無效的選擇！")
```

---

## 7.8 本章小結

| 資料結構 | 語法 | 用途 |
|----------|------|------|
| 字典 | `{key: value}` | 建立鍵值對映射 |
| 集合 | `{1, 2, 3}` | 存放不重複元素 |

| 字典操作 | 語法 |
|----------|------|
| 存取 | `dict[key]`, `dict.get(key)` |
| 新增/修改 | `dict[key] = value` |
| 刪除 | `del dict[key]`, `dict.pop(key)` |
| 遍歷 | `for k, v in dict.items()` |

| 集合運算 | 語法 |
|----------|------|
| 聯集 | `A \| B` |
| 交集 | `A & B` |
| 差集 | `A - B` |
| 對稱差集 | `A ^ B` |

---

## 練習題

### 基礎題

1. **字典操作**：建立學生成績字典，查詢特定學生成績。
2. **集合建立**：從輸入的字串中找出不重複的字元。
3. **好友分析**：練習集合的交集、聯集運算。
4. **字典新增**：建立字典並新增鍵值對。
5. **字典遍歷**：遍歷字典的所有鍵並輸出。
6. **集合大小**：建立集合並使用 len() 取得元素個數。
7. **集合新增**：練習 add() 和 update() 方法。
8. **字典取得**：使用 get() 方法安全取得字典值。
9. **字典刪除**：刪除字典中的指定鍵值對。
10. **集合清空**：建立集合後練習 clear() 方法。

### 進階題

1. **統計字母**：統計一段文字中每個英文字母出現次數。
2. **生日記錄簿**：使用字典儲存多位聯絡人的姓名和生日。
3. **去除重複**：將兩個串列合併並去除重複元素。
4. **詞頻分析**：讀取一段文章，統計每個詞出現的次數並排序。
5. **會員系統**：實作會員註冊、登入、查詢功能。
6. **字典排序**：將字典按鍵或值進行排序。
7. **集合比較**：判斷兩個集合是否有交集或子集關係。
8. **通訊錄管理**：使用字典實作簡單的通訊錄系統。

### 挑戰題

1. **反向字典**：將 {a:1, b:2, c:3} 轉換為 {1:a, 2:b, 3:c}。
2. **分組統計**：根據年齡將人員分組統計人數。
3. **電影評分系統**：使用字典儲存電影和評分，計算平均分數。

---

## 進一步閱讀

### 字典常用方法

```python
student = {"name": "Alice", "age": 20, "grade": "A"}

# 存取與修改
student.get("name")           # 取得值，不存在回傳 None
student.get("school", "NTU")  # 預設值
student.setdefault("city", "Taipei")  # 不存在則設定

# 新增與更新
student.update({"age": 21, "school": "NTU"})  # 批量更新

# 移除
student.pop("age")            # 移除並回傳
student.popitem()             # 移除最後一對

# 檢查
"name" in student             # 檢查鍵是否存在
```

### 集合常用方法

```python
fruits = {"apple", "banana", "cherry"}

fruits.add("orange")         # 新增元素
fruits.remove("banana")       # 移除（不存在會錯誤）
fruits.discard("grape")      # 移除（不存在不錯誤）
fruits.pop()                 # 隨機移除一個
fruits.clear()              # 清空集合

# 集合運算
A = {1, 2, 3}
B = {2, 3, 4}

A | B        # 聯集 {1, 2, 3, 4}
A & B        # 交集 {2, 3}
A - B        # 差集 {1}
A ^ B        # 對稱差集 {1, 4}
```

### 字典視為式

```python
# 基本語法
squares = {x: x**2 for x in range(5)}
# {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}

# 條件過濾
even_squares = {x: x**2 for x in range(10) if x % 2 == 0}
# {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}
```

### 集合生成式

```python
# 基本語法
squares = {x**2 for x in range(5)}
# {0, 1, 4, 9, 16}

# 過濾
even_squares = {x**2 for x in range(10) if x % 2 == 0}
# {0, 4, 16, 36, 64}
```

### Python 官方文件

- [字典](https://docs.python.org/3/library/stdtypes.html#dict) - 字典完整說明
- [集合](https://docs.python.org/3/library/stdtypes.html#set) - 集合說明
- [types.MappingProxyType](https://docs.python.org/3/library/types.html#types.MappingProxyType) - 唯讀字典

---

*下一章節，我們將學習字串處理，這是程式設計中非常重要的技能。*
