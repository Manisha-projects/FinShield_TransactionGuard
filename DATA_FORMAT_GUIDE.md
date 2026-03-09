# 📊 TransactionGuard Data Format Guide

## ✅ Supported Input Formats

Your app accepts **both CSV and JSON** files in multiple formats. The system automatically converts all timestamps to ISO format.

---

## 🔷 JSON Format

### Standard Format (Recommended)
```json
[
  {
    "accountId": "A1",
    "amount": 20000,
    "timestamp": "2026-02-19T10:00:00Z",
    "city": "Delhi"
  },
  {
    "accountId": "A1",
    "amount": 15000,
    "timestamp": "2026-02-19T10:00:30Z",
    "city": "Mumbai"
  }
]
```

### Alternative Field Names (All Supported)
The system recognizes these field name variations:

| Primary | Alternatives |
|---------|--------------|
| `accountId` | `AccountID`, `account_id`, `account` |
| `amount` | `TransactionAmount`, `transaction_amount`, `Txn_Amt` |
| `timestamp` | `TransactionDate`, `transaction_date`, `date`, `Date`, `Txn_Date` |
| `city` | `City`, `Location`, `location`, `Place`, `place` |

### Example with Alternative Names
```json
[
  {
    "AccountID": "A1",
    "TransactionAmount": 20000,
    "TransactionDate": "2026-02-19T10:00:00Z",
    "Location": "Delhi"
  }
]
```

---

## 🔷 CSV Format

### Standard Format
```csv
accountId,amount,timestamp,city
A1,20000,2026-02-19T10:00:00,Delhi
A1,15000,2026-02-19T10:00:30,Mumbai
```

### Alternative Field Names
```csv
AccountID,TransactionAmount,TransactionDate,Location
A1,20000,2026-02-19T10:00:00,Delhi
```

### Space-Separated Values
```csv
accountId amount timestamp city
A1 20000 2026-02-19T10:00:00 Delhi
```

---

## 🕐 Supported Timestamp Formats

The system automatically converts any of these formats to ISO 8601:

### ✅ Already Supported
- **ISO 8601**: `2026-02-19T10:00:00`
- **ISO with space**: `2026-02-19 10:00:00`

### ✅ Automatic Conversion
- **DD/MM/YYYY HH:MM:SS**: `19/02/2026 10:00:00`
- **DD-MM-YYYY HH:MM:SS**: `19-02-2026 10:00:00`
- **MM/DD/YYYY HH:MM:SS**: `02/19/2026 10:00:00`
- **MM/DD/YYYY**: `02/19/2026` (time defaults to 00:00:00)
- **Unix Timestamp (seconds)**: `1740141600`
- **Unix Timestamp (milliseconds)**: `1740141600000`
- **JavaScript Date String**: `Wed Feb 19 2026 10:00:00` (most formats)

### Example Variations
```
Input: "19/02/2026 10:30:45"     → Output: "2026-02-19T10:30:45"
Input: "02-19-2026 14:15:30"     → Output: "2026-02-19T14:15:30"
Input: "1740141600"               → Output: "2026-02-19T11:06:40.000Z"
```

---

## 📋 Fraud Detection Rules

Your system checks for 3 suspicious patterns:

### Rule 1️⃣: High Daily Amount
- **Threshold**: Total daily transactions > **₹50,000**
- **Detection**: Sums all transactions for a given date (YYYY-MM-DD)
- **Example**: If account has ₹30K + ₹25K on 2026-02-19 = ₹55K (FLAGGED ⚠️)

### Rule 2️⃣: Rapid Transactions
- **Threshold**: **More than 3 transactions within 1 minute**
- **Detection**: Counts transactions in 60-second windows
- **Example**: If transactions at 10:00:00, 10:00:15, 10:00:30, 10:00:45 = 4 txns (FLAGGED ⚠️)

### Rule 3️⃣: Different Cities in Short Duration
- **Threshold**: **Transactions from different cities within 30 minutes**
- **Detection**: Compares city locations across 30-minute windows
- **Example**: Transaction in Delhi at 10:00, then Mumbai at 10:15 (FLAGGED ⚠️)

---

## 📥 Uploading Files

### Step 1: Click "Upload CSV / JSON"
- Supports `.csv`, `.json` files
- Automatically detects format (JSON parsed first, then CSV fallback)

### Step 2: Choose File
- JSON files with any valid structure
- CSV files with header row
- Any timestamp format listed above

### Step 3: System Processes
1. ✅ Parses file format
2. ✅ Converts all timestamps to ISO format
3. ✅ Runs fraud detection rules
4. ✅ Displays results

---

## 📤 Output Format

### Results Display
The system outputs:
```json
{
  "accountId": "A1",
  "reason": [
    "High daily transaction amount",
    "Multiple transactions within short time",
    "Transactions from different cities in short duration"
  ]
}
```

### Reasons Returned
- `"High daily transaction amount"` - Rule 1 triggered
- `"Multiple transactions within short time"` - Rule 2 triggered
- `"Transactions from different cities in short duration"` - Rule 3 triggered

---

## 🧪 Test Your Data

### Download Sample Files
- **JSON**: [sample-transactions.json](/sample-transactions.json)
- **CSV**: [sample-transactions.csv](/sample-transactions.csv)

### Test Scenarios
1. **Run Example** - Instant test with 3 transactions
2. **Upload Sample** - Use provided JSON/CSV files
3. **Custom Data** - Upload your own transactions

---

## ⚡ Tips

✅ **Field names are case-insensitive**  
✅ **Extra whitespace is trimmed**  
✅ **Timestamps are auto-converted**  
✅ **Both CSV and JSON work equally**  
✅ **Invalid rows are skipped**  

---

## 🚫 Invalid Data Examples

These will be skipped or show errors:

```json
// Missing required field
{ "accountId": "A1", "amount": 20000 }  // ❌ No timestamp

// Invalid amount
{ "accountId": "A1", "amount": "abc", "timestamp": "2026-02-19", "city": "Delhi" }  // ❌ Non-numeric

// Invalid account ID
{ "accountId": "", "amount": 20000, "timestamp": "2026-02-19", "city": "Delhi" }  // ❌ Empty

// Zero or negative amount
{ "accountId": "A1", "amount": 0, "timestamp": "2026-02-19", "city": "Delhi" }  // ❌ Invalid
```

---

## 💡 Common Questions

**Q: Can I mix timestamp formats?**  
A: Yes! Each timestamp is converted independently.

**Q: What if timestamp is missing?**  
A: Current date/time is used as default.

**Q: Can I use field names in different languages?**  
A: The system only recognizes English field names listed above.

**Q: What's the maximum file size?**  
A: Supports up to 10,000 transactions per file.

**Q: Can I upload multiple files?**  
A: One file at a time. Process separately or combine into one file.

---

**Ready to detect fraud? Upload your data now!** 🔍
