# 第 10 章｜Tkinter GUI 程式設計

## 學習目標

- 理解 GUI（圖形使用者介面）的概念
- 掌握 Tkinter 的基本使用方法
- 學會建立各種常用元件（標籤、按鈕、文字方塊等）
- 理解事件處理的原理
- 能夠設計簡單的 GUI 應用程式

---

## 10.1 什麼是 GUI？

> **📝 Note（說明）**：**GUI（Graphical User Interface，圖形使用者介面）** 讓使用者可以透過圖形化元素（如按鈕、選單、文字方塊）與程式互動，而不需要輸入指令。GUI 程式設計是現代軟體開發的基礎技能。

**GUI（Graphical User Interface，圖形使用者介面）** 讓使用者可以透過圖形化元素（如按鈕、選單、文字方塊）與程式互動，而不需要輸入指令。

### 常見的 GUI 元件

| 元件 | 說明 | 範例 |
|------|------|------|
| 視窗（Window） | 程式的主要畫面 | 應用程式的視窗 |
| 標籤（Label） | 顯示文字或圖片 | 標題、說明文字 |
| 按鈕（Button） | 點擊後執行動作 | 確認、取消按鈕 |
| 文字方塊（Entry） | 讓使用者輸入文字 | 登入帳號密碼 |
| 文字區域（Text） | 多行文字輸入 | 留言板、記事本 |
| 下拉選單（OptionMenu） | 選擇單一選項 | 國家、性別選擇 |
| 核取方塊（Checkbutton） | 勾選或多選 | 同意條款 |
| 選項按鈕（Radiobutton） | 單一選擇 | 性別選擇 |
| 列表方塊（Listbox） | 顯示選項清單 | 聯絡人清單 |

### Tkinter 簡介

> **💡 Tip（小技巧）**：Tkinter 是 Python 內建的 GUI 模組，不需要額外安裝就可以使用。它基於 Tk 工具包，簡單易學，非常適合初學者練習 GUI 程式設計。

**Tkinter** 是 Python 內建的 GUI 模組，不需要額外安裝就可以使用。它簡單易學，非常適合初學者練習 GUI 程式設計。

---

## 10.2 第一個 Tkinter 程式

> **⚠️ Caution（注意）**：`window.mainloop()` 是 Tkinter 程式的關鍵！沒有這行程式碼，視窗會閃一下就關閉。`mainloop()` 會持續執行直到使用者關閉視窗。

### 建立視窗

```python
import tkinter as tk

# 建立主視窗
window = tk.Tk()

# 設定視窗標題
window.title("我的第一個 GUI 程式")

# 設定視窗大小（寬 x 高）
window.geometry("400x300")

# 執行視窗程式
window.mainloop()
```

### 加入標籤

```python
import tkinter as tk

window = tk.Tk()
window.title("加入標籤")
window.geometry("300x200")

# 建立標籤
label = tk.Label(window, text="你好，歡迎使用 GUI！")
label.pack()  # 放置元件

window.mainloop()
```

### 加入按鈕

```python
import tkinter as tk

def button_clicked():
    label.config(text="按鈕被點擊了！")

window = tk.Tk()
window.title("按鈕範例")
window.geometry("300x200")

# 建立標籤
label = tk.Label(window, text="按下方的按鈕")
label.pack(pady=10)

# 建立按鈕
button = tk.Button(window, text="點擊我", command=button.pack(padybutton_clicked)
=10)

window.mainloop()
```

---

## 10.3 常用元件

> **💡 Tip（小技巧）**：使用 `entry.get()` 可以取得文字方塊中的內容，而 `entry.delete(0, tk.END)` 可以清除文字方塊的內容。

### 文字方塊（Entry）

```python
import tkinter as tk

def show_input():
    text = entry.get()
    label.config(text=f"你輸入的是：{text}")

window = tk.Tk()
window.title("文字方塊範例")
window.geometry("300x150")

# 建立標籤
label = tk.Label(window, text="請輸入文字：")
label.pack(pady=5)

# 建立文字方塊
entry = tk.Entry(window, width=30)
entry.pack(pady=5)

# 建立按鈕
button = tk.Button(window, text="顯示輸入", command=show_input)
button.pack(pady=5)

window.mainloop()
```

