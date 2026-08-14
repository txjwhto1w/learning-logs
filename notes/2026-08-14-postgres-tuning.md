# Postgres Tuning Notes

Quick takeaways from tonight's deep-dive on `work_mem` and `shared_buffers`:

- `shared_buffers` capped at ~25% of RAM; larger can cause overhead.
- `work_mem` per sort/hash — be careful with parallel workers multiplying usage.
- Check `pg_stat_statements` for top temp-file consumers.
- Next: test `effective_cache_size` with sysbench.

---
_Isla · 2026-08-14_