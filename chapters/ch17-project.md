# 第 17 章｜專題實作

## 學習目標

- 整合本書籍所學知識
- 完成一個完整的專案
- 學習專案開發的流程

---

## 專案：通訊錄管理系統

> **💡 Tip（小技巧）**：在開始寫程式之前，先規劃好專案的需求和結構，可以讓開發過程更加順利。建議先畫出流程圖或寫出 pseudo-code。

### 專案需求

建立一個命令列版的通訊錄管理系統，具備以下功能：
1. 新增聯絡人
2. 顯示所有聯絡人
3. 搜尋聯絡人
4. 刪除聯絡人
5. 編輯聯絡人
6. 匯入/匯出資料（JSON）

### 專案結構

> **📝 Note（說明）**：良好的專案結構可以讓程式碼更容易維護。建議將不同功能模組化，每個檔案負責一個主要功能，這樣有利於程式碼的重用和測試。

```
address_book/
├── main.py          # 主程式
├── contact.py       # 聯絡人類別
├── storage.py       # 資料儲存
├── ui.py            # 使用者介面
└── data/
    └── contacts.json # 資料檔案
```

---

## 17.1 建立聯絡人類別

> **💡 Tip（小技巧）**：使用 `@classmethod` 可以提供 Alternative constructors，讓你能夠用不同的方式建立物件，例如從字典或 JSON 資料建立。

### contact.py

```python
"""聯絡人類別"""
from typing import Optional

class Contact:
    """聯絡人類別"""
    
    def __init__(self, name: str, phone: str, 
                 email: Optional[str] = None,
                 address: Optional[str] = None):
        self.name = name
        self.phone = phone
        self.email = email
        self.address = address
    
    def __str__(self):
        return f"{self.name} - {self.phone}"
    
    def __repr__(self):
        return f"Contact(name='{self.name}', phone='{self.phone}')"
    
    def to_dict(self):
        """轉換為字典"""
        return {
            "name": self.name,
            "phone": self.phone,
            "email": self.email,
            "address": self.address
        }
    
    @classmethod
    def from_dict(cls, data: dict):
        """從字典建立"""
        return cls(
            name=data["name"],
            phone=data["phone"],
            email=data.get("email"),
            address=data.get("address")
        )
    
    def update(self, name: str = None, phone: str = None,
               email: str = None, address: str = None):
        """更新聯絡人資訊"""
        if name:
            self.name = name
        if phone:
            self.phone = phone
        if email is not None:
            self.email = email
        if address is not None:
            self.address = address
```

---

## 17.2 資料儲存模組

> **⚠️ Caution（注意）**：在處理檔案時要注意例外處理，確保程式不會因為檔案不存在或權限問題而崩潰。建議使用 `with` 語句來自動管理檔案資源。

### storage.py

```python
"""資料儲存模組"""
import json
import os
from typing import List
from contact import Contact

class Storage:
    """通訊錄儲存"""
    
    def __init__(self, filename: str = "contacts.json"):
        self.filename = filename
    
    def save(self, contacts: List[Contact]):
        """儲存到檔案"""
        data = [c.to_dict() for c in contacts]
        
        # 確保目錄存在
        os.makedirs(os.path.dirname(self.filename) or ".", exist_ok=True)
        
        with open(self.filename, "w", encoding="utf-8") as f:
            json.dump(data, f, ensure_ascii=False, indent=2)
    
    def load(self) -> List[Contact]:
        """從檔案載入"""
        if not os.path.exists(self.filename):
            return []
        
        try:
            with open(self.filename, "r", encoding="utf-8") as f:
                data = json.load(f)
                return [Contact.from_dict(d) for d in data]
        except (json.JSONDecodeError, FileNotFoundError):
            return []
```

---

## 17.3 使用者介面

### ui.py

