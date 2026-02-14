# 第 1 章｜緒論

## 學習目標

- 理解什麼是程式設計
- 了解 Python 語言的特點
- 掌握安裝 Python 開發環境的方法
- 撰寫並執行第一個 Python 程式

---

## 1.1 什麼是程式設計？

### 程式設計的定義

**程式設計（Programming）** 是人類與電腦溝通的過程，透過撰寫特定的指令，讓電腦幫我們完成各種任務。

想像一下：你是一家餐廳的老闆，需要訓練新員工做事。你會給員工作業指示，例如「客人入座後，先遞上菜單」。這些指示就像「程式」，而員工就像「電腦」，按照你的指示行動。

### 程式語言的重要性

電腦只能聽懂 0 和 1 的二元訊息，對人類來說太過艱澀。**程式語言**作為人類與電腦之間的橋樑，讓我們可以用較直觀的方式表達指令。

常見的程式語言包括：
- **Python** - 簡潔易學，用途廣泛
- **Java** - 企業級應用開發
- **C/C++** - 系統程式、遊戲開發
- **JavaScript** - 網頁開發

---

## 1.2 為什麼選擇 Python？

> **📝 Note（說明）**：Python 可以在 Windows、UNIX 和 Mac 作業系統上執行。安裝方式請參考官方網站。

Python 是一款於 1991 年由 Guido van Rossum 創造的程式語言，如今已成為全球最受歡迎的語言之一。

### Python 的優點

| 優點 | 說明 |
|------|------|
| **語法簡潔** | 程式碼像英文句子，易於閱讀和理解 |
| **用途廣泛** | 網頁開發、資料分析、人工智慧、自動化腳本都能做 |
| **社群龐大** | 有豐富的學習資源和套件支持 |
| **跨平台** | Windows、Mac、Linux 都能執行 |

### Python 的應用領域

```
┌─────────────────────────────────────────────────────────┐
│                      Python 應用                         │
├──────────────┬──────────────┬──────────────┬───────────┤
│   網頁開發    │   資料分析    │   人工智慧    │  自動化    │
│   Django     │   Pandas     │   TensorFlow │  腳本      │
│   Flask      │   NumPy      │   PyTorch    │  網路爬蟲  │
└──────────────┴──────────────┴──────────────┴───────────┘
```

---

## 1.3 安裝 Python 開發環境

### Windows 安裝步驟

1. 瀏覽 Python 官方網站：https://www.python.org
2. 點擊「Downloads」>「Download Python」
3. 執行下載的安裝檔
4. **重要**：勾選「Add Python to PATH」
5. 點擊「Install Now」

### macOS 安裝步驟

macOS 通常已預安裝 Python，但版本可能較舊。建議使用 Homebrew 安裝最新版本：

```bash
# 安裝 Homebrew（如果還沒安裝）
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# 使用 Homebrew 安裝 Python
brew install python
```

### Linux 安裝步驟

大多數 Linux 發行版已預安裝 Python。可在終端機輸入以下指令確認：

```bash
python3 --version
```

若需要安裝或更新：

```bash
# Ubuntu/Debian
sudo apt update
sudo apt install python3

# Fedora
sudo dnf install python3
```

### 驗證安裝

開啟終端機（Windows 使用 PowerShell 或 CMD），輸入：

```bash
python3 --version
```

如果顯示類似 `Python 3.11.4` 的版本號，表示安裝成功！

---

## 1.3.1 WinPython - 免安裝便攜版

如果你不想安裝 Python 到系統中，或者在學校/公用電腦上無法安裝軟體，**WinPython** 是一個很好的選擇。

### 什麼是 WinPython？

WinPython 是一個**免安裝**的 Python 發行版，專為 Windows 設計。它包含：
- Python 直譯器
- Jupyter Notebook（網頁版開發環境）
- Spyder（科學計算 IDE）
- 常用科學計算套件（NumPy、Pandas 等）

### 下載與使用

1. 前往官網：https://winpython.github.io
2. 下載 ZIP 檔案（選擇「Winpython64」版本）
3. 解壓縮到任意資料夾
4. 執行 `jupyter-notebook.exe` 即可開始寫 Python！