### 文字區域（Text）

```python
import tkinter as tk

window = tk.Tk()
window.title("文字區域範例")
window.geometry("300x250")

# 建立文字區域
text = tk.Text(window, height=10, width=35)
text.pack(pady=10)

# 放入一些文字
text.insert("1.0", "這是一個文字區域\n可以輸入多行文字\n")

window.mainloop()
```

### 下拉選單（OptionMenu）

```python
import tkinter as tk

def show_choice():
    label.config(text=f"你選擇的是：{choice.get()}")

window = tk.Tk()
window.title("下拉選單範例")
window.geometry("300x150")

# 建立變數
choice = tk.StringVar()
choice.set("請選擇")

# 建立下拉選單
option = tk.OptionMenu(window, choice, "蘋果", "香蕉", "橘子", "西瓜")
option.pack(pady=10)

# 建立按鈕
button = tk.Button(window, text="確認", command=show_choice)
button.pack(pady=10)

# 建立標籤顯示結果
label = tk.Label(window, text="")
label.pack(pady=5)

window.mainloop()
```

### 核取方塊（Checkbutton）

```python
import tkinter as tk

def show_check():
    result = []
    if var1.get():
        result.append("選項一")
    if var2.get():
        result.append("選項二")
    if var3.get():
        result.append("選項三")
    label.config(text=f"你選擇：{result}")

window = tk.Tk()
window.title("核取方塊範例")
window.geometry("300x200")

var1 = tk.BooleanVar()
var2 = tk.BooleanVar()
var3 = tk.BooleanVar()

# 建立核取方塊
c1 = tk.Checkbutton(window, text="選項一", variable=var1)
c2 = tk.Checkbutton(window, text="選項二", variable=var2)
c3 = tk.Checkbutton(window, text="選項三", variable=var3)

c1.pack()
c2.pack()
c3.pack()

# 建立按鈕
button = tk.Button(window, text="確認", command=show_check)
button.pack(pady=10)

label = tk.Label(window, text="")
label.pack()

window.mainloop()
```

### 選項按鈕（Radiobutton）

```python
import tkinter as tk

def show_choice():
    label.config(text=f"你選擇的是：{choice.get()}")

window = tk.Tk()
window.title("選項按鈕範例")
window.geometry("300x200")

choice = tk.StringVar()
choice.set("")

# 建立選項按鈕
r1 = tk.Radiobutton(window, text="選項 A", variable=choice, value="A")
r2 = tk.Radiobutton(window, text="選項 B", variable=choice, value="B")
r3 = tk.Radiobutton(window, text="選項 C", variable=choice, value="C")

r1.pack()
r2.pack()
r3.pack()

button = tk.Button(window, text="確認", command=show_choice)
button.pack(pady=10)

label = tk.Label(window, text="")
label.pack()

window.mainloop()
```

---

## 10.4 版面配置管理

> **💡 Tip（小技巧）**：建議在一個視窗中只使用一種版面配置管理器（pack、grid 或 place），混合使用可能會造成不可預期的結果。新手推薦使用 grid，因為它最容易理解和掌握。

Tkinter 提供三種版面配置管理器來安排元件的位置：

### pack 配置器

按照順序自動排列元件。

```python
import tkinter as tk

window = tk.Tk()
window.geometry("200x200")

label1 = tk.Label(window, text="標籤 1", bg="red", fg="white")
label2 = tk.Label(window, text="標籤 2", bg="green", fg="white")
label3 = tk.Label(window, text="標籤 3", bg="blue", fg="white")

label1.pack(fill="x")
label2.pack(fill="x")
label3.pack(fill="x")

window.mainloop()
```

### grid 配置器

使用表格方式排列元件。

```python
import tkinter as tk

window = tk.Tk()
window.title("Grid 範例")

# 建立標籤和文字方塊
tk.Label(window, text="帳號：").grid(row=0, column=0, padx=5, pady=5)
tk.Entry(window).grid(row=0, column=1, padx=5, pady=5)

tk.Label(window, text="密碼：").grid(row=1, column=0, padx=5, pady=5)
tk.Entry(window, show="*").grid(row=1, column=1, padx=5, pady=5)

tk.Button(window, text="登入").grid(row=2, column=0, columnspan=2, pady=10)

window.mainloop()
```