```python
"""使用者介面模組"""
from typing import List
from contact import Contact

class UI:
    """命令列使用者介面"""
    
    @staticmethod
    def show_menu():
        """顯示選單"""
        print("\n" + "=" * 40)
        print("     通訊錄管理系統")
        print("=" * 40)
        print("1. 新增聯絡人")
        print("2. 顯示所有聯絡人")
        print("3. 搜尋聯絡人")
        print("4. 刪除聯絡人")
        print("5. 編輯聯絡人")
        print("6. 匯入資料")
        print("7. 匯出資料")
        print("0. 離開系統")
        print("=" * 40)
    
    @staticmethod
    def get_choice() -> str:
        """取得選項"""
        return input("請選擇：")
    
    @staticmethod
    def get_contact_info() -> dict:
        """取得聯絡人資訊"""
        print("\n新增聯絡人：")
        name = input("姓名：").strip()
        phone = input("電話：").strip()
        email = input("Email（可選）：").strip()
        address = input("地址（可選）：").strip()
        
        return {
            "name": name,
            "phone": phone,
            "email": email if email else None,
            "address": address if address else None
        }
    
    @staticmethod
    def show_contacts(contacts: List[Contact]):
        """顯示聯絡人列表"""
        if not contacts:
            print("\n通訊錄是空的！")
            return
        
        print(f"\n共有 {len(contacts)} 位聯絡人：")
        print("-" * 60)
        for i, contact in enumerate(contacts, 1):
            print(f"{i}. {contact.name}")
            print(f"   電話：{contact.phone}")
            if contact.email:
                print(f"   Email：{contact.email}")
            if contact.address:
                print(f"   地址：{contact.address}")
            print("-" * 60)
    
    @staticmethod
    def show_message(message: str):
        """顯示訊息"""
        print(f"\n{message}")
    
    @staticmethod
    def get_search_keyword() -> str:
        """取得搜尋關鍵字"""
        return input("\n請輸入搜尋關鍵字（姓名或電話）：").strip()
```

---

## 17.4 主程式

### main.py

```python
"""通訊錄管理系統 - 主程式"""
from typing import List
from contact import Contact
from storage import Storage
from ui import UI

class AddressBook:
    """通訊錄管理系統"""
    
    def __init__(self):
        self.contacts: List[Contact] = []
        self.storage = Storage()
        self.ui = UI()
        self.load_data()
    
    def load_data(self):
        """載入資料"""
        self.contacts = self.storage.load()
        self.ui.show_message(f"已載入 {len(self.contacts)} 位聯絡人")
    
    def save_data(self):
        """儲存資料"""
        self.storage.save(self.contacts)
        self.ui.show_message("資料已儲存")
    
    def add_contact(self):
        """新增聯絡人"""
        info = self.ui.get_contact_info()
        
        if not info["name"] or not info["phone"]:
            self.ui.show_message("姓名和電話不能為空！")
            return
        
        contact = Contact(**info)
        self.contacts.append(contact)
        self.ui.show_message(f"已新增聯絡人：{contact.name}")
        self.save_data()
    
    def show_contacts(self):
        """顯示所有聯絡人"""
        self.ui.show_contacts(self.contacts)
    
    def search_contact(self):
        """搜尋聯絡人"""
        keyword = self.ui.get_search_keyword()
        
        results = [c for c in self.contacts 
                   if keyword in c.name or keyword in c.phone]
        
        if results:
            self.ui.show_contacts(results)
        else:
            self.ui.show_message("找不到符合的聯絡人")
    
    def delete_contact(self):
        """刪除聯絡人"""
        self.ui.show_contacts(self.contacts)
        
        try:
            index = int(input("\n請輸入編號（0 取消）：")) - 1
            if index < 0 or index >= len(self.contacts):
                self.ui.show_message("取消刪除")
                return
            
            contact = self.contacts[index]
            confirm = input(f"確定要刪除 {contact.name} 嗎？(y/n)：")
            
            if confirm.lower() == "y":
                self.contacts.pop(index)
                self.ui.show_message(f"已刪除 {contact.name}")
                self.save_data()
        except ValueError:
            self.ui.show_message("輸入無效")
    
    def edit_contact(self):
        """編輯聯絡人"""
        self.ui.show_contacts(self.contacts)
        
        try:
            index = int(input("\n請輸入編號（0 取消）：")) - 1
            if index < 0 or index >= len(self.contacts):
                self.ui.show_message("取消編輯")
                return
            
            contact = self.contacts[index]
            print(f"\n編輯 {contact.name}（直接 Enter 保留原值）：")
            
            name = input(f"姓名 [{contact.name}]：").strip()
            phone = input(f"電話 [{contact.phone}]：").strip()
            email = input(f"Email [{contact.email or '-'}]：").strip()
            address = input(f"地址 [{contact.address or '-'}]：").strip()
            
            contact.update(
                name=name or None,
                phone=phone or None,
                email=email if email else None,
                address=address if address else None
            )
            
            self.ui.show_message("已更新聯絡人")
            self.save_data()
        except ValueError:
            self.ui.show_message("輸入無效")
    
    def run(self):
        """執行主迴圈"""
        while True:
            self.ui.show_menu()
            choice = self.ui.get_choice()
            
            if choice == "1":
                self.add_contact()
            elif choice == "2":
                self.show_contacts()
            elif choice == "3":
                self.search_contact()
            elif choice == "4":
                self.delete_contact()
            elif choice == "5":
                self.edit_contact()
            elif choice == "0":
                self.ui.show_message("感謝使用，再見！")
                break
            else:
                self.ui.show_message("選項無效，請重新選擇")


if __name__ == "__main__":
    app = AddressBook()
    app.run()
```

