# defer

- ## 在for循环中使用defer闭包
```golang
func main() {
	for i := 0; i < 3; i++ {
		defer func(i int) { fmt.Println(i) }(i)
	}
}
```
```shell
output:
2
1
0
```
在for循环中闭包执行3次，然而derfer只会在程序退出前执行，此时i=3，所以输出了三次3

