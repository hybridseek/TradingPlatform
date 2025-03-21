# Trading App Database Schema

---

### ✅ **How to Add to GitHub:**  
1. Open your repository on GitHub.  
2. Open the `README.md` file.  
3. Paste the ERD Markdown code below.  
4. Commit the changes directly to your branch.  
5. Open a Pull Request → Review → Merge!  

---

### 🚀 **Why This Works:**  
✔️ Markdown supports plaintext diagrams using ` ```plaintext ` for consistent formatting.  
✔️ ASCII-style ERD keeps it readable and version-controllable.  
✔️ Clean and professional for documentation!  

---

🔥 **Try it out — you're nailing it!** 😎

## Entity Relationship Diagram (ERD)

```plaintext
+---------------------+           +-----------------+
|       Users         |<--------->|    Wallets      |
|---------------------|           +-----------------+
| id                  |               ^            
| fullName            |               |
| email               |               |         
| ...                 |               |
+---------------------+               |
                                      |
+--------------------+            +--------------------+
|      Assets        |<---------->| WalletTransactions |
|--------------------|            +--------------------+
| id                 |
| quantity           |
| buy_price          |<---------->+-----------------+
| coin_id            |            |  Coins          |
| user_id            |            +-----------------+
+--------------------+            | id              |
                                  | symbol          |
+--------------------+            | ...             |
| Withdrawals        |<---------->+-----------------+
|--------------------|
| id                 |
| status             |
| amount             |
| user_id            |
| date               |
+--------------------+

+--------------------+
| Watchlists         |
|--------------------+
| id                 |
| user_id            |
+--------------------+
          |
          |
          v
+--------------------+
| Watchlist_Coins    |
|--------------------+
| watchlist_id       |
| coin_id            |
+--------------------+

+---------------------+           +---------------------+
|   VerificationCodes |<--------->|        Users        |
|---------------------|           +---------------------+
| id                  |
| otp                 |
| user_id             |
| email               |
| mobile              |
| verification_type   |
+---------------------+

+---------------------+           +---------------------+
|  TradingHistories   |<--------->|        Users        |
|---------------------|           +---------------------+
| id                  |
| selling_price       |
| buying_price        |
| coin_id             |
| user_id             |
+---------------------+

+---------------------+           +---------------------+
|    PaymentOrders    |<--------->|        Users        |
|---------------------|           +---------------------+
| id                  |
| amount              |
| status              |
| payment_method      |
| user_id             |
+---------------------+

+---------------------+           +---------------------+
|   PaymentDetails    |<--------->|        Users        |
|---------------------|           +---------------------+
| id                  |
| account_number      |
| account_holder_name |
| ifsc                |
| bank_name           |
| user_id             |
+---------------------+

+---------------------+           +---------------------+
|        Orders       |<--------->|        Users        |
|---------------------|           +---------------------+
| id                  |
| user_id             |
| order_type          |
| price               |
| timestamp           |
| status              |
| order_item_id       |
+---------------------+
          |
          |
          v
+---------------------+           +---------------------+
|      OrderItems     |<--------->|        Coins        |
|---------------------|           +---------------------+
| id                  |
| quantity            |
| coin_id             |
| buy_price           |
| sell_price          |
| order_id            |
+---------------------+

+---------------------+             +---------------------+
|    Notifications    | <---------> |        Users        |
|---------------------|             +---------------------+
| id                  |
| from_user_id        |
| to_user_id          |
| amount              |
| message             |
+---------------------+

+---------------------+           
|   MarketChartData   |
|---------------------|
| id                  |
| timestamp           |
| price               |
+---------------------+

+---------------------+           +---------------------+
| ForgotPasswordTokens|<--------->|        Users        |
|---------------------|           +---------------------+
| id                  |
| user_id             |
| otp                 |
| verification_type   |
| send_to             |
+---------------------+
```

### ✅ **What Happens Here:**  
✔️ The three backticks (`\`\`\``) after the ERD will **end the plaintext block**.  
✔️ After that, you can continue using regular Markdown formatting without affecting the ERD style.  
✔️ GitHub will display the ERD as a fixed-width, readable diagram while the rest of the document stays clean.  

---

🔥 Now you’ve got it all structured! 😎

---

## Database Tables

### **Users**
| Column Name | Type |
|------------|------|
| id         | INT  |
| fullName   | VARCHAR |
| email      | VARCHAR |
| ...        | ...  |

### **Wallets**
| Column Name | Type |
|------------|------|
| id         | INT  |
| user_id    | INT (FK to Users.id) |

