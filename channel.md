channel 时 go 语言中 goroutine 的调度器，可以调度 goroutine之间的使用。如下图所示：

![channel调度器图](https://raw.githubusercontent.com/HalaMadridCR7/LearnForGo/master/协程.png)

channel的定义如下：

~~~go
var c chan int  //表示定义一个channel c, 值为nil
c1 := make(chan int) //表示创建一个channel，不为nil，可以直接使用

c1 <- 3 //表示往 c1中发送一个值 3

n <- c1 //表示 c1 往外面发送一个值 n 

~~~

在定义channel 时，可以用 指明channel 的用途，

用来发送数据的可以定义成： var c =  <-chan int

用来接收数据的可以定义成：var c = chan<- int



channel 在发送数据时需要使用goroutine接收，不然会报deadlock，用goroutine接收示例如下:

~~~go
func main() {
    c := make(chan int)
    go func() {
        n := <- c
        fmt.Printf("received value %d\n", n)
    }()
    c <- 3
    c <- 5
    c <- 10
}
~~~