### WinPython 的優點

| 優點 | 說明 |
|------|------|
| **免安裝** | 解壓縮就能用，無需管理員權限 |
| **便攜性** | 可放在 USB 隨身碟，到處使用 |
| **多版本** | 可同時安裝多個 Python 版本 |
| **含預設套件** | 內建常用科學計算套件 |

---

## 1.3.2 線上 Python 開發環境

如果你只想快速體驗 Python，或者沒有電腦可以安裝軟體，以下是完全免費的線上開發環境：

### 推薦的線上 Python 環境

| 平台 | 網址 | 特色 |
|------|------|------|
| **Google Colab** | https://colab.research.google.com | 免費 GPU支援，適合 AI/資料分析 |
| **Replit** | https://replit.com | 即時協作，適合教學 |
| **Programiz** | https://www.programiz.com/python-programming/online-compiler | 簡單易用，無需註冊 |
| **OnlineGDB** | https://www.onlinegdb.com/python-compiler | 支援除錯功能 |

### Google Colab 快速上手

1. 前往 https://colab.research.google.com
2. 使用 Google 帳號登入
3. 點擊「新增筆記本」
4. 在格子中輸入 Python 程式碼
5. 按 `Shift + Enter` 執行

```python
# 在 Colab 中測試
print("Hello, Python!")
for i in range(5):
    print(i)
```

### 適合的使用情境

| 情境 | 推薦環境 |
|------|----------|
| 資料分析/機器學習 | Google Colab |
| 學校教學/作業缴交 | Replit |
| 快速測試簡單程式 | Programiz |
| 需要除錯練習 | OnlineGDB |

---

## 1.4 安裝程式碼編輯器

撰寫 Python 程式需要一個好的**整合開發環境（IDE）**或文字編輯器。

### 推薦的工具

| 工具 | 類型 | 適用對象 |
|------|------|----------|
| **VS Code** | 免費/跨平台 | 所有人（推薦） |
| **PyCharm** | 免費/專業版 | 專業開發者 |
| **Thonny** | 免費/簡單 | 完全初學者 |
| **Jupyter Notebook** | 網頁式 | 資料分析 |

### VS Code 安裝（推薦）

1. 下載 VS Code：https://code.visualstudio.com
2. 安裝並啟動
3. 安裝 Python 擴充套件：
   - 開啟 VS Code
   - 按下 `Ctrl + P`（Mac 為 `Cmd + P`）
   - 輸入 `ext install ms-python.python`
   - 點擊安裝

---

## 1.5 第一個 Python 程式

### 使用互動式解釋器

開啟終端機，輸入 `python3`（或 `python`），會進入 Python 的**互動式解釋器**：

```python
>>> print("Hello, World!")
Hello, World!
```

`print()` 是 Python 用來輸出文字的函式，雙引號包住的內容會原樣顯示。

> **📝 Note（說明）**：Python 需要使用雙引號或單引號來標示字串，以區分程式碼。Python 不會在輸出中顯示這些引號。

> **📝 Note（說明）**：在程式設計術語中，當你「使用」一個函式時，稱為「呼叫」或「invoke」函式。

> **💡 Tip（小技巧）**：如果你不知道如何修正語法錯誤，請仔細對照課本中的範例，逐字元比較。在學習的前幾週，你可能會花很多時間在修正語法錯誤上，但很快你就會熟悉 Python 語法，能夠快速修正錯誤！

### 建立第一個程式檔案

1. 打開 VS Code
2. 新建檔案：`Ctrl + N`
3. 輸入以下程式碼：

```python
# 我的第一個 Python 程式
# 這是一個簡單的問候程式

name = "小明"          # 變數：儲存名字
age = 18               # 變數：儲存年齡

print("你好！")         # 輸出問候語
print("我叫" + name)   # 輸出名字
print("我今年", age, "歲")  # 輸出年齡
```

4. 儲存檔案為 `hello.py`（`.py` 是 Python 檔案的副檔名）
5. 執行程式：
   - 在 VS Code 中按 `F5` 或
   - 在終端機輸入 `python3 hello.py`

### 執行結果

```
你好！
我叫小明
我今年 18 歲
```

---

