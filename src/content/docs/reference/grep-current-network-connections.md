---
title: Grep connects by netstat
---

```
netstat -ant | grep tcp | tr -s ' ' ' ' | awk '{print $6}' | sort | uniq -c
```