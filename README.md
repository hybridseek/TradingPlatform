# Trading App Database Schema

## Entity Relationship Diagram (ERD)

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
