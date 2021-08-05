 # Garbage Collector


- ## 四个阶段
- ### 上次清理终止阶段（_GCoff）
1. 暂停程序，所有的处理器核心进入安全点
2. 若是因堆内存达到上次GC时的两倍（goenv GOGC设置）而致的强制清理，则要额外清理内存管理单元
- ### 标记阶段(_GCmark)
1. 切换状态至_GCmark，开启写屏障，用户程序助手（Mutator Assiste）将根对象入队（遍历队列）；
2. 将程序恢复执行，标记进程和用户程序助手开始并发标记内存中的对象，新创建的对象会被标记成黑色，写屏障会将覆盖到的指针及新指针标记为灰色；
3. 扫描根对象，包括Goroutine的栈、全局对象、不在堆中的运行时数据。扫描Goroutine栈时会暂停当前处理器核心；
4. 处理灰色队列中的对象，将对象标记成黑色并将他们的指向标记为灰色；
5. 通过分布式算法检查剩余的工作，在标记阶段完成后进入标记终止阶段
- ### 标记终止阶段(_GCmarktermination)
1. 暂停程序、将状态切换至_GCmarktermination，关闭辅助标记的用户程序助手
2. 清理处理器上的线程缓存
- ### 清理阶段(_GCoff)
1. 将状态切换至_GCoff，开始清理阶段，初始化清理状态，关闭写屏障
2. 恢复用户程序，所有新创建的对象会被标记成白色
3. 后台并发清理所有的内存管理单元，当Goroutine申请新的内存管理单元时会触发清理。