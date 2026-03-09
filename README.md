# 🛡️ TransactionGuard

**TransactionGuard** is a Suspicious Transaction Detection System that analyzes banking transactions and flags accounts that show potentially fraudulent behavior based on predefined risk rules.

The system processes transaction data and detects unusual patterns such as high daily spending, rapid transactions, or transactions from different locations within a short period.

---

# 🚨 Problem Statement

Banks and financial institutions continuously monitor customer transactions to detect suspicious or fraudulent activity.

Unusual spending patterns, rapid transactions, or transactions from different locations within a short time period may indicate fraud.

This project implements a **JavaScript-based fraud detection system** that analyzes transaction data and flags suspicious accounts.

---

# ⚙️ Tech Stack

- **React**
- **TypeScript**
- **Node.js**
- **Vite**
- **Bun**
- **JavaScript**
- **CSS**

---

# 📊 Transaction Data Format

Each transaction record contains:

- `accountId`
- `amount`
- `timestamp` (ISO format)
- `city`

Example:

```json
{
  "accountId": "A1",
  "amount": 20000,
  "timestamp": "2026-02-19T10:00:00",
  "city": "Delhi"
}
```

---

# 🔍 Fraud Detection Rules

The system flags accounts if any of the following conditions are met:

### 1️⃣ High Daily Transaction Amount
If the **total transaction amount in a single day exceeds ₹50,000**

---

### 2️⃣ Rapid Transactions
If **more than 3 transactions occur within 1 minute**

---

### 3️⃣ Different Cities in Short Duration
If **transactions occur from different cities within 30 minutes**

---

# 🧠 Processing Logic

1. Load transaction data (JSON format)
2. Group transactions by **accountId**
3. Sort transactions by **timestamp**
4. Apply fraud detection rules
5. Generate a report of flagged accounts

---

# 📥 Input Format

```json
[
  {
    "accountId": "A1",
    "amount": 20000,
    "timestamp": "2026-02-19T10:00:00",
    "city": "Delhi"
  },
  {
    "accountId": "A1",
    "amount": 15000,
    "timestamp": "2026-02-19T10:00:30",
    "city": "Delhi"
  },
  {
    "accountId": "A1",
    "amount": 20000,
    "timestamp": "2026-02-19T10:01:00",
    "city": "Mumbai"
  }
]
```

---

# 📤 Output Format

The system returns flagged accounts along with the fraud reasons.

```json
[
  {
    "accountId": "A1",
    "reason": [
      "High daily amount",
      "Multiple transactions in short time",
      "Different cities within short duration"
    ]
  }
]
```

---

# ⚠️ Edge Cases Considered

The system also handles:

- Transactions across **multiple days**
- **Multiple transactions at the same timestamp**
- Accounts with **only one transaction**
- Cases where **no accounts are flagged**

---



---

# 🚀 Running the Project

### Install dependencies

```bash
npm install
```

or

```bash
bun install
```

---

### Start development server

```bash
npm run dev
```

or

```bash
bun dev
```

---

# 📈 System Capacity

- Supports up to **10,000 transactions**
- Efficient grouping and rule evaluation
- Structured **JSON output**

---

# 🎯 Goal

The goal of this system is to demonstrate how rule-based fraud detection can help financial institutions quickly identify suspicious activity and prevent fraudulent transactions.

---

# 👨‍💻 Author

**Manisha Dutta**

GitHub  
https://github.com/Manisha-projects