### place 配置器

使用座標精確定位元件。

```python
import tkinter as tk

window = tk.Tk()
window.geometry("300x200")

# 使用座標放置元件
label = tk.Label(window, text="固定位置", bg="yellow")
label.place(x=100, y=50)

button = tk.Button(window, text="按鈕")
button.place(x=120, y=100)

window.mainloop()
```

---

## 10.5 事件處理

> **📝 Note（說明）**：事件處理是 GUI 程式的核心概念。當使用者點擊按鈕、輸入文字或移動滑鼠時，都會觸發一個「事件」。我們可以透過綁定（bind）函式來處理這些事件。

### 滑鼠事件

```python
import tkinter as tk

def on_click(event):
    label.config(text=f"滑鼠點擊位置：({event.x}, {event.y})")

window = tk.Tk()
window.title("滑鼠事件")
window.geometry("300x200")

label = tk.Label(window, text="點擊視窗看看", font=("Arial", 16))
label.pack(pady=20)

# 綁定滑鼠點擊事件
window.bind("<Button-1>", on_click)

window.mainloop()
```

### 鍵盤事件

```python
import tkinter as tk

def on_key(event):
    label.config(text=f"你按下了：{event.char}")

window = tk.Tk()
window.title("鍵盤事件")
window.geometry("300x200")

label = tk.Label(window, text="按下一個鍵看看", font=("Arial", 16))
label.pack(pady=20)

# 綁定鍵盤事件
window.bind("<Key>", on_key)

window.mainloop()
```

---

## 10.6 實用範例

### 範例1：計算機

```python
import tkinter as tk

def click(number):
    current = entry.get()
    entry.delete(0, tk.END)
    entry.insert(tk.END, current + str(number))

def clear():
    entry.delete(0, tk.END)

def calculate():
    try:
        result = eval(entry.get())
        entry.delete(0, tk.END)
        entry.insert(tk.END, str(result))
    except:
        entry.delete(0, tk.END)
        entry.insert(tk.END, "錯誤")

window = tk.Tk()
window.title("計算機")
window.geometry("300x400")

# 顯示螢幕
entry = tk.Entry(window, font=("Arial", 24), justify="right")
entry.pack(fill="x", padx=10, pady=10)

# 按鈕框架
btn_frame = tk.Frame(window)
btn_frame.pack()

# 按鈕列表
buttons = [
    ("7", 1, 0), ("8", 1, 1), ("9", 1, 2), ("/", 1, 3),
    ("4", 2, 0), ("5", 2, 1), ("6", 2, 2), ("*", 2, 3),
    ("1", 3, 0), ("2", 3, 1), ("3", 3, 2), ("-", 3, 3),
    ("0", 4, 0), (".", 4, 1), ("=", 4, 2), ("+", 4, 3),
]

for (text, row, col) in buttons:
    if text == "=":
        btn = tk.Button(btn_frame, text=text, width=5, height=2, command=calculate)
    else:
        btn = tk.Button(btn_frame, text=text, width=5, height=2, command=lambda t=text: click(t))
    btn.grid(row=row, column=col, padx=5, pady=5)

# 清除按鈕
clear_btn = tk.Button(window, text="清除", command=clear, width=30)
clear_btn.pack(pady=10)

window.mainloop()
```

### 範例2：體重BMI計算機

```python
import tkinter as tk

def calculate_bmi():
    try:
        height = float(entry_height.get()) / 100  # 轉換為公尺
        weight = float(entry_weight.get())
        bmi = weight / (height ** 2)
        
        if bmi < 18.5:
            result = f"BMI: {bmi:.1f} - 過輕"
        elif bmi < 24:
            result = f"BMI: {bmi:.1f} - 正常"
        elif bmi < 27:
            result = f"BMI: {bmi:.1f} - 過重"
        else:
            result = f"BMI: {bmi:.1f} - 肥胖"
        
        label_result.config(text=result)
    except:
        label_result.config(text="請輸入有效的數字")

window = tk.Tk()
window.title("BMI 計算機")
window.geometry("300x250")

# 標題
tk.Label(window, text="BMI 體重計算機", font=("Arial", 18, "bold")).pack(pady=10)

# 身高
tk.Label(window, text="身高 (cm)：").pack()
entry_height = tk.Entry(window)
entry_height.pack(pady=5)

# 體重
tk.Label(window, text="體重 (kg)：").pack()
entry_weight = tk.Entry(window)
entry_weight.pack(pady=5)

# 計算按鈕
btn = tk.Button(window, text="計算 BMI", command=calculate_bmi, bg="lightblue")
btn.pack(pady=15)

# 結果
label_result = tk.Label(window, text="", font=("Arial", 14))
label_result.pack(pady=10)

window.mainloop()
```

