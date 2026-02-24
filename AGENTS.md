# AGENTS.md - 代理編碼指南

本文檔為在此專案庫中工作的 AI 代理提供編碼指南。

## 建置、Lint 與測試指令

### 常用指令
```bash
# 安裝依賴
pip install -r requirements.txt
pip install -e .  # 可編輯安裝

# 執行應用程式
python -m <package_name>

# 執行所有測試
pytest

# 執行測試並顯示覆蓋率
pytest --cov=<package_name> --cov-report=term-missing

# 執行單一測試檔案
pytest tests/test_file.py

# 執行單一測試函數
pytest tests/test_file.py::test_function_name

# 執行符合模式的測試
pytest -k "test_pattern"

# Linting
flake8 .
pylint <package_name>

# 型別檢查
mypy <package_name>

# 格式化
black .
isort .

# 所有檢查 (lint + typecheck + tests)
pytest && flake8 . && mypy <package_name>
```

### Pre-commit 鉤子
```bash
pre-commit install
pre-commit run --all-files
```

## 程式碼風格指南

### 匯入 (Imports)
- 盡可能使用絕對匯入而非相對匯入
- 匯入分組順序：標準庫、第三方、本地/應用程式
- 各組內按字母排序
- 使用 `isort` 自動排序
- 範例：
  ```python
  import os
  import sys
  from typing import Any, Dict, List, Optional

  import numpy as np
  import pandas as pd
  from fastapi import APIRouter, HTTPException

  from myapp import utils
  from myapp.models import User
  from myapp.schemas import UserCreate
  ```

### 格式化
- 使用 Black 格式化（行長：88 字元）
- 使用 isort 排序匯入
- 最大行長：88 字元（Black 預設）
- 所有函式簽名使用型別提示
- 加入回傳型別標註
- 為相容 Python < 3.10，使用 `Optional[X]` 而非 `X | None`

### 型別
- 所有公開函式使用明確的型別提示
- 盡量少用 `Any`，偏好具體型別
- 使用 typing 中的 `Dict`、`List`、`Tuple`（或 Python 3.9+ 的 lowercase 版本）
- 範例：
  ```python
  def process_users(user_ids: List[int]) -> Dict[int, User]:
      ...
  ```

### 命名慣例
- **變數**：`snake_case`（例如 `user_id`、`total_count`）
- **函式**：`snake_case`（例如 `get_user_by_id`、`calculate_total`）
- **類別**：`PascalCase`（例如 `UserService`、`PaymentProcessor`）
- **常數**：`UPPER_SNAKE_CASE`（例如 `MAX_RETRIES`、`DEFAULT_TIMEOUT`）
- **私有方法/屬性**：前綴底線（例如 `_internal_method`）
- **檔案**：`snake_case.py`（例如 `user_service.py`、`utils.py`）

### 錯誤處理
- 為領域特定錯誤使用自訂例外類別
- 捕捉特定例外，避免裸 `except:`
- 只在必要時使用 `try/except`；偏好 EAFP（取得原諒比請求許可更容易）
- 拋出具描述性的錯誤訊息並附帶上下文
- 範例：
  ```python
  class UserNotFoundError(Exception):
      pass

  def get_user(user_id: int) -> User:
      user = db.query(User).filter(User.id == user_id).first()
      if not user:
          raise UserNotFoundError(f"User with id {user_id} not found")
      return user
  ```

### 日誌記錄
- 使用 `logging` 模組，而非 print 陳述式
- 使用適當的日誌級別：DEBUG、INFO、WARNING、ERROR、CRITICAL
- 在日誌訊息中包含上下文
- 範例：
  ```python
  logger = logging.getLogger(__name__)

  logger.info(f"Processing request for user {user_id}")
  logger.error(f"Failed to process payment: {error}")
  ```

### 非同步程式碼
- 一致使用 `async`/`await`
- 使用 `aiohttp` 或 `httpx` 進行非同步 HTTP 請求
- 避免在非同步函式中使用阻塞呼叫
- 使用 `asyncio.gather` 進行並發操作

### 資料庫
- 使用 ORM 並正確管理 session
- 使用依賴注入取得資料庫 session
- 在 finally 區塊或使用 context manager 關閉 session
- 對多步驟操作使用交易

