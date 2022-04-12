# p-dc-hivemind

steem hivemind

## requirements

> For a system with 16G of memory, here's a good start:

```txt
effective_cache_size = 12GB # 50-75% of avail memory
maintenance_work_mem = 2GB
random_page_cost = 1.0      # assuming SSD storage
shared_buffers = 4GB        # 25% of memory
work_mem = 512MB
synchronous_commit = off
checkpoint_completion_target = 0.9
checkpoint_timeout = 30min
max_wal_size = 4GB
```

## reference

- [hivemind 搭建教程](https://steemit.com/cn/@ety001/hivemind)
- [steemit : hivemind](https://github.com/steemit/hivemind)