---

## 17.5 執行與測試

### 執行方式

```bash
python main.py
```

### 執行範例

```
========================================
     通訊錄管理系統
========================================
1. 新增聯絡人
2. 顯示所有聯絡人
3. 搜尋聯絡人
4. 刪除聯絡人
5. 編輯聯絡人
6. 匯入資料
7. 匯出資料
0. 離開系統
========================================
請選擇：1

新增聯絡人：
姓名：小明
電話：0912345678
Email： 
地址： 
已新增聯絡人：小明
```

---

## 17.6 Turtle 專案：整合應用

學會了這麼多，讓我們用 Turtle 來做一個完整的專案！

### 專案：自動藝術生成器

```python
import turtle
import random
import json

class ArtGenerator:
    """藝術生成器類別"""
    
    def __init__(self):
        self.turtle = turtle.Turtle()
        self.turtle.speed(0)
        self.turtle.width(2)
        self.shapes = []
    
    def add_shape(self, shape_type, x, y, size, color):
        """新增圖形"""
        shape = {
            "type": shape_type,
            "x": x,
            "y": y,
            "size": size,
            "color": color
        }
        self.shapes.append(shape)
        return shape
    
    def draw_all(self):
        """畫出所有圖形"""
        for shape in self.shapes:
            self.turtle.penup()
            self.turtle.goto(shape["x"], shape["y"])
            self.turtle.pendown()
            self.turtle.color(shape["color"])
            
            if shape["type"] == "circle":
                self.turtle.circle(shape["size"])
            elif shape["type"] == "square":
                for i in range(4):
                    self.turtle.forward(shape["size"])
                    self.turtle.right(90)
            elif shape["type"] == "triangle":
                for i in range(3):
                    self.turtle.forward(shape["size"])
                    self.turtle.right(120)
    
    def save_to_file(self, filename):
        """儲存到檔案"""
        with open(filename, "w", encoding="utf-8") as f:
            json.dump(self.shapes, f, indent=2)
        print(f"已儲存 {len(self.shapes)} 個圖形到 {filename}")
    
    def load_from_file(self, filename):
        """從檔案讀取"""
        with open(filename, "r", encoding="utf-8") as f:
            self.shapes = json.load(f)
        print(f"已讀取 {len(self.shapes)} 個圖形")

# 使用範例
generator = ArtGenerator()

# 新增圖形
generator.add_shape("circle", -100, 0, 50, "red")
generator.add_shape("square", 0, 0, 60, "green")
generator.add_shape("triangle", 100, 0, 70, "blue")

# 儲存
generator.save_to_file("my_art.json")

# 畫圖
generator.draw_all()

turtle.done()
```