### 測試
- 為所有公開函式撰寫測試
- 使用描述性的測試名稱：`test_<函式名稱>_<預期行為>`
- 為常見測試資料使用 fixtures
- Mock 外部依賴
- 測試邊界情況和錯誤條件
- 保持測試快速 - mock 慢速操作
- 範例：
  ```python
  def test_get_user_by_id_returns_user():
      user = get_user(user_id=1)
      assert user.id == 1
      assert user.name == "John"

  def test_get_user_not_found_raises_error():
      with pytest.raises(UserNotFoundError):
          get_user(user_id=999)
  ```

### 設定
- 敏感資料使用環境變數
- 非敏感性設定使用設定檔（例如 `.env`、`config.yaml`）
- 絕不將密鑰提交至版本控制
- 使用 `.env.example` 作為範本

### 文件
- 為所有公開函式和類別撰寫文件字串
- 使用 Google 風格或 NumPy 風格的文件字串
- 在文件中包含型別提示以提高可讀性
- 範例：
  ```python
  def calculate_total(items: List[Item], tax_rate: float = 0.1) -> float:
      """計算含稅的總價格。

      Args:
          items: 要計算的項目清單。
          tax_rate: 稅率小數（預設 0.1）。

      Returns:
          含稅的總價格。

      Raises:
          ValueError: 如果項目清單為空。
      """
      if not items:
          raise ValueError("Items list cannot be empty")
      subtotal = sum(item.price for item in items)
      return subtotal * (1 + tax_rate)
  ```

### Git 慣例
- 使用有意義的 commit 訊息
- 保持 commit 原子性（每個 commit 只做一件事）
- 為新功能建立功能分支
- 合併前使用 PR 進行程式碼審查

### 安全性
- 絕不硬編碼密鑰或 API 金鑰
- 驗證所有使用者輸入
- 使用參數化查詢防止 SQL 注入
- 消毒輸出以防止 XSS（若適用）
- 保持依賴更新

## 專案結構

```
project/
├── src/
│   └── package/
│       ├── __init__.py
│       ├── main.py
│       ├── models/
│       ├── schemas/
│       ├── services/
│       ├── routers/
│       └── utils/
├── tests/
│   ├── __init__.py
│   ├── conftest.py
│   └── test_*.py
├── .env
├── .env.example
├── pyproject.toml
├── setup.py
└── README.md
```

## python-textbook 教材專案

此專案為 Python 程式設計教材，適用於大一新生或程式設計初學者。

### 專案結構

```
python-textbook/
├── README.md           # 書籍資訊與章節目錄
└── chapters/
    ├── ch01-introduction.md   # 第 1 章：緒論
    ├── ch02-variables.md      # 第 2 章：變數與資料型態
    ├── ch03-conditional.md    # 第 3 章：條件判斷
    ├── ch04-loop.md           # 第 4 章：迴圈
    ├── ch05-function.md       # 第 5 章：函式
    ├── ch06-list-tuple.md     # 第 6 章：串列與元組
    ├── ch07-dict-set.md       # 第 7 章：字典與集合
    ├── ch08-string.md         # 第 8 章：字串處理
    ├── ch09-file.md           # 第 9 章：檔案操作
    ├── ch10-gui.md            # 第 10 章：圖形使用者介面
    ├── ch11-exception.md      # 第 11 章：例外處理
    ├── ch12-oop.md            # 第 12 章：物件導向基礎
    ├── ch13-module.md         # 第 13 章：模組與套件
    ├── ch14-algorithm.md      # 第 14 章：演算法基礎
    ├── ch15-functional.md     # 第 15 章：函式式程式設計
    ├── ch16-tools.md          # 第 16 章：實用工具與技巧
    └── ch17-project.md        # 第 17 章：專題實作
```

### 章節格式規範

每章節應包含以下結構：

1. **學習目標** - 列出本章節的學習重點
2. **內容段落** - 依主題分為多個小節（13.1, 13.2...）
3. **本章小結** - 語法表格總結
4. **練習題** - 三個難度的練習題
5. **進一步閱讀** - 相關資源連結

### 練習題格式

```markdown
## 練習題

### 基礎題

1. **題目名稱**：描述

### 進階題

1. **題目名稱**：描述

### 挑戰題

1. **題目名稱**：描述
```

- **基礎題**：5-10 題，驗證基本概念
- **進階題**：4-8 題，應用與整合
- **挑戰題**：3-7 題，進階思考與專案
