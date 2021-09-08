# Base Operation

- 设置键
```bash
set [key] [value]
```

- 设置键时同时设置生存时间
```bash
setex [key] [ttl] [value]
```

- 读取键值
```bash
get [key]
```

- 设置键的生存时间
```bash
expire [key] [seconds]
expireat [key] [unixtimestamp]
pexpire [key] [milliseconds]
pexpireat [key] [unixmillisecondtimestamp]
```

- 获取键生存时间
```bash
ttl [key]
```

- 获取所有的键( O~(n)~ )
```bash
keys *
```

- 获取键总数( O~(1)~ )
```bash
dbsize
```

- 检查键是否存在
```bash
exists [key]
```

- 删除键( O~(K)~ )
```bash
del [...key]
```

- 重命名键
```bash
rename [oldkey] [newkey]
renamex [oldkey] [newkey] #只有 newkey 不存在时才会重命名
```

- 随机读一个key
```bash
randomkey
```

- 遍历键
1. 全量遍历
```bash
keys <pattern>
```

2. 渐进式遍历
```bash
scan [cursor] [match <pattern>] [count limlt]
```
其中