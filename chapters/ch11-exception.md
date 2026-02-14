# 第 11 章｜例外處理

## 學習目標

- 理解什麼是例外
- 掌握 try-except 語法
- 學會處理多種例外類型
- 能夠自訂例外類別

---

## 11.1 什麼是例外？

> **📝 Note（說明）**：**例外（Exception）** 是程式執行時發生的錯誤，會中斷程式的正常執行。

**例外（Exception）** 是程式執行時發生的錯誤，會中斷程式的正常執行。

```python
# 常見的錯誤
print(10 / 0)        # ZeroDivisionError：除以零
print(int("abc"))   # ValueError：值錯誤
print(x)            # NameError：名稱錯誤
```

### 不處理例外的情況

> **⚠️ Caution（注意）**：如果不安善處理例外，程式會直接崩潰並顯示錯誤訊息，這對使用者來說是不好的體驗。

```python
def divide(a, b):
    return a / b

result = divide(10, 0)  # 程式會崩潰！
```

---

## 10.2 try-except 基本語法

> **💡 Tip（小技巧）**：使用 `try-except` 語法可以讓程式在發生錯誤時優雅地處理，而不是直接崩潰。

### 語法結構

```python
try:
    # 可能發生錯誤的程式碼
    risky_code()
except ExceptionType:
    # 發生錯誤時執行的程式碼
    handle_error()
```

### 範例：除法運算

```python
def safe_divide(a, b):
    try:
        result = a / b
        print(f"結果：{result}")
    except ZeroDivisionError:
        print("錯誤：不能除以零！")

safe_divide(10, 2)   # 結果：5.0
safe_divide(10, 0)   # 錯誤：不能除以零！
```

---

## 10.3 多個 except

### 處理多種錯誤

```python
def process_input():
    try:
        num = int(input("請輸入數字："))
        result = 10 / num
        print(f"10 / {num} = {result}")
    except ValueError:
        print("錯誤：請輸入有效的數字！")
    except ZeroDivisionError:
        print("錯誤：不能輸入零！")

process_input()
```

### 擷取錯誤訊息

```python
try:
    x = int(input("數字："))
except ValueError as e:
    print(f"發生錯誤：{e}")
    print(f"錯誤類型：{type(e).__name__}")
```

---

## 10.4 else 與 finally

> **📝 Note（說明）**：`else` 區塊在沒有發生例外時執行，`finally` 區塊無論是否有例外都會執行，常用於清理資源。

### 完整語法

```python
try:
    # 可能發生錯誤的程式碼
    risky_code()
except Exception1:
    # 處理 Exception1
    handle_error1()
except Exception2:
    # 處理 Exception2
    handle_error2()
else:
    # 沒有發生錯誤時執行
    success_code()
finally:
    # 無論是否有錯誤都會執行
    cleanup_code()
```

### 範例

```python
def read_number():
    try:
        num = int(input("請輸入數字："))
    except ValueError:
        print("輸入無效！")
    else:
        print(f"你輸入的是：{num}")
    finally:
        print("感謝使用！")
```

---

## 10.5 常見例外類型

| 例外類型 | 說明 |
|----------|------|
| `ZeroDivisionError` | 除以零 |
| `ValueError` | 值錯誤 |
| `TypeError` | 型態錯誤 |
| `IndexError` | 索引錯誤 |
| `KeyError` | 鍵錯誤 |
| `FileNotFoundError` | 檔案不存在 |
| `AttributeError` | 屬性錯誤 |

### 取得所有錯誤訊息

```python
try:
    # 可能有問題的程式碼
    pass
except Exception as e:
    print(f"錯誤類型：{type(e).__name__}")
    print(f"錯誤訊息：{e}")
```

---

## 10.6 主動拋出例外

> **💡 Tip（小技巧）**：使用 `raise` 語法可以主動拋出例外，這在驗證輸入或實作業務邏輯時非常有用。

### raise 語法

```python
def set_age(age):
    if age < 0:
        raise ValueError("年齡不能為負數！")
    if age > 150:
        raise ValueError("年齡不合理！")
    return age

try:
    print(set_age(25))
    print(set_age(-5))   # 會拋出例外
except ValueError as e:
    print(f"錯誤：{e}")
```

---

## 10.7 自訂例外類別

> **📝 Note（說明）**：自訂例外類別可以讓程式碼更有結構性，幫助開發者區分不同類型的錯誤，並提供更精確的錯誤訊息。

### 建立自己的例外

```python
class AgeError(Exception):
    """年齡相關的錯誤"""
    pass

class NegativeAgeError(AgeError):
    """年齡為負數的錯誤"""
    pass

def set_age(age):
    if age < 0:
        raise NegativeAgeError("年齡不能為負數！")
    if age > 150:
        raise AgeError("年齡不合理！")
    return age

try:
    set_age(-5)
except NegativeAgeError as e:
    print(f"負數年齡錯誤：{e}")
except AgeError as e:
    print(f"年齡錯誤：{e}")
```

