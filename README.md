# Wallet Service

## Entity Relationship Diagram

```mermaid
erDiagram
    WALLET ||--o{ TRANSACTION : "1 wallet has many transactions"
    WALLET ||--o{ BALANCE_SNAPSHOT : "1 wallet has many snapshots"
    TRANSACTION ||--o{ AUDIT_LOG : "1 transaction generates a lot of audit logs"

    WALLET {
        string walletId PK
        BigDecimal balance
        BigDecimal blockedBalance
    }

    TRANSACTION {
        string transactionId PK
        string sourceWalletId FK
        string targetWalletId FK
        BigDecimal amount
        string type
        LocalDateTime timestamp
        string status
        string idempotencyKey
        string distributedTransactionId
    }

    BALANCE_SNAPSHOT {
        string snapshotId PK
        string walletId FK
        BigDecimal balance
        LocalDateTime timestamp
    }

    AUDIT_LOG {
        string logId PK
        string transactionId FK
        string walletId FK
        BigDecimal amount
        string type
        string status
        LocalDateTime timestamp
    }
```