### 練習：通訊錄 Turtle 版本

```python
import turtle
import json

class ContactDrawer:
    """用 Turtle 顯示通訊錄"""
    
    def __init__(self):
        self.contacts = []
    
    def add_contact(self, name, phone):
        self.contacts.append({"name": name, "phone": phone})
    
    def display_all(self):
        """在 Turtle 視窗中顯示所有聯絡人"""
        y = 150
        for contact in self.contacts:
            turtle.penup()
            turtle.goto(0, y)
            turtle.pendown()
            text = f"{contact['name']}: {contact['phone']}"
            turtle.write(text, align="center", font=("Arial", 14, "normal"))
            y -= 30

# 建立通訊錄
contacts = ContactDrawer()
contacts.add_contact("小明", "0912345678")
contacts.add_contact("小華", "0987654321")
contacts.add_contact("小美", "0977123456")

# 顯示
contacts.display_all()

turtle.done()
```

---

## 17.7 實用範例 - 額外小專案

### 專案 1：天氣查詢程式

結合 API 的天氣查詢程式！

```python
# 天氣查詢程式
# 學習重點：整合之前所學知識

import json
import os

# 簡易天氣資料庫（類比）
weather_db = {
    "台北": {"temp": 25, "weather": "晴", "humidity": 60},
    "台中": {"temp": 28, "weather": "晴", "humidity": 55},
    "高雄": {"temp": 30, "weather": "陰", "humidity": 70},
    "花蓮": {"temp": 24, "weather": "雨", "humidity": 80},
    "基隆": {"temp": 22, "weather": "雨", "humidity": 85},
}

def save_history(data, filename="weather_history.json"):
    """儲存查詢歷史"""
    with open(filename, "w", encoding="utf-8") as f:
        json.dump(data, f, ensure_ascii=False, indent=2)

def load_history(filename="weather_history.json"):
    """載入查詢歷史"""
    if os.path.exists(filename):
        with open(filename, "r", encoding="utf-8") as f:
            return json.load(f)
    return []

def get_weather(city):
    """查詢天氣"""
    if city in weather_db:
        return weather_db[city]
    return None

def show_weather(city, data):
    """顯示天氣資訊"""
    print(f"\n{'='*40}")
    print(f"   {city} 的天氣")
    print(f"{'='*40}")
    print(f"溫度：{data['temp']}°C")
    print(f"天氣：{data['weather']}")
    print(f"濕度：{data['humidity']}%")
    print(f"{'='*40}")
    
    # 給出建議
    if data['weather'] == "雨":
        print("💡 建議：記得帶傘！")
    elif data['temp'] > 28:
        print("💡 建議：注意防曬，多喝水！")
    elif data['temp'] < 20:
        print("💡 建議：天氣涼爽，注意保暖！")

# 主程式
print("=" * 50)
print("        🌤️  天氣查詢系統  🌤️")
print("=" * 50)

# 載入歷史
history = load_history()

if history:
    print("\n最近查詢過的城市：")
    for h in history[-5:]:
        print(f"  - {h}")

print("\n可查詢的城市：")
for city in weather_db.keys():
    print(f"  - {city}")

# 查詢迴圈
while True:
    print("\n" + "-" * 50)
    city = input("輸入城市名稱（輸入 q 離開）：")
    
    if city.lower() == "q":
        break
    
    if city in weather_db:
        data = get_weather(city)
        show_weather(city, data)
        
        # 記錄歷史
        if city not in history:
            history.append(city)
            save_history(history)
    else:
        print(f"\n抱歉，查不到 {city} 的天氣資訊")

print("\n感謝使用天氣查詢系統！")

# 顯示統計
print("\n===== 查詢統計 =====")
print(f"已查詢過 {len(set(history))} 個城市")
print(f"總查詢次數：{len(history)}")
```

---

### 專案 2：待辦事項管理程式

完整的待辦事項應用程式！