---

## 10.8 實用範例

> **📝 Note（說明）**：學會了例外處理，我們可以讓 Turtle 程式更加安全，當使用者輸入無效的值時不會程式崩潰！

### 安全的 Turtle 畫圖程式

```python
import turtle

def safe_draw_shape():
    """安全的畫圖程式"""
    try:
        sides = int(input("你要畫幾邊形 (3-10): "))
        if sides < 3 or sides > 10:
            raise ValueError("邊數必須在 3-10 之間")
        
        length = int(input("邊長: "))
        if length <= 0:
            raise ValueError("邊長必須是正數")
        
        # 畫多邊形
        angle = 360 / sides
        for i in range(sides):
            turtle.forward(length)
            turtle.right(angle)
            
    except ValueError as e:
        print(f"輸入錯誤：{e}")
    except Exception as e:
        print(f"發生錯誤：{e}")
    finally:
        print("程式結束")

safe_draw_shape()
turtle.done()
```

### 練習：安全的圓形畫圖

```python
import turtle

def safe_circle():
    try:
        radius = int(input("輸入半徑 (10-200): "))
        if radius < 10 or radius > 200:
            raise ValueError("半徑必須在 10-200 之間")
        
        turtle.circle(radius)
        
    except ValueError as e:
        print(f"錯誤：{e}")
        print("畫一個預設大小的圓")
        turtle.circle(50)

safe_circle()
turtle.done()
```

### 範例1：安全的計算機

```python
def calculator():
    """安全的計算機"""
    try:
        a = float(input("第一個數："))
        op = input("運算符號（+,-,*,/）：")
        b = float(input("第二個數："))
        
        if op == "+":
            result = a + b
        elif op == "-":
            result = a - b
        elif op == "*":
            result = a * b
        elif op == "/":
            result = a / b
        else:
            raise ValueError("不支援的運算符號")
        
        print(f"結果：{result}")
        
    except ValueError as e:
        print(f"輸入錯誤：{e}")
    except ZeroDivisionError:
        print("錯誤：不能除以零！")
    finally:
        print("計算結束")

calculator()
```

### 範例2：檔案操作安全寫法

```python
def read_file_safely(filename):
    """安全地讀取檔案"""
    try:
        with open(filename, "r", encoding="utf-8") as f:
            return f.read()
    except FileNotFoundError:
        return None
    except PermissionError:
        return None

content = read_file_safely("test.txt")
if content is None:
    print("無法讀取檔案")
else:
    print(content)
```

---

## 10.7 實用範例 - 小遊戲

### 遊戲 1：安全的冒險遊戲

使用例外處理的冒險遊戲！

