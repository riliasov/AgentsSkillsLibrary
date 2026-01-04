---
name: skill-etl-pipeline
description: Data Engineering patterns, Pandas best practices, and ETL (Extract-Transform-Load) design.
---

# ETL & Data Engineering Specialist

This guide covers building reliable and maintainable data pipelines.

## 1. Pipeline Design (ETL / ELT)

### Principles
- **Idempotency**: Running the same script twice should not duplicate data or cause errors.
- **Incremental Loading**: Only process new or changed data since the last run.
- **Atomic Writes**: Ensure either all data is saved or none (use DB transactions).

### Monitoring & Logging
- Log counts: `extracted_rows`, `transformed_rows`, `loaded_rows`.
- Store "last sync" timestamps to track pipeline health.

---

## 2. Pandas Best Practices

Pandas is the primary tool for data transformation.

### Vectorization
- **Avoid `.iterrows()`**: It is extremely slow for large datasets.
- **Use Vectorized Functions**: Use `df['col'] * 0.5` instead of loops.
- **Mapping**: Use `.map()` or `.apply()` (carefully) for row-level logic.

### Memory & Performance
- **Types**: Use `category` for low-cardinality strings and `int32`/`float32` where appropriate.
- **Profiling**: Check memory usage with `df.info()`.

---

## 3. Database Ingestion (PostgreSQL)

### Strategies
- **UPSERT**: Handle existing records using `ON CONFLICT` (see `skill-postgresql.md`).
- **Batching**: Use `sqlalchemy` with `method='multi'` or `psycopg2.extras.execute_batch`.
- **Validation**: Validate schemas and data types before ingestion to avoid partial load failures.

### Tooling
- **Alchemy**: Use SQLAlchemy for ORM/Abstraction.
- **Pydantic**: Use for data validation and schema enforcement at the "Transform" stage.

---

## 4. Error Handling
- **Dead Letter Queue (DLQ)**: Save rows that failed transformation/validation to a separate file or table for later audit.
- **Retries**: Implement exponential backoff for network-related failures.