### **Assets**
| Column Name | Type |
|------------|------|
| id         | INT  |
| quantity   | FLOAT |
| buy_price  | FLOAT |
| coin_id    | INT (FK to Coins.id) |
| user_id    | INT (FK to Users.id) |

### **Coins**
| Column Name | Type |
|------------|------|
| id         | INT  |
| symbol     | VARCHAR |
| ...        | ...  |

### **WalletTransactions**
| Column Name | Type |
|------------|------|
| id         | INT  |
| wallet_id  | INT (FK to Wallets.id) |
| coin_id    | INT (FK to Coins.id) |
| quantity   | FLOAT |

### **Withdrawals**
| Column Name | Type |
|------------|------|
| id         | INT  |
| status     | VARCHAR |
| amount     | FLOAT |
| user_id    | INT (FK to Users.id) |
| date       | DATE |

### **Watchlists**
| Column Name | Type |
|------------|------|
| id         | INT  |
| user_id    | INT (FK to Users.id) |

### **Watchlist_Coins**
| Column Name | Type |
|------------|------|
| watchlist_id | INT (FK to Watchlists.id) |
| coin_id       | INT (FK to Coins.id) |

### **VerificationCodes**
| Column Name | Type |
|------------|------|
| id                  | INT  |
| otp                 | VARCHAR |
| user_id             | INT (FK to Users.id) |
| email               | VARCHAR |
| mobile              | VARCHAR |
| verification_type   | VARCHAR |

### **TradingHistories**
| Column Name | Type |
|------------|------|
| id             | INT  |
| selling_price  | FLOAT |
| buying_price   | FLOAT |
| coin_id        | INT (FK to Coins.id) |
| user_id        | INT (FK to Users.id) |

### **PaymentOrders**
| Column Name | Type |
|------------|------|
| id             | INT  |
| amount         | FLOAT |
| status         | VARCHAR |
| payment_method | VARCHAR |
| user_id        | INT (FK to Users.id) |

### **PaymentDetails**
| Column Name          | Type |
|---------------------|------|
| id                  | INT  |
| account_number      | VARCHAR |
| account_holder_name | VARCHAR |
| ifsc                | VARCHAR |
| bank_name           | VARCHAR |
| user_id             | INT (FK to Users.id) |

### **Orders**
| Column Name  | Type |
|-------------|------|
| id          | INT  |
| user_id     | INT (FK to Users.id) |
| order_type  | VARCHAR |
| price       | FLOAT |
| timestamp   | DATETIME |
| status      | VARCHAR |
| order_item_id | INT (FK to OrderItems.id) |

### **OrderItems**
| Column Name | Type |
|------------|------|
| id         | INT  |
| quantity   | FLOAT |
| coin_id    | INT (FK to Coins.id) |
| buy_price  | FLOAT |
| sell_price | FLOAT |
| order_id   | INT (FK to Orders.id) |

### **Notifications**
| Column Name  | Type |
|-------------|------|
| id           | INT  |
| from_user_id  | INT (FK to Users.id) |
| to_user_id    | INT (FK to Users.id) |
| amount        | FLOAT |
| message       | VARCHAR |

### **MarketChartData**
| Column Name | Type |
|------------|------|
| id         | INT  |
| timestamp  | DATETIME |
| price      | FLOAT |

### **ForgotPasswordTokens**
| Column Name         | Type |
|--------------------|------|
| id                 | INT  |
| user_id            | INT (FK to Users.id) |
| otp                | VARCHAR |
| verification_type  | VARCHAR |
| send_to            | VARCHAR |

---

## 🛠️ Relationships
- **Users ↔ Wallets**: One-to-One  
- **Users ↔ Assets**: One-to-Many  
- **Users ↔ Withdrawals**: One-to-Many  
- **Users ↔ Watchlists**: One-to-Many  
- **Watchlists ↔ Watchlist_Coins**: One-to-Many  
- **Assets ↔ Coins**: One-to-One  
- **Orders ↔ OrderItems**: One-to-Many  
- **Coins ↔ OrderItems**: One-to-One  
- **Users ↔ Notifications**: One-to-Many  
- **Users ↔ TradingHistories**: One-to-Many  
- **Users ↔ PaymentOrders**: One-to-Many  
- **Users ↔ PaymentDetails**: One-to-One  

---

### ✅ How to Create Repository and Add This:
1. Create a new repository on GitHub.  
2. Clone the repository:
```sh
git clone https://github.com/your-username/your-repo.git