```python
# 安全的冒險遊戲
# 學習重點：例外處理、try-except-finally

import random
import time

print("=" * 50)
print("        ⚔️ 安全冒險島 ⚔️")
print("=" * 50)
print()

# 玩家資料
player = {"name": "", "hp": 100, "gold": 0, "exp": 0}

def get_input(prompt, data_type=str):
    """安全的輸入函式"""
    while True:
        try:
            value = input(prompt)
            if data_type == int:
                return int(value)
            elif data_type == float:
                return float(value)
            return value
        except ValueError:
            print("❌ 輸入無效，請重新輸入！")

def battle():
    """戰鬥"""
    enemies = [
        {"name": "哥布林", "hp": 30, "damage": 10},
        {"name": "狼", "hp": 40, "damage": 15},
        {"name": "哥布林戰士", "hp": 50, "damage": 20}
    ]
    
    enemy = random.choice(enemies).copy()
    enemy_hp = enemy["hp"]
    
    print(f"\n⚔️ 遭遇 {enemy['name']}！")
    
    while enemy_hp > 0 and player["hp"] > 0:
        try:
            print(f"\n你的 HP: {player['hp']} | 敵人 HP: {enemy_hp}")
            action = get_input("1.攻擊 2.逃跑 3.使用道具：", str)
            
            if action == "1":
                # 攻擊
                damage = random.randint(15, 25)
                enemy_hp -= damage
                print(f"\n你攻擊了 {enemy['name']}，造成 {damage} 傷害！")
                
                if enemy_hp > 0:
                    enemy_damage = random.randint(enemy["damage"]-5, enemy["damage"]+5)
                    player["hp"] -= enemy_damage
                    print(f"{enemy['name']} 反擊，造成 {enemy_damage} 傷害！")
                    
            elif action == "2":
                # 逃跑
                if random.random() > 0.5:
                    print("\n你成功逃跑了！")
                    return True
                else:
                    print("\n逃跑失敗！")
                    player["hp"] -= enemy["damage"]
                    
            elif action == "3":
                # 使用道具
                print("\n你使用了力量藥水！")
                player["hp"] = min(100, player["hp"] + 30)
                player["hp"] -= enemy["damage"]
                
            else:
                print("\n無效的選擇！")
                
        except Exception as e:
            print(f"\n發生錯誤：{e}")
    
    if player["hp"] <= 0:
        print("\n💀 你被打敗了...")
        return False
    
    gold_gained = random.randint(10, 30)
    exp_gained = random.randint(20, 40)
    player["gold"] += gold_gained
    player["exp"] += exp_gained
    
    print(f"\n🎉 打敗了 {enemy['name']}！")
    print(f"獲得 {gold_gained} 金幣和 {exp_gained} 經驗值！")
    return True

def explore():
    """探索"""
    outcomes = ["battle", "treasure", "nothing", "trap"]
    outcome = random.choice(outcomes)
    
    if outcome == "battle":
        return battle()
    elif outcome == "treasure":
        gold = random.randint(20, 50)
        player["gold"] += gold
        print(f"\n💰 你發現了寶箱，獲得 {gold} 金幣！")
        return True
    elif outcome == "trap":
        damage = random.randint(10, 20)
        player["hp"] -= damage
        print(f"\n💥 你踩到了陷阱！受到 {damage} 傷害！")
        return player["hp"] > 0
    else:
        print("\n🌲 這裡什麼都沒有...")
        return True

# 開始遊戲
try:
    player["name"] = get_input("勇者，請輸入你的名字：", str)
    print(f"\n歡迎來到冒險島，{player['name']}！")
    
    day = 1
    while player["hp"] > 0:
        print(f"\n=== 第 {day} 天 ===")
        print(f"HP: {player['hp']} | Gold: {player['gold']} | EXP: {player['exp']}")
        
        action = get_input("1.探索 2.商店 3.休息 0.離開：", str)
        
        if action == "1":
            result = explore()
            if not result:
                break
        elif action == "2":
            print("\n🏪 商店來了再來！")
        elif action == "3":
            player["hp"] = min(100, player["hp"] + 30)
            print("\n😴 你休息了一下，恢復了 30 HP！")
        elif action == "0":
            print("\n感謝遊玩！")
            break
        else:
            print("\n無效的選擇！")
        
        day += 1
        time.sleep(0.5)
        
except KeyboardInterrupt:
    print("\n\n遊戲中斷！")
except Exception as e:
    print(f"\n發生未預期的錯誤：{e}")
finally:
    print("\n" + "=" * 50)
    print("        📜 遊戲結束 📜")
    print("=" * 50)
    print(f"存活天數：{day - 1}")
    print(f"總金幣：{player['gold']}")
    print(f"總經驗：{player['exp']}")
```

---

### 遊戲 2：安全計算機遊戲

結合例外處理的數學問答遊戲！

```python
# 安全計算機遊戲
# 學習重點：例外處理、raise、自訂例外

class GameError(Exception):
    """遊戲錯誤"""
    pass

class InvalidInputError(GameError):
    """輸入錯誤"""
    pass

import random

def safe_input(prompt, expected_type=int):
    """安全輸入"""
    while True:
        try:
            value = input(prompt)
            if expected_type == int:
                return int(value)
            return float(value)
        except ValueError:
            print("❌ 輸入無效，請輸入數字！")

def generate_question():
    """產生數學問題"""
    ops = ["+", "-", "*", "/"]
    op = random.choice(ops)
    
    if op == "+":
        a = random.randint(1, 50)
        b = random.randint(1, 50)
        answer = a + b
    elif op == "-":
        a = random.randint(50, 100)
        b = random.randint(1, a)
        answer = a - b
    elif op == "*":
        a = random.randint(2, 12)
        b = random.randint(2, 12)
        answer = a * b
    else:
        a = random.randint(2, 12) * random.randint(2, 12)
        b = random.randint(2, 12)
        answer = a // b
    
    question = f"{a} {op} {b} = ?"
    return question, answer

def play_round(round_num):
    """玩一題"""
    question, answer = generate_question()
    
    print(f"\n第 {round_num} 題：{question}")
    
    try:
        player_answer = safe_input("你的答案：")
        
        if player_answer == answer:
            print("✅ 正確！+10 分")
            return 10
        else:
            print(f"❌ 錯誤！正確答案是 {answer}")
            return 0
            
    except Exception as e:
        print(f"❌ 發生錯誤：{e}")
        return 0

# 主程式
print("=" * 50)
print("        🧮 數學計算大賽 🧮")
print("=" * 50)
print()

name = input("玩家名稱：")
print(f"\n歡迎 {name}！回答數學問題來獲得分數！")
print("答對 +10 分，答錯 0 分")
print()

try:
    score = 0
    rounds = 5
    
    for i in range(1, rounds + 1):
        points = play_round(i)
        score += points
        print(f"目前得分：{score}")
        
    print()
    print("=" * 50)
    print(f"        遊戲結束！")
    print("=" * 50)
    print(f"\n{name}，你的總得分：{score} / {rounds * 10}")
    
    if score >= 40:
        print("🎉 太厲害了！你是數學高手！")
    elif score >= 20:
        print("👍 不錯喔！繼續努力！")
    else:
        print("📚 再加油！")

except KeyboardInterrupt:
    print("\n\n遊戲中斷！")
finally:
    print("\n感謝遊玩！")
```