```python
# 待辦事項管理程式
# 整合檔案 IO、例外處理、OOP

import json
import os
from datetime import datetime

class TodoItem:
    """待辦事項類別"""
    def __init__(self, title, description="", priority="中"):
        self.title = title
        self.description = description
        self.priority = priority
        self.completed = False
        self.created_at = datetime.now().strftime("%Y-%m-%d %H:%M")
    
    def to_dict(self):
        return {
            "title": self.title,
            "description": self.description,
            "priority": self.priority,
            "completed": self.completed,
            "created_at": self.created_at
        }
    
    @classmethod
    def from_dict(cls, data):
        item = cls(data["title"], data["description"], data["priority"])
        item.completed = data["completed"]
        item.created_at = data["created_at"]
        return item
    
    def __str__(self):
        status = "✓" if self.completed else " "
        return f"[{status}] {self.title} (優先度:{self.priority})"

class TodoApp:
    """待辦事項應用"""
    def __init__(self, filename="todos.json"):
        self.filename = filename
        self.items = []
        self.load()
    
    def load(self):
        """載入資料"""
        if os.path.exists(self.filename):
            try:
                with open(self.filename, "r", encoding="utf-8") as f:
                    data = json.load(f)
                    self.items = [TodoItem.from_dict(d) for d in data]
            except:
                self.items = []
    
    def save(self):
        """儲存資料"""
        try:
            with open(self.filename, "w", encoding="utf-8") as f:
                json.dump([i.to_dict() for i in self.items], f, ensure_ascii=False, indent=2)
            print("✅ 已儲存！")
        except Exception as e:
            print(f"❌ 儲存失敗：{e}")
    
    def add(self):
        """新增待辦"""
        print("\n--- 新增待辦 ---")
        title = input("標題：")
        if not title:
            print("標題不能為空！")
            return
        
        description = input("描述（可選）：")
        print("優先度：1.高 2.中 3.低")
        p_choice = input("選擇：")
        priority = {"1": "高", "2": "中", "3": "低"}.get(p_choice, "中")
        
        self.items.append(TodoItem(title, description, priority))
        print("✅ 已新增！")
    
    def list_items(self):
        """列出待辦"""
        if not self.items:
            print("\n沒有待辦事項！")
            return
        
        print("\n===== 待辦事項 =====")
        
        # 分類顯示
        pending = [i for i in self.items if not i.completed]
        completed = [i for i in self.items if i.completed]
        
        print(f"\n待辦 ({len(pending)})：")
        for i, item in enumerate(pending, 1):
            print(f"{i}. {item}")
        
        if completed:
            print(f"\n已完成 ({len(completed)})：")
            for i, item in enumerate(completed, 1):
                print(f"{i}. {item}")
    
    def complete(self):
        """標記完成"""
        pending = [i for i in self.items if not i.completed]
        if not pending:
            print("沒有待辦事項！")
            return
        
        print("\n--- 標記完成 ---")
        self.list_items()
        
        try:
            idx = int(input("\n輸入編號：")) - 1
            if 0 <= idx < len(pending):
                pending[idx].completed = True
                print("✅ 已標記完成！")
            else:
                print("無效編號！")
        except ValueError:
            print("輸入無效！")
    
    def delete(self):
        """刪除"""
        if not self.items:
            print("沒有待辦事項！")
            return
        
        print("\n--- 刪除 ---")
        self.list_items()
        
        try:
            idx = int(input("\n輸入編號：")) - 1
            if 0 <= idx < len(self.items):
                removed = self.items.pop(idx)
                print(f"✅ 已刪除：{removed.title}")
            else:
                print("無效編號！")
        except ValueError:
            print("輸入無效！")

# 主程式
app = TodoApp()

print("=" * 50)
print("        📝 待辦事項管理系統 📝")
print("=" * 50)

while True:
    print("\n選項：")
    print("1. 新增待辦")
    print("2. 列出待辦")
    print("3. 標記完成")
    print("4. 刪除")
    print("5. 儲存")
    print("0. 離開")
    
    choice = input("選擇：")
    
    if choice == "1":
        app.add()
    elif choice == "2":
        app.list_items()
    elif choice == "3":
        app.complete()
    elif choice == "4":
        app.delete()
    elif choice == "5":
        app.save()
    elif choice == "0":
        app.save()
        print("感謝使用！")
        break
    else:
        print("無效選擇！")
```

