# Global variable&local variable


- ## Global variable

- 作用域

	可以在整个包内被使用，包括包内各个函数

- 变量地址

	变量地址在`0x000000~0xffffff`之间，疑似不同作用域变量地址段不同
	
- ## Local variable

- 作用域
	
	仅在声明的函数内被使用，`func main(){}`内声明的变量也是局部变量
	
- 变量地址

	变量地址在`0x0000000000~0xffffffffff`之间

