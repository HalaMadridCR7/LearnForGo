### goroutine

go语言中并发编程使用的是协程，协程比线程划分粒度更小的，是go语言的解释器自己调度的。

协程是执行在线程中的，如下图所示，多个协程可以在一个进程当中。当然，多个协程也可以分布在多个进程单中。

![协程](/Users/superwang/git/LearnForGo/协程.png)

go语言中并发操作实现是很简单的。只要使用 go 关键字加在方法前就好了。如下：

~~~go
func main(){
    go func(){
        fmt.Println(123)
    }
}
~~~

或者是

~~~go
func Println(){
    fmt.Println("xxx")
}

go Println()
~~~



go语言中的协程和线程调度方式是不一样的，他是有go语言解释器调度的，属于非抢占式，它的控制权并不是操作系统分配的，是自己交出去的。



但是在执行某些操作的时候会被被动的发生调度操作，如在执行fmt.Println()时，发生io操作，

这里列出goroutine可能的切换点（发生调度）如下：

1. I/0，select
2. channel
3. 等待锁
4. 函数调用 （有时）
5. runtime.Gosched() ) （会交出协程自己的控制权）