---

## 練習題

### 基礎題

1. **圖形介面**：使用 tkinter 製作圖形介面版本
2. **資料驗證**：加入電話號碼格式驗證
3. **分類功能**：加入聯絡人分類（家人、朋友、同事等）
4. **匯入功能**：從 CSV 檔案匯入聯絡人
5. **密碼保護**：加入密碼保護功能

### 進階題

1. **搜尋功能**：加入多種搜尋方式（姓名、電話、Email）
2. **排序功能**：讓聯絡人可依不同欄位排序
3. **匯出功能**：將通訊錄匯出為 CSV 格式
4. **重複檢查**：新增聯絡人時檢查是否已存在
5. **修改記錄**：記錄每次修改的時間
6. **雲端同步**：使用 Firebase 進行資料同步
7. **搜尋引擎**：加入模糊搜尋功能
8. **統計分析**：顯示通訊錄統計圖表

### 挑戰題

1. **網頁版**：使用 Flask 或 Django 製作網頁版
2. **API 設計**：提供 REST API 供其他程式呼叫
3. **行動版**：使用 Kivy 製作手機 App 版
4. **測試覆蓋**：撰寫單元測試和整合測試
5. **CI/CD**：建立自動化測試和部署流程
6. **匯入匯出**：支援 vCard 格式的匯入匯出
7. **群組功能**：支援建立群組並管理群組成員

---

## 結語

> **📝 Note（說明）**：恭喜你完成了 Python 程式設計的學習！記住，程式設計是不斷學習和實踐的過程。持續練習、參與專案、閱讀他人程式碼，你會越來越厲害！

恭喜你完成了這本 Python 程式設計教材！

你現在應該已經掌握：
- Python 基礎語法
- 資料結構（串列、字典、集合）
- 函式與模組
- 物件導向程式設計
- 檔案操作與例外處理
- 演算法基礎

這只是程式設計的起點，持續練習和探索，你會發現 Python 的世界無比寬廣！

---

## 進一步閱讀

### 進階學習方向

| 領域 | 說明 | 推薦資源 |
|------|------|----------|
| **Web 開發** | Flask / Django | Flask 中文文档、Django 官方教程 |
| **資料科學** | Pandas / NumPy / Matplotlib | Python Data Science Handbook |
| **機器學習** | scikit-learn / TensorFlow / PyTorch | 官方教程、Kaggle 競賽 |
| **自動化測試** | pytest / unittest | pytest 文档 |
| **網路爬蟲** | requests / BeautifulSoup / Scrapy | 官方文档 |
| **DevOps** | Docker / Ansible | 官方文档 |

### 推薦學習網站

- [Real Python](https://realpython.com/) - 高品質 Python 教學
- [Python.org](https://www.python.org/) - 官方文件
- [Stack Overflow](https://stackoverflow.com/) - 問答社群
- [GitHub](https://github.com/) - 程式碼托管
- [LeetCode](https://leetcode.com/) - 演算法練習
- [Kaggle](https://www.kaggle.com/) - 資料科學競賽
- [Medium](https://medium.com/) - 技術文章

### 實用工具推薦

```python
# 開發環境
VS Code + Python 擴展
PyCharm
Jupyter Notebook / JupyterLab
Google Colab

# 版本控制
Git
GitHub / GitLab / Bitbucket

# 專案管理
pip / pipenv / poetry
virtualenv / conda
Docker
```

### 未來可以挑戰的專案

1. **個人部落格** - 使用 Flask 或 Django 建立
2. **天氣APP** - 串接天氣 API
3. **股票分析工具** - 視覺化股票資料
4. **聊天室** - 即時通訊應用
5. **自動化腳本** - 日常工作自動化
6. **機器學習專案** - 影像辨識或自然語言處理

---

*祝你在程式設計的道路上持續前進！*