### 範例3：通訊錄

```python
import tkinter as tk

contacts = {}

def add_contact():
    name = entry_name.get()
    phone = entry_phone.get()
    if name and phone:
        contacts[name] = phone
        listbox.insert(tk.END, f"{name}: {phone}")
        entry_name.delete(0, tk.END)
        entry_phone.delete(0, tk.END)

def delete_contact():
    selection = listbox.curselection()
    if selection:
        item = listbox.get(selection[0])
        name = item.split(":")[0]
        del contacts[name]
        listbox.delete(selection[0])

window = tk.Tk()
window.title("通訊錄")
window.geometry("350x400")

# 輸入區域
frame_input = tk.Frame(window)
frame_input.pack(pady=10)

tk.Label(frame_input, text="姓名：").grid(row=0, column=0)
entry_name = tk.Entry(frame_input, width=15)
entry_name.grid(row=0, column=1, padx=5)

tk.Label(frame_input, text="電話：").grid(row=1, column=0)
entry_phone = tk.Entry(frame_input, width=15)
entry_phone.grid(row=1, column=1, padx=5)

# 按鈕區域
frame_buttons = tk.Frame(window)
frame_buttons.pack(pady=5)

tk.Button(frame_buttons, text="新增", command=add_contact).pack(side=tk.LEFT, padx=5)
tk.Button(frame_buttons, text="刪除", command=delete_contact).pack(side=tk.LEFT, padx=5)

# 列表顯示
listbox = tk.Listbox(window, width=40, height=15)
listbox.pack(pady=10)

window.mainloop()
```

---

## 10.7 本章小結

> **💡 Tip（小技巧）**：學習 GUI 程式設計最重要的是多練習！嘗試修改範例程式碼，改變顏色、大小、功能，這樣才能真正掌握 Tkinter 的用法。

| 元件 | 用途 |
|------|------|
| `tk.Tk()` | 建立主視窗 |
| `tk.Label()` | 顯示文字標籤 |
| `tk.Button()` | 建立按鈕 |
| `tk.Entry()` | 單行文字輸入 |
| `tk.Text()` | 多行文字輸入 |
| `tk.OptionMenu()` | 下拉選單 |
| `tk.Checkbutton()` | 核取方塊 |
| `tk.Radiobutton()` | 選項按鈕 |
| `pack()` | 自動排列 |
| `grid()` | 表格排列 |
| `place()` | 座標定位 |

---

## 練習題

### 基礎題

1. **Hello GUI**：建立一個視窗，顯示「Hello GUI!」
2. **兩個按鈕**：建立兩個按鈕，分別顯示「你好」和「再見」，點擊時顯示問候語
3. **輸入輸出**：建立一個文字方塊和一個按鈕，點擊後顯示輸入的內容
4. **簡易表單**：建立帳號和密碼的輸入表單
5. **標籤更改**：建立一個標籤和兩個按鈕，點擊分別更改標籤文字
6. **數字相加**：建立兩個數字輸入框，按下按鈕後顯示兩數相加的結果
7. **下拉選單**：建立下拉選單，選擇後顯示選項名稱
8. **核取方塊**：建立三個核取方塊，顯示被勾選的項目
9. **單選按鈕**：建立性別選擇的單選按鈕
10. **計算面積**：輸入長和寬，計算長方形面積
11. **切換文字**：建立按鈕，切換標籤文字在「你好」和「再見」之間
12. **數字遞增**：建立按鈕，每次點擊數字加 1 並顯示

### 進階題

