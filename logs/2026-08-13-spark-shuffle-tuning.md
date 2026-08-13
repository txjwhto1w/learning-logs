# Spark Shuffle Tuning Notes

Date: 2026-08-13

## Problem
- Shuffle spill to disk on 200GB join job (cluster: 4 workers, 16GB each)
- High shuffle read/write metrics, stage retries

## Changes tried
- Increased `spark.sql.shuffle.partitions` from 200 to 400
- Set `spark.shuffle.file.buffer` to 64k (default 32k)
- Enabled `spark.shuffle.compress=true` (was already default)

## Result
- Shuffle spill reduced ~35%
- Job runtime 12m -> 8m
- CPU utilization improved, less GC pause

## Key takeaway
- For wide joins with skewed keys, also try `spark.sql.adaptive.skewJoin.enabled=true`
- Next: test with 600 partitions + AQE on