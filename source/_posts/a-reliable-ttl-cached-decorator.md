---
title: a reliable ttl_cached decorator
date: 2024-04-07 20:16:20
tags:
---

```python
import logging
import time
from functools import partial

logger = logging.getLogger(__name__)

def ttl_cached(ttl: int, f):
    _cache = None
    _time = time.time()

    def wrapper(*args, **kwargs):
        nonlocal _cache, _time
        if _cache is None:  # ensure first cache
            _cache = f(*args, **kwargs)
        elif time.time() - _time < ttl:
            logger.debug(f"cache hit: {f.__name__}")
        else:
            _time = time.time()
            try:
                _cache = f(*args, **kwargs)
            except Exception as e:  # avoid accidental exception, use cache
                logger.error(f"{f.__name__} error: {e}")
        return _cache

    return wrapper
```
