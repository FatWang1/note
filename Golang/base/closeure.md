# Closure



- ## 结构
```go
	func(i int) int {
		return i+1
	} (id)
```
其中 `i` 是闭包的形参，`id` 为实参。

- ## 理解
可以把闭包视为一种值类型(即 `func(... interface{}) ...interface{}` )，可以作为表达式的右值，也可以作为函数的返回值，如：
```go
	func Res() func(int) int {
        return func(i int) int {
            return i+1
        }
	}
```

- ## 注意事项
在并发执行闭包时，如果不指定实参，闭包会自动拿同名同类型的作为自己的实参，导致一些不必要的错误。如：
```go
	var wg sync.WaitGroup
	for i := 0; i <5; i++ {
		wg.Add(1)
		go func() {
			fmt.Println(i)
			wg.Done()
		}()
	}
	wg.Wait()
```
output:
```bash
2
5
5
5
5
```