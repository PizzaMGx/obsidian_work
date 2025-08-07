---
weight: 4
title: 🛡️ Tamper-Proof Transactions in Django with PostgreSQL - Blockchain & Concurrency Controls
date: 2025-07-30
draft: false
author: Vincent
description: "🛡️ Tamper-Proof Transactions in Django with PostgreSQL: Blockchain & Concurrency Controls"
tags:
  - IT
categories:
  - IT
---
### Intro
As applications scale and data integrity becomes critical, it's essential to implement safeguards that prevent tampering and maintain consistency. In this post, we’ll explore how to:

1. Build a **blockchain-like audit trail** using PostgreSQL
2. Use `SELECT ... FOR UPDATE` to prevent **race conditions**
3. Apply both techniques in a **Django environment**

---

### 🔗 Part 1: Blockchain-like Audit Trail in PostgreSQL

Blockchain’s core strength lies in its immutability—every record links cryptographically to the previous one. We can simulate this in PostgreSQL with a simple hash chaining approach.

#### 📦 Use Case: Financial Transactions

Let’s say you have a `transactions` table. To prevent tampering, we’ll store a `previous_hash` and `hash` column for each row.

#### 🧱 Table Design

```sql
CREATE TABLE transactions (
    id SERIAL PRIMARY KEY,
    sender_id INTEGER NOT NULL,
    receiver_id INTEGER NOT NULL,
    amount NUMERIC(10,2) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    previous_hash TEXT,
    hash TEXT NOT NULL
);
```

#### 🔁 Hash Generation Logic

Every new transaction will:

- Hash its content (sender, receiver, amount, timestamp, `previous_hash`)
- Store that as `hash`
- Use the previous row's `hash` as `previous_hash`

#### 🔐 Hashing in Python

Here’s how you generate the hash in Django:

```python
import hashlib

def generate_hash(transaction_data: dict) -> str:
    transaction_string = f"{transaction_data['sender_id']}{transaction_data['receiver_id']}{transaction_data['amount']}{transaction_data['created_at']}{transaction_data['previous_hash']}"
    return hashlib.sha256(transaction_string.encode()).hexdigest()
```

#### ➕ Creating a New Transaction

In Django:

```python
def create_transaction(sender, receiver, amount):
    from .models import Transaction
    last_tx = Transaction.objects.order_by('-id').first()

    tx_data = {
        "sender_id": sender.id,
        "receiver_id": receiver.id,
        "amount": amount,
        "created_at": timezone.now(),
        "previous_hash": last_tx.hash if last_tx else '',
    }

    tx_hash = generate_hash(tx_data)

    Transaction.objects.create(
        sender_id=sender.id,
        receiver_id=receiver.id,
        amount=amount,
        previous_hash=tx_data["previous_hash"],
        hash=tx_hash
    )
```

With this structure, **any modification to past data will break the hash chain**. You can verify the chain with a simple Python script.

---

### 🚥 Part 2: Preventing Race Conditions with `FOR UPDATE`

If multiple users try to withdraw from the same account simultaneously, you may end up with a negative balance unless you **lock the row during the transaction**.

#### For that we use: `SELECT ... FOR UPDATE`

This will lock the row until the transaction completes.

In Django:

```python
from django.db import transaction

def transfer_funds(sender_id, receiver_id, amount):
    with transaction.atomic():
        sender = Account.objects.select_for_update().get(pk=sender_id)
        receiver = Account.objects.select_for_update().get(pk=receiver_id)

        if sender.balance < amount:
            raise ValueError("Insufficient funds")

        sender.balance -= amount
        receiver.balance += amount

        sender.save()
        receiver.save()
```

This ensures:

- No two transactions modify the same row at the same time.
- Prevents overdraw and other race-condition bugs.

---

### 🧠 Final Thoughts

By combining a **blockchain-like structure** to track historical integrity and **row-level locking** to maintain consistency, your Django + PostgreSQL stack becomes incredibly resilient for financial or critical transactional systems.

These approaches are powerful because:

- 🔒 They **enhance auditability**
- ⚖️ They **preserve correctness**
- 💪 They **scale with confidence**

---

### 🏁 Bonus: How to Apply This

✅ Use hash chaining in models like:

- Financial transactions
- Document/version histories
- Sensitive user actions

✅ Use `FOR UPDATE` in services like:

- Wallet or banking operations
- Inventory stock updates
- Real-time bidding or ticketing