## 1.6 Turtle 繪圖初體驗

Python 內建了一個非常好玩的繪圖模組叫做 **turtle**（海龜繪圖）。你可以把它想成有一隻小烏龜拿著一支筆，你叫它往哪走，它就會畫出什麼圖案。這是一個學習程式設計的絕佳方式，讓我們能夠「看到」程式的執行結果！

### 認識 Turtle 基本指令

```python
import turtle

# 讓烏龜前進（畫線）
turtle.forward(100)   # 前進 100 像素

# 讓烏龜轉彎
turtle.right(90)      # 右轉 90 度
turtle.left(45)       # 左轉 45 度

# 畫圓形
turtle.circle(50)     # 畫一個半徑 50 的圓

# 改變顏色
turtle.color("red")    # 紅色
turtle.color("blue")   # 藍色
turtle.color("green") # 綠色

# 提起/放下畫筆
turtle.penup()        # 提起筆（移動不畫線）
turtle.pendown()      # 放下筆（移動會畫線）

# 讓視窗保持開啟
turtle.done()
```

### 畫出第一個圖案：正方形

```python
import turtle

turtle.forward(100)    # 前進
turtle.right(90)      # 右轉
turtle.forward(100)   # 前進
turtle.right(90)       # 右轉
turtle.forward(100)   # 前進
turtle.right(90)      # 右轉
turtle.forward(100)   # 前進

turtle.done()
```

### 練習：畫出不同的圖案

```python
import turtle

# 畫三角形
turtle.forward(100)
turtle.right(120)
turtle.forward(100)
turtle.right(120)
turtle.forward(100)

# 畫五邊形
turtle.penup()
turtle.goto(100, 0)
turtle.pendown()

for i in range(5):
    turtle.forward(80)
    turtle.right(72)

turtle.done()
```

### Turtle 座標系統

Turtle 繪圖視窗的中心是 (0, 0)，就像數學課本的座標系統一樣：
- X 軸：向右是正方向
- Y 軸：向上是正方向

```python
import turtle

# 移動到指定座標
turtle.goto(100, 100)   # 移動到 (100, 100)
turtle.goto(-50, -50)   # 移動到 (-50, -50)

# 回到原點
turtle.goto(0, 0)

turtle.done()
```

### 小挑戰

試著畫出以下圖案：
1. 一個長方形
2. 一個六邊形
3. 一個星星

---

## 1.7 實用範例 - 小遊戲

### 遊戲 1：幸運數字猜測遊戲

這是一個簡單的文字猜測遊戲，電腦會產生一個幸運數字，你需要猜測它！

```python
# 幸運數字猜測遊戲
# 學習重點：print() 的輸出練習

import random

print("=" * 40)
print("       🎯 幸運數字猜測遊戲 🎯")
print("=" * 40)
print()
print("規則：電腦會產生 1-10 的幸運數字")
print("      你有 3 次機會猜測！")
print()

# 電腦產生幸運數字
lucky_number = random.randint(1, 10)

# 顯示幸運數字（測試用，正式遊戲可刪除這行）
# print(f"[測試用] 幸運數字是：{lucky_number}")

# 第一次猜測
print("-" * 40)
guess1 = int(input("請輸入你的第 1 次猜測 (1-10)："))
if guess1 == lucky_number:
    print("🎉 恭喜你！第一次就猜對了！")
else:
    if guess1 < lucky_number:
        print("提示：幸運數字比你猜的還要大！")
    else:
        print("提示：幸運數字比你猜的還要小！")
    
    # 第二次猜測
    print("-" * 40)
    guess2 = int(input("請輸入你的第 2 次猜測 (1-10)："))
    if guess2 == lucky_number:
        print("🎉 太棒了！第二次猜對了！")
    else:
        if guess2 < lucky_number:
            print("提示：幸運數字比你猜的還要大！")
        else:
            print("提示：幸運數字比你猜的還要小！")
        
        # 第三次猜測
        print("-" * 40)
        guess3 = int(input("請輸入你的第 3 次猜測 (1-10)："))
        if guess3 == lucky_number:
            print("🎊 第三次終於猜對了！好厲害！")
        else:
            print("-" * 40)
            print(f"😢 抱歉，機會用完了！")
            print(f"幸運數字是：{lucky_number}")
            print("再接再厲，下次一定會猜對！")

print("-" * 40)
print("感謝遊玩！歡迎下次再來！")
```