1. **密碼驗證**：輸入密碼，顯示******，點擊顯示密碼
2. **顏色選擇**：使用選項按鈕選擇顏色，點擊後改變標籤顏色
3. **記事本**：使用 Text 元件建立簡易記事本，可輸入和顯示文字
4. **九九乘法表**：點擊按鈕顯示九九乘法表
5. **登入表單**：建立帳號密碼表單，輸入正確顯示「登入成功」，錯誤顯示「登入失敗」
6. **BMI 計算機**：輸入身高體重，計算 BMI 並顯示結果（過輕/正常/過重/肥胖）
7. **溫度轉換**：輸入攝氏溫度，轉換為華氏溫度
8. **數字比大小**：輸入兩個數字，比較大小並顯示結果
9. **成績計算**：輸入成績，顯示等第（A/B/C/D/E）
10. **幸運數字**：產生隨機幸運數字，讓使用者猜測
11. **計算機**：建立簡易計算機，可做加减乘除運算
12. **電子時鐘**：即時顯示目前時間

### 挑戰題

1. **貨幣轉換器**：設計匯率轉換工具（台幣、美元、日幣、歐元）
2. **倒數計時器**：設計倒數計時應用，可設定秒數倒數
3. **小畫家**：使用 Canvas 畫布製作簡單繪圖工具
4. **待辦事項**：建立待辦事項清單，可新增、刪除事項
5. **鬧鐘設定**：設定時間，到點發出提醒
6. **密碼管理員**：儲存和查詢網站密碼
7. **通訊錄管理**：新增、修改、刪除、搜尋聯絡人
8. **記帳程式**：記錄收入支出，顯示餘額

---

## 進一步閱讀

### Tkinter 更多元件

```python
import tkinter as tk
from tkinter import ttk

# 選單 (Menu)
menubar = tk.Menu(root)
file_menu = tk.Menu(menubar, tearoff=0)
file_menu.add_command(label="開啟", command=open_file)
file_menu.add_separator()
file_menu.add_command(label="結束", command=root.quit)
menubar.add_cascade(label="檔案", menu=file_menu)
root.config(menu=menubar)

# 對話方塊 (Dialog)
from tkinter import messagebox, simpledialog

messagebox.showinfo("訊息", "這是訊息方塊")
messagebox.showwarning("警告", "這是警告")
messagebox.showerror("錯誤", "這是錯誤")
result = simpledialog.askstring("輸入", "請輸入文字")

# Treeview (表格)
tree = ttk.Treeview(root, columns=("Name", "Age"), show="headings")
tree.heading("Name", text="姓名")
tree.heading("Age", text="年齡")
tree.insert("", "end", values=("Alice", "25"))
```

### 其他 GUI 框架

| 框架 | 說明 | 適用場景 |
|------|------|----------|
| **PyQt** | 功能強大，跨平台 | 複雜應用程式 |
| **PySide** | Qt 的 Python 綁定 | 與 PyQt 類似 |
| **Kivy** | 支援觸控和行動裝置 | 行動應用、多點觸控 |
| **wxPython** | Python 對 wxWidgets 的綁定 | 跨平台桌面應用 |
| **DearPyGui** | 現代化 GUI 框架 | 遊戲開發、工具程式 |

### 事件綁定

```python
# 鍵盤事件
root.bind("<Key>", on_key_press)
root.bind("<Return>", on_enter)      # Enter 鍵
root.bind("<Escape>", on_escape)     # Escape 鍵
root.bind("<Control-c>", on_copy)    # Ctrl+C
root.bind("<Double-Button-1>", on_double_click)  # 雙擊

# 滑鼠事件
root.bind("<Button-1>", on_click)   # 按一下
root.bind("<B1-Motion>", on_drag)   # 拖曳
root.bind("<ButtonRelease-1>", on_release)  # 放開
```

### Python 官方文件

- [tkinter](https://docs.python.org/3/library/tkinter.html) - Tkinter 完整文件
- [tkinter.ttk](https://docs.python.org/3/library/tkinter.ttk.html) - TTK 增強元件
- [PyQt 官網](https://www.riverbankcomputing.com/software/pyqt/) - PyQt 官方網站

---

*下一章節，我們將學習第 11 章例外處理，讓程式更加健壯。*
