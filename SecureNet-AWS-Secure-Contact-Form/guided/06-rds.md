# RDS MySQL

RDS is private and listens on TCP 3306. Database: `securenet`; user: `admin`.

Table:

```sql
CREATE TABLE IF NOT EXISTS contact_messages (
  id BIGINT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(120) NOT NULL,
  email VARCHAR(255) NOT NULL,
  subject VARCHAR(255) NOT NULL,
  message TEXT NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Connect from an approved application/admin host:

```bash
mysql -h YOUR_RDS_ENDPOINT -P 3306 -u admin -p
```

RDS is private so the database is not directly exposed to the internet.