執行的範例輸出：
```
========================================
       🎯 幸運數字猜測遊戲 🎯
========================================

規則：電腦會產生 1-10 的幸運數字
      你有 3 次機會猜測！

----------------------------------------
請輸入你的第 1 次猜測 (1-10)：5
提示：幸運數字比你猜的還要大！
----------------------------------------
請輸入你的第 2 次猜測 (1-10)：8
🎉 太棒了！第二次猜對了！
----------------------------------------
感謝遊玩！歡迎下次再來！
```

---

### 遊戲 2：文字冒險遊戲

這是一個簡單的文字冒險遊戲，你將扮演一位勇者，需要消滅怪物並拯救王國！

```python
# 文字冒險遊戲 - 勇者傳奇
# 學習重點：print() 的輸出練習與多行文字

print("=" * 50)
print("           🐉 勇者傳奇 🐉")
print("=" * 50)
print()
print("歡迎來到艾澤拉王國！")
print("你是一位勇敢的勇者，肩負著拯救王國的使命。")
print()
print("在前方的洞穴中，住著一隻邪惡的巨龍。")
print("你需要收集寶物，裝備自己，然後打敗巨龍！")
print()
print("=" * 50)
print()

# 遊戲開始
print("【第一關：森林】")
print("-" * 50)
print("你走進了陰暗的森林...")
print("突然，一隻哥布林衝了出來！")
print()
print("選項：")
print("  1. 使用寶劍攻擊")
print("  2. 使用魔法攻擊")
print("  3. 嘗試逃跑")
print()

choice1 = input("請選擇你的行動 (1/2/3)：")

if choice1 == "1":
    print()
    print("⚔️ 你舉起寶劍，大喊一聲衝向哥布林！")
    print("鏘！鏘！鏘！")
    print("哥布林應聲倒地！")
    print()
    print("🎉 你戰勝了哥布林！獲得了 100 點經驗值！")
    print("你獲得了【寶石】x3")
    
elif choice1 == "2":
    print()
    print("✨ 你聚集魔力，準備施放火焰術！")
    print("轟！")
    print("火焰包圍了哥布林，哥布林慘叫一聲後逃走了！")
    print()
    print("🎉 你嚇跑了哥布林！獲得了 50 點經驗值！")
    print("你獲得了【魔法書】x1")
    
else:
    print()
    print("🏃 你轉身就跑！")
    print("但哥布林跑得比你更快...")
    print("你被抓住了！")
    print()
    print("😢 遊戲結束！下次要勇敢一點！")
    print()
    print("=" * 50)
    print("感謝遊玩！")
    print("=" * 50)
    exit()

print()
print("-" * 50)
print("【第二關：洞穴入口】")
print("-" * 50)
print("你來到了巨龍的洞穴入口...")
print("洞口有一道古老的石門，上面刻著謎語：")
print()
print("「什麼東西，早上四條腿，中午兩條腿，")
print("   晚上三條腿？」")
print()
answer = input("請輸入答案：")

if answer == "人" or answer == "人類":
    print()
    print("✅ 石門緩緩打開了！")
    print("你成功進入了洞穴！")
    print()
    print("🎉 恭喜你通過了所有關卡！")
    print()
    print("=" * 50)
    print("        🏆 遊戲通關！ 🏆")
    print("=" * 50)
    print("感謝你拯救了艾澤拉王國！")
    print("你是一位真正的勇者！")
else:
    print()
    print("❌ 石門一點反應都沒有...")
    print("看來答案不正確。")
    print()
    print("不過，你仍然決定闖入洞穴...")
    print("讓我們期待下一次的冒險！")
    print()
    print("=" * 50)
    print("        📜 待續... 📜")
    print("=" * 50)

print()
print("感謝遊玩《勇者傳奇》！")
print("下次再見！")
```

---

## 1.7 本章小結

