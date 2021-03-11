# Test&Benchmark


## test
1. 在Goland中，选中想要测试的函数，`control + shift + T`，即可自动生成测试函数
2. 在`// TODO: Add test cases.`的代码段中添加测试用例即可完成测试函数
3. 如果通过Goland直接执行报错可以尝试将要测试函数的目录设为 `Resoure Root`
4. 或者命令行执行
```bash
go test -v
```

## Benchmark
1. 在Test文件中创建名为`BenchmarkFuncname`的函数
2. 在循环中添加一个测试体
- 性能测试
```bash
go test -bench=. -benchmem
```
- 覆盖率测试
```bash
go test -cover
```