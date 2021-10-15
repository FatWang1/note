# Base Operation

## Key-Value Operation

### string

- 设置键
```ruby
set [key] [value] [nx|xx]
```

其中, `nx|xx` 为可选参数,
	 `nx` 用于添加(只有键不存在时才能设置成功)
	 `xx` 用于更新(只有键存在时才能设置成功)

- string 追加( O~(1)~ )
```ruby
append [key] [value]
```

- 获取 value (string) 长度
```ruby
strlen [key]
```

- 获取 key (string)长度
```ruby
strlen [key]
```

- 设置键时同时设置生存时间
```ruby
setex [key] [seconds] [value]
setpx [key] [milliseconds] [value]
```

- 批量设置键值( O~(K)~ )
```ruby
mset [key1] [value1] [key2] [value2] ...
```

- 读取键值( O~(1)~ )
```ruby
get [key]
```

- 批量获取键值( O~(K)~ )
```ruby
mget [key1] [key2] ...
```

- 设置并返回原值
```ruby
getset [key] [value]
```
*当key不存在时，可以执行成功，但不会返回值*

- 根据位置获取子串
```ruby
getrange [key] [strat] [end]
```

- 修改字符串自定位置的字符( O~(n)~ ), 返回设置后字符串长度
```ruby
setrange [key] [index] [char]
```
注意, `index` 不大于 `strlen [key]` , 当二者相等时,  即为在原 `value` 追加字符

- 设置键的生存时间
```ruby
expire [key] [seconds]
expireat [key] [unixtimestamp]
pexpire [key] [milliseconds]
pexpireat [key] [unixmillisecondtimestamp]
```

- 获取键生存时间
```ruby
ttl [key]
```

- 获取所有的键( O~(n)~ )
```ruby
keys *
```

- 获取键总数( O~(1)~ )
```ruby
dbsize
```

- 检查键是否存在
```ruby
exists [key]
```

- 删除键( O~(K)~ )
```ruby
del [...key]
```

- 重命名键
```ruby
rename [oldkey] [newkey]
renamex [oldkey] [newkey] #只有 newkey 不存在时才会重命名
```

- 随机读一个key
```ruby
randomkey
```

- 遍历键
1. 全量遍历
```ruby
keys <pattern>
```

2. 渐进式遍历( O~(1)~ )
```ruby
scan [ *cursor ] [match *<pattern>] [count *limlt ]
```
其中：
	`cursor` 是游标值, 第一次时为 0 , 之后为上次 `scan` 结果返回值的第一项
	`limit` 是 `redis` 单次遍历的字典槽位数量(约为)
例如：
```ruby
scan 0 match key99* count 1000
```
Output:
```ruby
1) "13912"
2)  1) "key997"
    2) "key9906"
    3) "key9957"
    4) "key9902"
    5) "key9971"
    6) "key9935"
    7) "key9958"
    8) "key9928"
    9) "key9931"
   10) "key9961"
   11) "key9948"
   12) "key9965"
   13) "key9937"
```
```ruby
scan 13912 match key99* count 1000
```
Output:
```ruby
1) "5292"
2)  1) "key996"
    2) "key9960"
    3) "key9973"
    4) "key9978"
    5) "key9927"
    6) "key995"
    7) "key9992"
    8) "key9993"
    9) "key9964"
   10) "key9934"
```

### hash

- 设置值
```ruby
hset [key] [field] [value]
```

- 获取值
```ruby
hget [key] [field]
```

- 删除 field 
```ruby
hdel [key] [...fields]
```

- 获取指定 key 的 field 总数
```ruby
hlen [key]
```

- 批量设置 field-value 
```ruby
hmset [key] [field1] [value] [field2] [value2] ...
```

- 批量获取 field-value
```ruby
hmget [key] [...fields]
```

- 判断 field 是否存在
```ruby
hexists [key] [field]
```

- 获取所有 field
```ruby
hkeys [key]
```

- 获取所有 value
```ruby
hvals [key]
```

- 获取所有的 field-value
```ruby
hgetall [key]
```

