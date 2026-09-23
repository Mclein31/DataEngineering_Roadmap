---
title: Python Data Wrangling Coding Bank
aliases:
  - Python Data Wrangling Coding Bank
---

# 🐍 Python Data Wrangling & Engineering Coding Bank

This problem bank contains 20 production-grade Python challenges focused on high-performance data processing, streaming generators, schema validation, and memory efficiency.

---

## 📋 Problem 1: Memory-Bounded Streaming CSV Parser with Custom Generators

### Problem Statement
Write a generator function `stream_large_csv(filepath: Path)` that streams a multi-gigabyte file line-by-line, yields validated batch dictionaries, and never uses more than 50MB of RAM.

### Production Solution
```python
import csv
from typing import Generator, Any
from pathlib import Path

def stream_large_csv(filepath: Path) -> Generator[dict[str, Any], None, None]:
    with filepath.open(mode="r", encoding="utf-8") as f:
        reader = csv.DictReader(f)
        for row in reader:
            yield {
                "transaction_id": row["txn_id"],
                "customer_id": int(row["customer_id"]),
                "amount": float(row["amount"]),
                "timestamp": row["timestamp"],
            }
```

---

## 📋 Problem 2: Resilient API Ingestion with Jittered Exponential Backoff

### Problem Statement
Implement an HTTP extraction client using `httpx` and `pydantic` that automatically handles rate limits (`HTTP 429`) and server errors (`HTTP 503`) with randomized exponential backoff.

### Production Solution
```python
import time
import random
import httpx
from pydantic import BaseModel, Field

class OrderPayload(BaseModel):
    order_id: str
    amount: float = Field(gt=0)
    customer_email: str

def fetch_with_backoff(url: str, max_retries: int = 3, base_delay: float = 1.0) -> list[OrderPayload]:
    headers = {"Accept": "application/json"}
    with httpx.Client(timeout=10.0) as client:
        for attempt in range(max_retries):
            try:
                response = client.get(url, headers=headers)
                if response.status_code == 200:
                    data = response.json()
                    return [OrderPayload.model_validate(item) for item in data]
                elif response.status_code in (429, 503):
                    jitter = random.uniform(0.1, 0.5)
                    sleep_time = (base_delay * (2 ** attempt)) + jitter
                    time.sleep(sleep_time)
                else:
                    response.raise_for_status()
            except (httpx.ConnectError, httpx.ReadTimeout):
                if attempt == max_retries - 1:
                    raise
                time.sleep(base_delay * (2 ** attempt))
    raise RuntimeError(f"Failed to fetch data from {url} after {max_retries} attempts.")
```

---

## 📋 Problem 3: High-Throughput Aggregations with Polars LazyFrames

### Problem Statement
Load a 10M row parquet dataset lazily, compute windowed 7-day rolling average spend per user, filter out users with less than 3 orders, and sink to partitioned Parquet without out-of-memory errors.

### Production Solution
```python
import polars as pl
from pathlib import Path

def aggregate_user_spend(input_path: Path, output_path: Path) -> None:
    lazy_plan = (
        pl.scan_parquet(str(input_path))
        .filter(pl.col("amount") > 0)
        .with_columns(
            pl.col("timestamp").str.to_datetime().alias("txn_time")
        )
        .sort(["user_id", "txn_time"])
        .with_columns(
            pl.col("amount").rolling_mean(window_size="7d", by="txn_time").over("user_id").alias("rolling_7d_spend"),
            pl.len().over("user_id").alias("total_orders")
        )
        .filter(pl.col("total_orders") >= 3)
    )
    
    lazy_plan.sink_parquet(str(output_path), compression="zstd")
```
