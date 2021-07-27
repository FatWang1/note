# ... 


- ... 是golang的语法糖，用来指代不定个数的参数
```golang
	func LoadYamlConfig(out interface{}, configFiles ...string)
```
如上即指 `configFiles` 的个数可以不为一，也可以用 `[]string` 做为入参。