---

## 10.8 本章小結

| 語法 | 說明 |
|------|------|
| `try-except` | 捕捉例外 |
| `except TypeError:` | 捕捉特定例外 |
| `except as e:` | 取得例外訊息 |
| `else` | 沒發生錯誤時執行 |
| `finally` | 無論如何都執行 |
| `raise` | 主動拋出例外 |

---

## 練習題

### 基礎題

1. **除法函式**：撰寫函式，處理除法的例外情況。
2. **轉換函式**：將輸入轉換為整數，處理可能的錯誤。
3. **列表操作**：練習處理 IndexError。
4. **字典操作**：練習處理 KeyError。
5. **檔案讀取**：練習處理 FileNotFoundError。
6. **數學運算**：處理 ValueError 和 ZeroDivisionError。
7. **型態檢查**：嘗試將字串轉換為浮點數並處理錯誤。
8. **除錯輸出**：在例外處理中輸出錯誤訊息。
9. **多層例外**：練習捕捉多種不同類型的例外。
10. **finally 使用**：確保程式結束時執行清理工作。

### 進階題

1. **計算機**：參考範例 1，實作完整的計算機。
2. **登入驗證**：使用例外處理驗證帳號密碼。
3. **自訂例外**：建立一個 BankError 例外類別。
4. **重試機制**：實作一個可以重試失敗操作的函式。
5. **驗證系統**：建立一個包含多種驗證的表單處理系統。
6. **鏈結例外**：在例外中拋出新的例外。
7. **全域例外處理**：設定全域的例外處理器。
8. **複合計算機**：支援更多運算並處理各種錯誤。

### 挑戰題

1. **重試計數器**：實作有次數限制的重試機制。
2. **交易系統**：實作銀行轉帳並處理各種錯誤情況。
3. **日誌記錄**：在例外發生時記錄錯誤到檔案。

---

## 進一步閱讀

### 常見內建例外

| 例外 | 說明 |
|------|------|
| `SyntaxError` | 語法錯誤 |
| `IndentationError` | 縮排錯誤 |
| `NameError` | 未定義的變數 |
| `TypeError` | 型態錯誤 |
| `ValueError` | 值錯誤 |
| `IndexError` | 索引超出範圍 |
| `KeyError` | 字典鍵不存在 |
| `FileNotFoundError` | 檔案不存在 |
| `ZeroDivisionError` | 除以零 |
| `AttributeError` | 屬性不存在 |

### 自訂例外類別

```python
class ValidationError(Exception):
    def __init__(self, field, message):
        self.field = field
        self.message = message
        super().__init__(f"{field}: {message}")

# 使用自訂例外
def validate_age(age):
    if age < 0:
        raise ValidationError("age", "年齡不能為負數")
    if age > 150:
        raise ValidationError("age", "年齡不合理")
    return True

try:
    validate_age(-5)
except ValidationError as e:
    print(f"欄位: {e.field}, 錯誤: {e.message}")
```

### logging 模組

```python
import logging

# 設定日誌
logging.basicConfig(
    level=logging.DEBUG,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'
)

logger = logging.getLogger(__name__)

try:
    result = 10 / 0
except ZeroDivisionError:
    logger.error("發生除以零錯誤", exc_info=True)
```

### assert 斷言

```python
# 開發時檢查條件
def divide(a, b):
    assert b != 0, "除數不能為零"
    return a / b

# 關閉斷言（正式環境）
python -O script.py  # 會忽略 assert
```

### Python 官方文件

- [例外處理](https://docs.python.org/3/tutorial/errors.html) - 官方例外教學
- [內建例外](https://docs.python.org/3/library/exceptions.html#bltin-exceptions) - 所有內建例外
- [logging](https://docs.python.org/3/library/logging.html) - 日誌模組

---

*下一章節，我們將學習第 12 章物件導向程式設計，這是 Python 程式設計的重要概念。*
