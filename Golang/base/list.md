# List & Pointer

- 在 golang 中，list 是一种自定类型，可以被定义为：

```goalng
	type ListNode struct {
        Val  int
        Next *ListNode
	}
```

之前一直有一个疑问:

```golang
	type ListNode struct {
        Val  int
        Next *ListNode
    }

    func main() {
        a := &ListNode{
            Val:  1,
            Next: nil,
        }
        b := &ListNode{
            Val:  2,
            Next: a,
        }
        c := &ListNode{
            Val:  3,
            Next: b,
        }

        tmp := c
        fmt.Println(&tmp, &c)
    }

```
output：
```golang
	0xc000006030 0xc000006028
```
在链表( *ListNode )进行赋值时，明显 tmp c 两个变量的地址不同，那么想当然如果对 ( *ListNode )tmp.Next 进行操作，应该不会影响到 ( *ListNode )c 。

但事与愿违，

```golang
		tmp := c
        tmp.Next = a
        for tmp != nil && c != nil {
            fmt.Println(tmp.Val, "\t", c.Val)
            tmp = tmp.Next
            c = c.Next
        }
```
output：
```golang
	3 	 3
	1 	 1
```

显然，和我的猜想不符，那么就思考一下，赋值，应该是让两个变量的值相同，那么地址不同就可以理解了，同时 ( *ListNode )c 的  c.Next， 其实也是其值的一部分。理应 `c.Next == tmp.Next` 。

```golang
		tmp := c
        tmp.Next = a
        fmt.Println(&c.Next,"\t",&tmp.Next)
```
output：
```golang
	0xc00004c268 	 0xc00004c268
```

- ## 结语

	在 golang 中，指针类型的变量赋值是将值 copy 一份，如果赋与的值是结构体包括指针的话，指针可以被认为是值， copy 过去。

