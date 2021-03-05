# Map

- 当Map的索引不存在时，Map的值为0，如下：
```golang
Pairs := map[byte]byte{
		')': '(',
		']': '[',
		'}': '{',
	}
fmt.Printf("%d", Pairs['('])
```
output：
```bash
0
```