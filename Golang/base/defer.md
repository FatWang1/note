# defer

- ## 在for循环中使用defer闭包
```golang
func main() {
	for i := 0; i < 3; i++ {
		defer func() { fmt.Println(i) }
	}
}
```
```shell
output:
3
3
3
```
在for循环中闭包执行3次，然而derfer只会在程序退出前执行，此时i=3，所以输出了三次3