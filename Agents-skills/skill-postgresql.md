---
name: skill-postgresql
description: Essential PostgreSQL & Supabase guide for developers. Focuses on schema design, JSONB, RLS, and common patterns.
---

# PostgreSQL & Supabase Developer Guide

This guide provides the most valuable PostgreSQL knowledge for building applications with Supabase or standalone PostgreSQL.

## 1. Schema Best Practices

### Data Types (Do's and Don'ts)
- ✅ **Use `TIMESTAMPTZ`**: Always include time zone. `TIMESTAMP` (without zone) leads to UTC confusion.
- ✅ **Use `TEXT`**: In Postgres, `TEXT` and `VARCHAR(n)` have no performance difference. Use `TEXT` unless you have a strict business length constraint.
- ✅ **Use `NUMERIC`**: For financial data and exact calculations. Avoid `FLOAT`/`REAL` for money.
- ✅ **Use `BIGINT GENERATED ALWAYS AS IDENTITY`**: Modern standard for primary keys. Safe, fast, and simple.
- ✅ **Use `snake_case`**: Postgres treats unquoted names as lowercase. `CamelCase` requires double quotes everywhere.

### Naming Conventions
- Tables: `users`, `orders` (plural)
- Primary Keys: `id` or `{table_name}_id`
- Timestamps: `created_at`, `updated_at`

---

## 2. Keys and Constraints

### Foreign Key Indexes
- **Rule**: Always create an index on every foreign key column.
- **Why**: Postgres does *not* index foreign keys automatically. Without an index, deletions or updates on parent tables can trigger full table scans or lock issues on the child table.

### Data Integrity
- **NOT NULL**: Apply to every column where data is required.
- **CHECK Constraints**: Use for logic validation at the DB level (e.g., `CHECK (price > 0)`, `CHECK (status IN ('draft', 'published'))`).

---

## 3. JSONB Mastery

JSONB is powerful for flexible data but requires correct indexing to be fast.

### Common Indexing Strategies
- **GIN Index (Default)**: Use for general "containment" queries.
  ```sql
  CREATE INDEX ON tbl USING GIN (metadata);
  -- Accelerates: metadata @> '{"status": "active"}'
  ```
- **Specific Field Indexing (B-tree)**: If you frequently filter by a specific scalar field inside JSONB, extract it into a functional index.
  ```sql
  CREATE INDEX ON tbl ((metadata->>'user_id'));
  ```

### When to use JSONB vs Columns
- Use **Columns** for: Data used in JOINs, mandatory data, or frequently filtered ranges.
- Use **JSONB** for: Optional attributes, varying metadata, or data you rarely query deep inside.

---

## 4. Upsert Pattern (The Developer's Swiss Army Knife)

Essential for data synchronization (e.g., importing from Google Sheets).

```sql
INSERT INTO target_table (id, val, updated_at)
VALUES (1, 'new_value', now())
ON CONFLICT (id) 
DO UPDATE SET 
  val = EXCLUDED.val,
  updated_at = EXCLUDED.updated_at
WHERE target_table.val IS DISTINCT FROM EXCLUDED.val;
```
*Tip: `IS DISTINCT FROM` prevents unnecessary writes if values are identical.*

---

## 5. Supabase & Row-Level Security (RLS)

RLS is your primary security layer in Supabase.

### Core Principles
1. **Enable RLS**: `ALTER TABLE users ENABLE ROW LEVEL SECURITY;`
2. **Use auth.uid()**: Link policies to the authenticated user.
   ```sql
   CREATE POLICY "Users can view their own data" 
   ON profiles FOR SELECT 
   USING (auth.uid() = id);
   ```
3. **Admin Access**: Use a separate schema or the `service_role` key ONLY in secure environments (backend/Edge Functions).

---

## 6. Performance Tips for Small/Medium Data

- **Avoid `SELECT *`**: Fetch only columns you need to reduce bandwidth and memory.
- **Explain Analyze**: Run `EXPLAIN ANALYZE <your query>` to see what the database is actually doing.
- **Indexes**: Don't overcompute. One index per frequent query pattern is enough.
- **Partial Indexes**: If you only query "active" items, use a partial index:
  ```sql
  CREATE INDEX ON orders (created_at) WHERE status = 'active';
  ```