| 概念 | 重點 |
|------|------|
| 程式設計 | 人類透過程式語言指示電腦完成任務 |
| Python 優點 | 語法簡潔、用途廣泛、社群龐大 |
| 安裝 Python | 從 python.org 下載並安裝 |
| 第一個程式 | 使用 `print()` 函式輸出文字 |

---

## 練習題

### 基礎題

1. **環境確認**：確認你的電腦已正確安裝 Python，並顯示版本號。
2. **Hello World**：撰寫一個程式，輸出「Hello, Python!」。
3. **自我介紹**：撰寫一個程式，輸出你的姓名和系級。
4. **輸出數字**：使用 `print()` 輸出數字 12345。
5. **輸出符號**：使用 `print()` 輸出你的幸運數字。
6. **數學計算**：撰寫程式輸出 7 + 8 的結果。
7. **除法練習**：撰寫程式輸出 15 除以 3 的結果。
8. **多重輸出**：使用三個 `print()` 語句輸出三句問候語。
9. **輸出自己的資訊**：輸出你的年齡和體重（假設值）。
10. **輸出現在時間**：使用 `print()` 輸出現在應該做什麼（例如：吃飯、睡覺、學習）。

### 進階題

1. **多行輸出**：使用 `print()` 函式輸出三行詩歌或名言。
2. **計算輸出**：使用 `print()` 輸出 `5 + 3` 的運算結果（不要直接寫 8）。
3. **個人資訊卡**：撰寫一個程式，以美觀的格式輸出你的個人資訊卡片，包含：姓名、年級、興趣、最喜歡的科目。
4. **ASCII 藝術**：用文字符號畫出一個簡單的圖案（如愛心、星星或動物）。
5. **格式化輸出**：使用一個 `print()` 語句輸出「我是 XXX，今年 Y 歲，就讀 Z 學校」。
6. **計算機輸出**：輸出「3 + 5 = 8」格式的算式，計算部分使用程式計算。
7. **引號輸出**：使用 `print()` 輸出包含雙引號的文字，例如：他说「你好」。
8. **轉義字元**：輸出包含換行和 Tab 的文字，展示它們的效果。

### 挑戰題

1. **互動式問候**：使用 `input()` 輸入姓名，然後輸出問候語。
2. **計算年齡**：輸入今年的年份和出生年份，計算並輸出年齡。
3. **個人名片**：設計一個精美的個人名片程式，包含姓名、系級、社團、專長等資訊。

---

## 進一步閱讀

### 常用內建函式

Python 提供了豐富的內建函式，以下是本章介紹的函式詳細說明：

| 函式 | 說明 | 範例 |
|------|------|------|
| `print()` | 輸出物件到標準輸出 | `print("Hello")` |
| `input()` | 從使用者取得輸入字串 | `name = input("請輸入姓名：")` |
| `type()` | 回傳物件的型態 | `type(123)` → `<class 'int'>` |
| `help()` | 顯示說明文件 | `help(print)` |

### 更多內建函式

Python 還有許多實用的內建函式值得探索：

```python
# 轉換函式
int("123")      # 轉為整數
float("3.14")   # 轉為浮點數
str(123)        # 轉為字串
bool(1)         # 轉為布林值

# 數學相關
abs(-5)         # 絕對值 → 5
round(3.7)      # 四捨五入 → 4
pow(2, 3)       # 次方 → 8
max(1, 5, 3)    # 最大值 → 5
min(1, 5, 3)    # 最小值 → 1
sum([1, 2, 3])  # 總和 → 6
```

### Python 官方文件

- [Python 內建函式](https://docs.python.org/3/library/functions.html) - 完整的內建函式清單
- [Python 教學](https://docs.python.org/3/tutorial/index.html) - 官方入門教學
- [turtle 模組](https://docs.python.org/3/library/turtle.html) - 海龜繪圖完整說明
- [Python 速查表](https://docs.python.org/3/) - 官方文件首頁

### 延伸學習

- [Google Colab](https://colab.research.google.com/) - 免費線上 Python 開發環境
- [Real Python](https://realpython.com/) - 高品質 Python 教學網站
- [Python.org 下載](https://www.python.org/downloads/) - 取得最新 Python 版本

---

*下一章節，我們將深入了解變數與各種資料型態。*
