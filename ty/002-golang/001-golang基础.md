

# `for && range`

>#### `for range`循环遍历数组或者切片
>
>在遍历数组或者切片的时候 是拷贝一份数组进行遍历 ， 所以在原数组上操作并不影响遍历原数组
>
>`for`循环两道案例题
>
>```go
>func main() {
>	arr := []int{1, 2, 3}
>	for _, v := range arr {
>		arr = append(arr, v)
>	}
>	fmt.Println(arr)
>}
>输出： 1 2 3 1 2 3 
>```
>
>原因： 对于所有的 `range` 循环，`Go `语言都会在编译期间将原切片或者数组赋值给一个新的变量 `ha`，在赋值的过程中其实就发生了拷贝，所以我们遍历的切片其实已经不是原有的切片变量了。
>
>-----
>
>```go
>func main() {
>	arr := []int{1, 2, 3}
>	newArr := []*int{}
>	for _, v := range arr {
>		newArr = append(newArr, &v)  //原想拷贝
>	}
>	for _, v := range newArr {
>		fmt.Println(*v)
>	}
>}
>
>$ go run main.go
>3 3 3
>```
>
>总结： 而遇到这种同时遍历索引和元素的 range 循环时，Go 语言会额外创建一个新的 `v2` 变量存储切片中的元素，**循环中使用的这个变量 v2 会在每一次迭代被重新赋值而覆盖，赋值时也会触发拷贝**。   如何取到每个元素地址呢 `for i,_:range arr{ append(&arr[i])}` 这种形式
>
>-----
>
>
>
>#### `for range 遍历 map `
>
>在遍历`map`的时候拷贝的副本是指针  所以遍历的过程中修改 也会影响到原`map`
>
>```go
>func main() {
>	m := make(map[int]int)
>	m[1] = 1
>	key := 2
>	for k, v := range m {
>		fmt.Println(k, v)
>		m[key] = key
>		key++
>	}
>	fmt.Println(m)
>}
>map[1:1 2:2 3:3 4:4 5:5 6:6 7:7 8:8 9:9]
>```
>
>这种打印结果就是随机的  随机的原因猜测就是在`map`这种数据结构的原因，在遍历桶的时候可能遍历完了猜测





# `append && delete`

>#### `append`两个案例题
>
>```go
>func test() {
>	x := make([]int, 0, 3)   
>	x  = append(x, 1)				x=[1]
>	y := append(x, 8, 9)	  y=[1,8,9] x=[1]
>	z := append(x, 1)				z=[1,1]   x=[1]  y=[1,1,9]
>	fmt.Println(x)
>	fmt.Println(y)
>	fmt.Println(z)
>}
>
>[1]
>[1 1 9]
>[1 1]
>```
>
>**总结： append 追加操作没有发生扩容。所有操作还是基于源数组上进行操作。 只是每一个变量内部维护自己的`len cap` 切片实质上就是一个结构体，内部指向数组的指针在上述操作都是一样的。**
>
>-----
>
>```go
>func test() {
>   x := make([]int, 0, 3)
>   x = append(x, 1)							x=[1]
>   y := append(x, 8, 9)					y=[1,8,9]
>   z := append(x, 1,1,1,1,1,)	  z=[1,1,1,1,1,1]  这是一个新的slice 所以初始化容量在这里就是至关重要呗
>   fmt.Println(x)
>   fmt.Println(y)
>   fmt.Println(z)
>}
>
>[1]
>[1 8 9]
>[1 1 1 1 1 1]
>```
>
>**总结： append追加发生扩容， 原有的数据结构不改变， 而是在新的slice上进行追加扩容呗 ** 
>
>------
>
>#### append的时候发生扩容的动作
>
>- append单个元素，或者append少量的多个元素，这里的少量指double之后的容量能容纳，这样就会走以下扩容流程，不足1024，双倍扩容，超过1024的，1.25倍扩容。
>- 若是append多个元素，且double后的容量不能容纳，直接使用预估的容量。并且需要考虑内存对其的特性。
>
>-----
>
>#### append追加切片的几种方式
>
>```go
>var a []int
>a = append(a, 1) // 追加1个元素
>a = append(a, 1, 2, 3) // 追加多个元素, 手写解包方式
>a = append(a, []int{1,2,3}...) // 追加一个切片, 切片需要解包
>```











# `defer`

>`Go` 语言的 `defer` 会在当前函数返回前执行传入的函数，它会经常被用于**关闭文件描述符、关闭数据库连接以及解锁资源**。
>
>----
>
>在运行期间获取`runtime._defer`j结构体 它都会被追加到所在 `Goroutine _defer` 链表的最前面。 
>
>![golang-new-defer](https://img.draveness.me/2020-01-19-15794017184614-golang-new-defer.png)
>
>`defer` 关键字的插入顺序是链表头插， 而 `defer` 关键字执行是从前向后的，这也是为什么后调用的 `defer` 会优先执行。



# `panic && recover`

>`panic`:  类似于`java`中`throw` 手动抛出异常     `panic("error")`
>
>`recover:`类似于`java`中`try catch`  但是作用域必须是在**`defer 关键字之后`**， 其他作用域下是不生效的。
>
>```go
>defer func(){
>  if err:=recover; err!=nil{
>     deal err
>  }
>}()
>```





# ==-- 数组 && 切片 && hmap && chan --==



# `array`

>#### **1. 数组的创建方式：**    数组是值传递
>
>```go
>arr1 := [3]int{1, 2, 3}
>arr2 := [...]int{1, 2, 3}
>```
>
>显示指定数组长度和类型
>
>隐士指定数组长度和类型   在编译期间 会对该类型进行推导呗  
>
>```go
>package types 
>func NewArray(elem *Type, bound int64) *Type {  
>	if bound < 0 {
>		Fatalf("NewArray: invalid bound %v", bound)
>	}
>	t := New(TARRAY)
>	t.Extra = &Array{Elem: elem, Bound: bound}
>	t.SetNotInHeap(elem.NotInHeap())
>	return t
>}
>```
>
>上述是在源码当中显示指定创建数组的方式呗
>
>-------
>
>#### 2. 数组创建 编译器优化
>
>1. 当元素数量小于或者等于 4 个时，会直接将数组中的元素放置在栈上；
>2. 当元素数量大于 4 个时，会将数组中的元素放置到静态区并在运行时取出；
>
>总结起来，在不考虑逃逸分析的情况下，如果数组中元素的个数小于或者等于 4 个，那么所有的变量会直接在栈上初始化，如果数组元素大于 4 个，变量就会在静态存储区初始化然后拷贝到栈上，代码进入中间代码的机器码二个部门，最后生成可以执行的二进制文件。







# `slice`

>#### 1. slice创建方式
>
>切片数据结构
>
>```go
>type SliceHeader struct {
>	Data uintptr				Data 是指向数组的指针;  这里边为什么不是unsafe.point 是为了保证指针安全呗
>	Len  int				   	Len  是当前切片的长度；
>	Cap  int				  	Cap  是当前切片的容量，即 Data 数组的大小：
>}   
>```
>
>三种创建方式 推荐Make初始化创建
>
>```go
>arr[0:3] or slice[0:3]       //编译期间确定
>slice := []int{1, 2, 3}		   //编译期间就是确定了呢
>slice := make([]int, 10)     //运行确定 make初始化的时候 需要指定长度 容量可以不指定 如果([]int ,6,10) len=6 会默认初始化6个0 
>```
>
>make创建切片的源码函数
>
>```go
>func makeslice(et *_type, len, cap int) unsafe.Pointer {
>	mem, overflow := math.MulUintptr(et.size, uintptr(cap))
>	if overflow || mem > maxAlloc || len < 0 || len > cap {
>		mem, overflow := math.MulUintptr(et.size, uintptr(len))
>		if overflow || mem > maxAlloc || len < 0 {
>			panicmakeslicelen()
>		}
>		panicmakeslicecap()
>	}
>
>	return mallocgc(mem, et, true)
>}
>```
>
>上述函数的主要工作是计算切片占用的内存空间并在堆上申请一片连续的内存，它使用如下的方式计算占用的内存：
>
>​												**内存空间=片中元素大小×切片容量**
>
>虽然编译期间可以检查出很多错误，但是在创建切片的过程中如果发生了以下错误会直接触发运行时错误并崩溃：
>
>1. 内存空间的大小发生了溢出；
>2. 申请的内存大于最大可分配的内存；
>3. 传入的长度小于 0 或者长度大于容量；
>
>------
>
>#### 2. 追加和扩容 详细见append函数





# `map`

>在`go`里边解决`hash`冲突的是拉链地址法  就是跟java `hashmap`跟类似
>
>#### 1. 创建、put、get操作
>
>​         `Go` 语言使用拉链法来解决哈希碰撞的问题实现了哈希表，它的访问、写入和删除等操作都在编译期间转换成了运行时的函数或者方法。哈希在每一个桶中存储键对应哈希的前 8 位，当对哈希进行操作时，这些 `tophash` 就成为可以帮助哈希快速遍历桶中元素的缓存。哈希表的每个桶都只能存储 8 个键值对，**一旦当前哈希的某个桶超出 8 个，新的键值对就会存储到哈希的溢出桶**中。随着键值对数量的增加，溢出桶的数量和哈希的装载因子也会逐渐升高，超过一定范围就会触发扩容，扩容会将桶的数量翻倍，元素再分配的过程也是在调用写操作时增量进行的，不会造成性能的瞬时巨大抖动。
>
>
>
>#### 2. delete 删除
>
>```go
>func delete(m map[Type]Type1, key Type)
>```



# `string`

>####  1.string 数据结构
>
>```go
>type StringHeader struct {
>	Data uintptr     			 // 指向字节数组的指针   
>	Len  int
>}
>```
>
>字符串在GO里边就是类似于只读的字节切片。 其余操作会返回一个新的	`string。 `  `string`是以`UTF-8`编码的,而`UTF-8`是一种1-4字节的可变长字符集，每个字符可用`1-4`字节 来表示`
>
>----
>
>#### 2.`for range `遍历`string`
>
>概念理解：
>
>- **UTF-8**       **UTF-8是一种字符编码规范，一个字符的长度不固定，可以用1-4个字节来表示**
>- **Unicode**  **用“U+”随后紧接着4个数字来表示一个字符。**
>- **rune**       **`type rune = int32`    rune4个字节**
>- **byte**       **`type byte = uint8`   uint8别名呗**
>
>
>
>三种遍历方式：
>
>1. `for` 遍历是遍历字节数组 返回是一个 `utf-8` 编码对应的字符 如果存在中文字符乱码
>2. `for range:`    遍历 `rune` 类型的字符  采取`for range`方式比较好
>3. `[]rune()` :      将字符串转为 Unicode 码点再进行截取
>
>------
>
>`String`  就是类似于`java`中的`string `
>
> Strings.Builder  就是类似于java里边stringBuilder     这种形式字符串拼接就是不是比较耗时间呗 在这里哈呢

# ==-- 并发编程 --==



# `sync` 

## `Mutex`

>#### 1.`Mutex`基础数据结构
>
>Go 语言的`sync.mutex`由两个字段 `state` 和 `sema` 组成。其中 `state` 表示当前互斥锁的状态，而 `sema` 是用于控制锁状态的信号量。
>
>```go
>type Mutex struct {
>	state int32
>	sema  uint32
>}
>```
>
>上述两个加起来只占 8 字节空间的结构体表示了` Go` 语言中的互斥锁。
>
>互斥锁的状态比较复杂，如下图所示，最低三位分别表示 `mutexLocked`、`mutexWoken` 和 `mutexStarving`，剩下的位置用来表示当前有多少个 `Goroutine` 在等待互斥锁的释放：
>
>![golang-mutex-state](https://img.draveness.me/2020-01-23-15797104328010-golang-mutex-state.png)
>
>**图 6-6 互斥锁的状态**
>
>在默认情况下，互斥锁的所有状态位都是 0，`int32` 中的不同位分别表示了不同的状态：
>
>- `mutexLocked` — 表示互斥锁的锁定状态；
>- `mutexWoken` — 表示从正常模式被从唤醒；
>- `mutexStarving` — 当前的互斥锁进入饥饿状态；
>- `waitersCount` — 当前互斥锁上等待的 `Goroutine` 个数；
>
>-----
>
>#### 2. 正常模式和饥饿模式转换条件
>
>**正常模式--->饥饿模式**：在正常模式下，锁的等待者会按照先进先出的顺序获取锁。但是刚被唤起的 `Goroutine` 与新创建的 `Goroutine` 竞争时，大概率会获取不到锁，为了减少这种情况的出现，一旦 `Goroutine `超过 `1ms` 没有获取到锁，它就会将当前互斥锁切换饥饿模式，防止部分 `Goroutine `被**『饿死』**。
>
>----
>
>**饥饿模式--->正常模式**：在饥饿模式中，互斥锁会直接交给等待队列最前面的·`Goroutine`。新的 `Goroutine` 在该状态下不能获取锁、也不会进入自旋状态，它们只会在队列的末尾等待。如果一个 `Goroutine` 获得了互斥锁并且它在队列的末尾或者它等待的时间少于 `1ms`，那么当前的互斥锁就会切换回正常模式。
>
>与饥饿模式相比，正常模式下的互斥锁能够提供更好地性能，饥饿模式的能避免` Goroutine` 由于陷入等待无法获取锁而造成的高尾延时。
>
>
>
>#### 3. `lock`上锁过程
>
>1. 如果`state lock`标志位为0 则`cas`改变标志位进行上锁
>2. 如果`state lock`标志位为1 ， 会判断是否进行自旋状态：能够进行自旋状态的条件也非常严格
>3. 如果自旋没有获取到锁，或者自旋条件不成立， 会重新计算一下锁的最新状态，并通过信号量的机制来获取锁
>
>```go
>func (m *Mutex) Lock() {
>	if atomic.CompareAndSwapInt32(&m.state, 0, mutexLocked) {    //cas 将锁的标志位置1 
>		return
>	}
>	m.lockSlow()   //如果锁的状态不是0 通过自旋等方式来等待锁的释放
>}
>```
>
>**如果当前锁的状态不是0  会进入到自旋等状态 进入`m.lockSlow`方法**
>
>```go
>func (m *Mutex) lockSlow() {
>	var waitStartTime int64
>	starving := false
>	awoke := false
>	iter := 0
>	old := m.state
>	for {
>		if old&(mutexLocked|mutexStarving) == mutexLocked && runtime_canSpin(iter) { //runtime_canSpin(iter) 返回true
>			if !awoke && old&mutexWoken == 0 && old>>mutexWaiterShift != 0 &&
>				atomic.CompareAndSwapInt32(&m.state, old, old|mutexWoken) {
>				awoke = true
>			}
>			runtime_doSpin()    //调用自旋 执行30次push指令
>			iter++
>			old = m.state
>			continue
>		}
>    ...//计算锁的最新状态
>    if atomic.CompareAndSwapInt32(&m.state, old, new) {
>			if old&(mutexLocked|mutexStarving) == 0 {
>				break // locked the mutex with CAS  通过CAS函数获取到锁
>			}
>			// If we were already waiting before, queue at the front of the queue.
>			queueLifo := waitStartTime != 0
>			if waitStartTime == 0 {
>				waitStartTime = runtime_nanotime()
>			}
>			runtime_SemacquireMutex(&m.sema, queueLifo, 1)  //没获取到锁 通过信号量保证资源不会被两个 Goroutine 获取
>      							  	//在方法中不断尝试获取锁并陷入休眠等待信号量的释放，一旦当前 Goroutine 可以获取信号量，它就会立刻返回，
>```
>
>1. 判断当前 Goroutine 能否进入自旋；  **互斥锁只有正常模式下、`canSpin`判断是否运行在多核`cpu`、自旋次数小于4次、当前机器上至少存在一个正在运行的处理器 P 并且处理的运行队列为空；** 只有当前条件都成立才会进行自旋。
>2. 通过自旋等待互斥锁的释放；
>3. 计算互斥锁的最新状态；
>4. 更新互斥锁的状态并获取锁；
>
>如果没有通过自旋获取到锁，会`runtime_SemacquireMutex(&m.sema, queueLifo, 1)`会在方法中不断尝试获取锁并陷入休眠等待信号量的释放，一旦当前 `Goroutine` 可以获取信号量，它就会立刻返回，`lock()`方法剩余代码也会继续执行。
>
>- 在正常模式下，上述代码会设置唤醒和饥饿标记、重置迭代次数并重新执行获取锁的循环；
>- 在饥饿模式下，当前 `Goroutine` 会获得互斥锁，如果等待队列中只存在当前 `Goroutine`，互斥锁还会从饥饿模式中退出；
>
>#### 4. `unlock`释放锁过程
>
>1. 利用`atomic.AddInt32`-1操作 进行快速解锁 如果返回值为0 解锁成功  如果返回值不为0 则进行慢解锁状态
>2. 
>
>```go
>func (m *Mutex) Unlock() {
>	new := atomic.AddInt32(&m.state, -mutexLocked) 
>	if new != 0 {
>		m.unlockSlow(new)
>	}
>}
>```
>
>进入慢速解锁状态函数
>
>```go
>func (m *Mutex) unlockSlow(new int32) {
>	if (new+mutexLocked)&mutexLocked == 0 {		  //如果是已经解锁 会抛出异常 
>		throw("sync: unlock of unlocked mutex")
>	}
>	if new&mutexStarving == 0 { // 正常模式
>		old := new
>		for {
>			if old>>mutexWaiterShift == 0 || old&(mutexLocked|mutexWoken|mutexStarving) != 0 {
>				return
>			}
>			new = (old - 1<<mutexWaiterShift) | mutexWoken
>			if atomic.CompareAndSwapInt32(&m.state, old, new) {
>				runtime_Semrelease(&m.sema, false, 1)
>				return
>			}
>			old = m.state
>		}
>	} else { // 饥饿模式
>		runtime_Semrelease(&m.sema, true, 1)
>	}
>}
>```
>
>**正常模式下：** 果互斥锁不存在等待者或者互斥锁的 `mutexLocked`、`mutexStarving`、`mutexWoken` 状态不都为 0，那么当前方法可以直接返回，不需要唤醒其他等待者；如果互斥锁存在等待者，会通过`runtime_Semrelease` 唤醒等待者并移交锁的所有权；
>
>**饥饿模式下：**直接调用`runme_Semrelease`将当前锁交给下一个正在尝试获取锁的等待者，等待者被唤醒后会得到锁，在这时互斥锁还不会退出饥饿状态；

## ` RWMutex `

>读写锁是一种锁粒度更低的读写锁， 他不限制资源的并发读， **但是读写、写写 无法并行执行**
>
>#### 1. 基本数据结构
>
>`RWMutex`中总共包含以下 5 个字段：
>
>```go
>type RWMutex struct {
>	w           Mutex
>	writerSem   uint32
>	readerSem   uint32
>	readerCount int32
>	readerWait  int32
>}
>```
>
>- `w` — 复用互斥锁提供的能力；
>- `writerSem` 和 `readerSem` — 分别用于写等待读和读等待写：
>- `readerCount` 存储了当前正在执行的读操作数量；
>- `readerWait` 表示当写操作被阻塞时等待的读操作个数；
>
>我们会依次分析获取写锁和读锁的实现原理，其中：
>
>- 写操作使用 `rw.lock`和`rw.unlock`；
>- 读操作使用`rw.RLock 和 rw.RUnlock`
>
>-------
>
>读锁过程和写锁过程操作见 https://draveness.me/golang/docs/part3-runtime/ch06-concurrency/golang-sync-primitives/





## `Cond`

>它可以让一组的 Goroutine 都在满足特定条件时被唤醒。 相当于`java ` 里边`wait Notify AllNotify` ->对应`go`里边 `wait singal brodcast`
>
>初始化
>
>```go
>cond:=sync.NewCond(&sync.Mutex{})   返回是一个指针类型呗
>```
>
>- [`sync.Cond.Wait`](https://draveness.me/golang/tree/sync.Cond.Wait) 在调用之前一定要使用获取互斥锁，否则会触发程序崩溃；
>- [`sync.Cond.Signal`](https://draveness.me/golang/tree/sync.Cond.Signal) 唤醒的 Goroutine 都是队列最前面、等待最久的` Goroutine`；  队列在源码里边大部分是采用链表结构
>- [`sync.Cond.Broadcast`](https://draveness.me/golang/tree/sync.Cond.Broadcast) 会按照一定顺序广播通知等待的全部 `Goroutine`；





## `WaitGroup`

>`sync.WaitGroup` 可以等待一组 `Goroutine` 的返回，一个比较常见的使用场景是批量发出 `RPC` 或者 `HTTP` 请求：
>
>```go
>requests := []*Request{...}
>wg := &sync.WaitGroup{}
>wg.Add(len(requests))
>
>for _, request := range requests {
>    go func(r *Request) {
>        defer wg.Done()
>        // res, err := service.call(r)
>    }(request)
>}
>wg.Wait()
>```
>
>这种形式就是批量处理`http` 请求呗
>
>-----
>
>#### 1.基本数据结构
>
>```go
>type WaitGroup struct {
>	noCopy noCopy
>	state1 [3]uint32
>}
>```
>
>- `noCopy` — 保证 [`sync.WaitGroup`](https://draveness.me/golang/tree/sync.WaitGroup) 不会被开发者通过再赋值的方式拷贝； 所以不能对`waitGroup`进行拷贝  
>- `state1` — 存储着状态和信号量
>
>每个sync内部都是维护一个值 内部维护着一个计数，此计数的初始值默认就是为0
>
>`Add`： 等待计数组+1
>
>`Done`:  内部还是调用`Add` 进行-1 
>
>`Wait`:  当等待组计数器内部计数器为0 如果为0 `wait`就是一个空操作。 如果不为0 将会阻塞当前协程 （一般我们在`main`主协程中进行调用`wait`方法）



## `Once`

>函数只执行一次  相当于单例模式呗 在这里哈呢
>
>```go
>type Once struct {
>	done uint32     //保持只执行一次 就是在这里uint32变量上
>	m    Mutex
>}
>```
>
>`sync.Once.Do()`该方法会接收一个入参为空的函数：
>
>```go
>func (o *Once) Do(f func()) {          	 //Once Do 传入空参方法 
>	if atomic.LoadUint32(&o.done) == 0 {    //变量 done==0 才会进入方法调用  ==1会直接返回呗
>		o.doSlow(f)
>	}
>}
>
>func (o *Once) doSlow(f func()) {
>	o.m.Lock()
>	defer o.m.Unlock()
>	if o.done == 0 {
>		defer atomic.StoreUint32(&o.done, 1)   //如果执行一次 就将 done 变量置为1 
>		f()
>	}
>}
>```

## `sync.map`

>并发安全的Map  在这里就是设计理念  看看如何 会不会哈呢  
>
>
>
>根据上述的压测结果，我们可以得出 `sync.Map` 类型：
>
>- 在读和删场景上的性能是最佳的，领先一倍有多。
>- 在写入场景上的性能非常差，落后原生 map+锁整整有一倍之多。
>
>因此在实际的业务场景中。假设是读多写少的场景，会更建议使用 `sync.Map` 类型。
>
>但若是那种写多的场景，例如多 goroutine 批量的循环写入，那就建议另辟途径了，性能不忍直视（无性能要求另当别论）。
>
>-----------
>
>其实 `sync.map`内部 是存在两个`map` 一个是`read 还有就是 dirty`  
>
>```go
>type Map struct {
>    // 保护dirty的锁
>    mu Mutex                        
>    // 只读数据（修改采用原子操作)
>    read atomic.Value                
>    // 包含只读中所有数据（冗余），写入新数据时也在dirty中操作
>    dirty map[interface{}]*entry  
>    // 当原子操作访问只读read时找不到数据时会去dirty中寻找，此时misses+1，dirty及作为存储新写入的数据，又冗余了只读结构中的数        据，所以当misses > dirty 的长度时， 会将dirty升级为read，同时将老的dirty置nil
>    misses int 
>}
>```

​    

# ` channel`

## 线程和协程和进程

>多进程的程序要比多线程的程序健壮，但在进程切换时，耗费资源较大，效率要差一些
>
>- **一个线程只能属于一个进程，而一个进程可以有多个线程，但至少有一个线程**；
>- 资源分配给进程，同一进程的所有线程共享该进程的所有资源；
>- 处理机分给线程，即**真正在处理机上运行的是线程**；
>- 线程在执行过程中，需要协作同步。不同进程的线程间要利用消息通信的办法实现同步。
>-  
>- [协程](https://so.csdn.net/so/search?q=协程&spm=1001.2101.3001.7020)，是一种比线程更加轻量级的存在，协程不是被操作系统内核所管理，而完全是由程序所控制（也就是在用户态执行）。这样带来的好处就是性能得到了很大的提升，不会像线程切换那样消耗资源。
>- **协程在子程序内部是可中断的，然后转而执行别的子程序，在适当的时候再返回来接着执行**。
>- 协程的特点在于是一个线程执行
>- 极高的执行效率：因为子程序切换不是线程切换，而是由程序自身控制，因此，没有线程切换的开销，和[多线程](https://so.csdn.net/so/search?q=多线程&spm=1001.2101.3001.7020)比，线程数量越多，协程的性能优势就越明显；





## `channel `设计理念

>**GO设计模式： 不要通过共享内存的方式进行通信(`sync.mutex`)， 而是应该通过通信的方式来共享内存。**
>
><img src="https://img.draveness.me/2020-01-28-15802171487080-channel-and-goroutines.png" alt="channel-and-goroutines" style="zoom:50%;" />
>
>#### 1.基本数据结构
>
>Go 语言的` Channel` 在运行时使用 [`runtime.hchan`]结构体表示。我们在 Go 语言中创建新的 `Channel `时，实际上创建的都是如下所示的结构：
>
>```go
>type hchan struct {
>	qcount   uint
>	dataqsiz uint
>	buf      unsafe.Pointer
>	elemsize uint16
>	closed   uint32
>	elemtype *_type
>	sendx    uint
>	recvx    uint
>	recvq    waitq
>	sendq    waitq
>	lock mutex
>}
>```
>
>Go
>
>[`runtime.hchan`]结构体中的五个字段 `qcount`、`dataqsiz`、`buf`、`sendx`、`recv` 构建底层的循环队列：
>
>- `qcount` — Channel 中的元素个数；
>- `dataqsiz` — Channel 中的循环队列的长度；
>- `buf` — Channel 的缓冲区数据指针；
>- `sendx` — Channel 的发送操作处理到的位置；
>- `recvx` — Channel 的接收操作处理到的位置；
>
>`sendq` 和 `recvq` 存储了当前 `Channel` 由于缓冲区空间不足而阻塞的` Goroutine` 列表，这些等待队列使用双向链表 [`runtime.waitq`]表示，链表中所有的元素都是 [`runtime.sudog`]结构：
>
>```go
>type waitq struct {
>	first *sudog
>	last  *sudog
>}
>```



## `channel `中的坑

>1. 关闭未初始化 channel 会产生 panic
>2. 重复关闭 channel 产生 panic
>3. 向已关闭 channel 中发送会产生 panic
>4. 从已关闭的 channel 读取不会 panic，能读出 channel 未被读取的，若消息均已读出则会读到类型的零值。从已关闭的 channel 中读取不会阻塞，会返回一个为 false 的 ok-idiom（判断 channel 是否关闭）
>5. 关闭 channel 产生广播机制，所有读取channel的 goroutine 都会收到消息



#  `goroutine `  &&  `GPM` 调度器

>G：=`goroutine`
>
>M：=`线程`
>
>P：=队列
>
>----
>
>1. 程序一开始怎么创建P的 
>2. G怎么跟P进行绑定的
>3. M是如何拿取P中的队列里边的任务进行执行的
>4. 如果G阻塞 M和P是如何处理的
>5. GMP如果有多个p，有什么影响
>6. GMP相比于GM有什么优势
>7. P和M的数量可以无限扩张么
>8. P和M是在程序运行时就是创建好了么
>9. G在GMP模型中的流动过程
>10. 你有没有想过队列和线程的优化可以做在G层和M层，为什么要加一个P层呢？
>
>https://blog.csdn.net/slphahaha/article/details/119584039    就是相当于GMP的深挖心路历程

## goroutine  GPM 模型

>https://tonybai.com/2017/06/23/an-intro-about-goroutine-scheduler/    这里边就是简单介绍goroutine 调度器
>
>https://blog.csdn.net/dream_1996/article/details/118051217 
>
>问题：
>
>1. 程序一开始怎么创建P的 
>2. G怎么跟P进行绑定的
>3. M是如何拿取P中的队列里边的任务进行执行的
>
><img src="https://img-blog.csdnimg.cn/20210619121109386.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RyZWFtXzE5OTY=,size_16,color_FFFFFF,t_70" alt="img" style="zoom:67%;" />
>
>1. G — 表示 Goroutine，它是一个待执行的任务；
>2. M — 表示操作系统的线程，它由操作系统的调度器调度和管理；
>3. P — 表示处理器，它可以被看做运行在线程上的本地调度器；
>
>**全局队列：该队列存储的 G 将被所有的 M 全局共享，为保证数据竞争问题，需加锁处理。**
>
>“当线程处于阻塞状态后，如果其他线程都处于running状态, 这个时候是不是会创建一个新的线程来运行当前处理器P队列中的Gorountine, 如果是这样，那多出来的线程以后会怎么处理？   但是 Go 语言在启动线程时会设置 `PTHREAD_CREATE_DETACHED`，当线程执行完成后会自动回收和重用。
>
>![img](https://img-blog.csdnimg.cn/20210619140252156.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2RyZWFtXzE5OTY=,size_16,color_FFFFFF,t_70)
>
>1. 我们通过 go func()来创建一个goroutine
>2. 有两个存储G的队列，一个是局部调度器P的本地队列、一个是全局G队列。新创建的G会先保存在P的本地队列中，如果P的本地队列已经满了就会保存在全局的队列中
>3. G只能运行在M中，一个M必须持有一个P，M与P是1：1的关系。M会从P的本地队列弹出一个可执行状态的G来执行，如果P的本地队列为空，就会向其他的MP组合偷取一个可执行的G来执行
>4. 当M执行某一个G时候如果发生了syscall或则其余阻塞操作，M会阻塞，如果当前有一些G在执行，runtime会把这个线程M从P中摘除(detach)，然后再创建一个新的操作系统的线程(如果有空闲的线程可用就复用空闲线程)来服务于这个P
>5. 当M系统调用结束时候，这个G会尝试获取一个空闲的P执行，并放入到这个P的本地队列。如果获取不到P，那么这个线程M变成休眠状态， 加入到空闲线程中，然后这个G会被放入全局队列中



# `context`

>上下文`context.Context` 是`Go` 语言中用来设置取消`groutine`、截止日期、同步信号，传递请求相关值的结构体。上下文与 `Goroutine `有比较密切的关系
>
>**`context`的由来**： 在开启一个`goroutine` 我们是无法控制其结束， 所以我们采用`select + chan`方式来控制`goroutine`结束，但是当前`goroutine`可能就是存在子协程，可能需要多个`select+chan`程序也不够美观。 所以才使用`context` 这种上下文来进行取消控制。
>
>-----
>
>#### 1. 首先`select + chan` 模式来控制`goroutine`停止呗
>
>```go
>func main() {
>   stop := make(chan bool)
>   go func() {
>      for {
>         select {
>         case <-stop: //这里边如果就是读取到stop的值呗 我们就是进行一下操作呗 在这里哈呢
>            fmt.Println("退出当前goroutine 停止后台运行")
>            return //这里边就是必须要执行return呗 
>         default:
>            fmt.Println("继续执行任务")
>            time.Sleep(2 * time.Second)
>         }
>      }
>   }()
>   time.Sleep(10 * time.Second)
>   fmt.Println("停止后台goroutine 运行")
>   stop <- true
>   time.Sleep(10 * time.Second)
>}
>```
>
>-----
>
>#### 2. 使用`context + select`来停止`goroutine`
>
>```go
>func main() {
>	//context.Background() 这里边就是顶层context  下边对应的功能都是基于子节点context来使用的呗
>	ctx, cancel := context.WithCancel(context.Background())
>	go dealTask(ctx,"1号")
>	go dealTask(ctx,"2号")
>	go dealTask(ctx,"3号")
>	time.Sleep(10 * time.Second)
>	fmt.Println("通知当前context 去执行取消 goroutine")
>	cancel()
>	time.Sleep(5 * time.Second)
>}
>func dealTask(ctx context.Context, name string) {
>	for true {
>		select {
>		case <-ctx.Done():
>			fmt.Println(name, ":goroutine--1-- 停止")
>			return
>		default:
>			fmt.Println(name, ":goroutine1 执行任务")
>			time.Sleep(2 * time.Second)
>		}
>	}
>}
>```
>
>`withCancel`这里边就是开启3个`goroutine` 我们同一使用同一个`cancel context`来进行管理呗 
>
>- `context.Background()` 是**根context**   
>- `context.WithCancel(context.Background())` 取消机制的子`context` 返回类型是一个子`ctx`和`cancel`函数
>- `ctx.Done`                        收到通知信号 进行处理关闭
>
>-----
>
>1. `WithDeadline`函数，和`WithCancel`差不多，它会多传递一个截止时间参数，意味着到了这个时间点，会自动取消Context，当然我们也可以不等到这个时候，可以提前通过取消函数进行取消。
>
>2. `WithTimeout`和`WithDeadline`基本上一样，这个表示是超时自动取消，是多少时间后自动取消Context的意思。
>
>3. `WithValue`函数和取消Context无关，它是为了生成一个绑定了一个键值对数据的`Context`，这个绑定的数据可以通过`Context.Value`方法访问到，后面我们会专门讲。
>
>------
>
>#### 2. `context` 内部实现
>
>像 `WithCancel`、`WithDeadline`、`WithTimeout`、`WithValue` 这些创建函数，实际上是创建了一个个的链表结点而已。我们知道，对链表的操作，通常都是 `O(n)` 复杂度的，效率不高。所以`context`可能并不完美，但是简单高效完成了我们所处的问题呗。







# `epoll `    网络轮训器 





# ==-- 标准库 --==



# `strings`

>正常对于 `string` 字符串的操作 
>
>**拼接操作**
>
>```go
>a:="a" b:="b" s:=a+b 
>```
>
>---
>
>**截取操作**
>
>```go
>str:="hello" res:=str[start:end]  res就是对字符串进行截取
>```
>
>-----
>
>**字符串包含**
>
>```go
>func Contains(s, substr string) bool   
>```
>
>----
>
>**子串包含次数**
>
>```go
>func Count(s, sep string) int     //实现的是 Rabin-Karp 算法
>```
>
>-----
>
>**分割空格**
>
>```go
>func Fields(s string) []string    //分割一个或者多个空格 返回string数组
>```
>
>-----
>
>**分割字符串**
>
>```go
>func Split(s, sep string) []string
>```
>
>**大小写转换**
>
>```go
>func ToLower(s string) string
>```
>
>```go
>func ToUpper(s string) string
>```



# `strconv`

>将字符串转化为其他类型 或者 其他基本类型转化为字符串
>
>*strconv* 包定义了两个 *error* 类型的变量**：*ErrRange* 和 *ErrSyntax***。其中，*ErrRange* 表示值超过了类型能表示的最大范围，比如将 "128" 转为 int8 就会返回这个错误；*ErrSyntax* 表示语法错误，比如将 "" 转为 int 类型会返回这个错误。
>
>-----
>
>**字符串转化为整数 int64有符号整数**
>
>```go
>func Atoi(s string) (i int, err error)
>```
>
>```go
>func ParseUint(s string, base int, bitSize int) (n uint64, err error)   //转化为无符号整数
>```
>
>----
>
>**整数转化为字符串 **  
>
>```go
>func Itoa(i int) string
>```



# `json`

>`encoding/json`是官方提供的标准json。使用的时候需要预定义`struct`，原理是通过`reflection`和`interface`来完成工作, 性能低。
>
>常用的接口：
>
>- `func Marshal(v interface{}) ([]byte, error)`           生成JSON
>- `func Unmarshal(data []byte, v interface{}) error` 解析JSON到`struct`
>
>```go
>func Marshal(v interface{}) ([]byte, error) { body }
>func Unmarshal(data []byte, v interface{}) error { body } 
>```
>
>-----
>
>一般就是不使用标准库里边的 因为反射影响性能呗
>
>GitHub：https://github.com/pquerna/ffjson  阿里巴巴实现
>
>--------------
>
>**go语言里边两种方式实现将对象的值转化为json呗**
>
>第一种：
>
>第一种是基于流。编码器，进行编码值到io流 Writer
>
>```go
>type Encoder struct {}
>
>func NewEncoder(w io.Writer) *Encoder     buf:=new(bytes.Buffer) enc:=json.NewEncoder(buf) 这里边Buffer为什么
>
>func (enc *Encoder) Encode(v interface{}) error
>```
>



# `time`

>```go
>now=Time.now()  //获取当前时间 
>later:=now.Add(time.Hour) //一段时间后呗 
>time.sleep(time.Second)  //睡眠几秒钟之后
>v.expiresAt.After(time.Now()) //time.After 在什么时间之后
>            Before
>
>```
>
>
>



# `bufio`



# `ioutil`





# `http`

><img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/69631e098bca4db086f277c6a12a025b~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp" alt="socket建立过程" style="zoom:50%;" />
>
>http请求进行TCP协议传输
>
>## http 客户端实现cookie
>
>
>
>## http客户端实现事务





# `container`

**list**

>`container.list`    内部数据结构
>
>```go
>type Element struct {
>   // Next and previous pointers in the doubly-linked list of elements.
>   // To simplify the implementation, internally a list l is implemented
>   // as a ring, such that &l.root is both the next element of the last
>   // list element (l.Back()) and the previous element of the first list
>   // element (l.Front()).
>   next, prev *Element
>
>   // The list to which this element belongs.  这里边就是为什么要这么设计就是不懂呗 
>   list *List
>
>   // The value stored with this element.
>   Value interface{}
>}
>```
>
>`Element` 是节点 
>
>```go
>type List struct {
>   root Element // sentinel list element, only &root, root.prev, and root.next are used
>   len  int     // current list length excluding (this) sentinel element
>}
>```
>
>`list`是双向链表   并且在初始化的时候这个双向链表是构成一个环。
>
>-----

**heap**

>`container.heap` 
>
>```go
>type Interface interface {
>   sort.Interface
>   Push(x interface{}) // add x as element Len()
>   Pop() interface{}   // remove and return element Len() - 1.
>}
>```
>
>要是实现堆这种数据结构 编码的时候需要实现这几个接口
>
>----
>
>例子： 实现最小堆
>
>```golang
>type IntHeap []int
>
>func (h IntHeap) Len() int           { return len(h) }
>func (h IntHeap) Less(i, j int) bool { return h[i] < h[j] }
>func (h IntHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }
>
>func (h *IntHeap) Push(x interface{}) {
>    *h = append(*h, x.(int))
>}
>
>func (h *IntHeap) Pop() interface{} {
>    old := *h
>    n := len(old)
>    x := old[n-1]
>    *h = old[0 : n-1]
>    return x
>}
>
>func main(){
>  h := &IntHeap{2, 1, 5}
>  heap.Init(h)
>  heap.Push(h, 3)
>  heap.Pop(h) ==1 
>}
>```
>
>上述是最小堆的实现方式 
>
>如果要实现最大堆 只需要修改 `func less (i,j int) `

**ring**

>环的尾部就是头部，所以每个元素实际上就可以代表自身的这个环。 它不需要像 list 一样保持 list 和 element 两个结构，只需要保持一个结构就行。
>
>```golang
>type Ring struct {
>    next, prev *Ring
>    Value      interface{}
>}
>```
>
>```golang
>func (r *Ring) init() *Ring {
>   r.next = r
>   r.prev = r
>   return r
>}
>```
>
>上述是`ring`的结构和初始化









# ==-- 内存管理 --==

# 堆内存管理



# 栈内存管理



# 垃圾收集器







## [go 字节对齐](https://geektutu.com/post/hpg-struct-alignment.html )

>内存与CPU之间的数据传输需要经过cache，当前Intel的通用CPU基本全部是64位，每个cacheline大小为64字节，因此一次内存访问至少可以获取64字节的数据到cache。
>
>那么按照以下针对不同类型的数据的对齐规则进行对齐的话，就可以保证内存的一次访问都在64字节的 cacheline 宽度范围之内：
>（1）1字节数据可以在任何位置开始访问(对齐在任何地址)
>（2）2字节数据的开始地址是2的倍数，(按2字节对齐)
>（3）3-4字节数据的开始地址是4的倍数，(按4字节对齐)
>（4）5-8字节数据的开始地址是8的倍数，(按8字节对齐)
>
>（5）9-16字节数据的开始地址是16的倍数，(按16字节对齐)
>
>一个64字节或更大的数据结构或数组的开始地址应该按照64字节边界对齐。
>
>## 1 如何计算结构体占用的空间
>
>在 Go 语言中，我们可以使用 `unsafe.Sizeof` 计算出一个数据类型实例需要占用的字节数。
>
>```go
>package main
>
>import (
>	"fmt"
>	"unsafe"
>)
>
>type Args struct {
>    num1 int
>    num2 int
>}
>
>type Flag struct {
>    num1 int16
>    num2 int32
>}
>
>func main() {
>    fmt.Println(unsafe.Sizeof(Args{}))
>    fmt.Println(unsafe.Sizeof(Flag{}))
>}
>```
>
>运行上面的例子将会输出：
>
>```go
>$ go run main.go
>16
>8
>```
>
>- `Args` 由 2 个 int 类型的字段构成，在 64位机器上，一个 int 占 8 字节，因此存储一个 `Args` 实例需要 16 字节。
>- `Flag` 由一个 int32 和 一个 int16 的字段构成，成员变量占据的字节数为 4+2 = 6，但是 `unsafe.Sizeof` 返回的结果为 8 字节，多出来的 2 字节是内存对齐的结果。
>
>因此，一个结构体实例所占据的空间等于各字段占据空间之和，再加上内存对齐的空间大小。
>
>## 2 内存对齐
>
>### 2.1 为什么需要内存对齐
>
>CPU 访问内存时，并不是逐个字节访问，而是以字长（word size）为单位访问。比如 32 位的 CPU ，字长为 4 字节，那么 CPU 访问内存的单位也是 4 字节。
>
>这么设计的目的，是减少 CPU 访问内存的次数，加大 CPU 访问内存的吞吐量。比如同样读取 8 个字节的数据，一次读取 4 个字节那么只需要读取 2 次。
>
>CPU 始终以字长访问内存，如果不进行内存对齐，很可能增加 CPU 访问内存的次数，例如：
>
>![memory alignment](https://geektutu.com/post/hpg-struct-alignment/memory_alignment.png)
>
>变量 a、b 各占据 3 字节的空间，内存对齐后，a、b 占据 4 字节空间，CPU 读取 b 变量的值只需要进行一次内存访问。如果不进行内存对齐，CPU 读取 b 变量的值需要进行 2 次内存访问。第一次访问得到 b 变量的第 1 个字节，第二次访问得到 b 变量的后两个字节。
>
>从这个例子中也可以看到，内存对齐对实现变量的原子性操作也是有好处的，每次内存访问是原子的，如果变量的大小不超过字长，那么内存对齐后，对该变量的访问就是原子的，这个特性在并发场景下至关重要。
>
>简言之：合理的内存对齐可以提高内存读写的性能，并且便于实现变量操作的原子性。
>
>> 参考 [Purpose of memory alignment](https://stackoverflow.com/questions/381244/purpose-of-memory-alignment)
>
>### 2.1 unsafe.Alignof
>
>在上面的例子中，`Flag{}` 两个字段占据了 6 个字节，但是最终对齐后的结果是 8 字节。Go 语言中内存对齐需要遵循什么规律呢？
>
>`unsafe` 标准库提供了 `Alignof` 方法，可以返回一个类型的对齐值，也可以叫做对齐系数或者对齐倍数。例如：
>
>```
>unsafe.Alignof(Args{}) // 8
>unsafe.Alignof(Flag{}) // 4
>```
>
>- `Args{}` 的对齐倍数是 8，`Args{}` 两个字段占据 16 字节，是 8 的倍数，无需占据额外的空间对齐。
>- `Flag{}` 的对齐倍数是 4，因此 `Flag{}` 占据的空间必须是 4 的倍数，因此，6 内存对齐后是 8 字节。
>
>### 2.2 对齐保证(align guarantee)
>
>Go 官方文档 [Size and alignment guarantees - golang spec](https://golang.org/ref/spec#Size_and_alignment_guarantees) 描述了 `unsafe.Alignof` 的规则。
>
>> 1. For a variable x of any type: unsafe.Alignof(x) is at least 1.
>> 2. For a variable x of struct type: unsafe.Alignof(x) is the largest of all the values unsafe.Alignof(x.f) for each field f of x, but at least 1.
>> 3. For a variable x of array type: unsafe.Alignof(x) is the same as the alignment of a variable of the array’s element type.
>
>- 对于任意类型的变量 x ，`unsafe.Alignof(x)` 至少为 1。
>- 对于 struct 结构体类型的变量 x，计算 x 每一个字段 f 的 `unsafe.Alignof(x.f)`，`unsafe.Alignof(x)` 等于其中的最大值。
>- 对于 array 数组类型的变量 x，`unsafe.Alignof(x)` 等于构成数组的元素类型的对齐倍数。
>
>> A struct or array type has size zero if it contains no fields (or elements, respectively) that have a size greater than zero. Two distinct zero-size variables may have the same address in memory.
>
>没有任何字段的空 struct{} 和没有任何元素的 array 占据的内存空间大小为 0，不同的大小为 0 的变量可能指向同一块地址。
>
>## 3 struct 内存对齐的技巧
>
>### 3.1 合理布局减少内存占用
>
>假设一个 struct 包含三个字段，`a int8`、`b int16`、`c int64`，顺序会对 struct 的大小产生影响吗？我们来做一个实验：
>
>```go
>type demo1 struct {
>	a int8
>	b int16
>	c int32
>}
>
>type demo2 struct {
>	a int8
>	c int32
>	b int16
>}
>
>func main() {
>	fmt.Println(unsafe.Sizeof(demo1{})) // 8
>	fmt.Println(unsafe.Sizeof(demo2{})) // 12
>}
>```
>
>答案是会产生影响。每个字段按照自身的对齐倍数来确定在内存中的偏移量，字段排列顺序不同，上一个字段因偏移而浪费的大小也不同。
>
>接下来逐个分析，首先是 demo1：
>
>- a 是第一个字段，默认是已经对齐的，从第 0 个位置开始占据 1 字节。
>- b 是第二个字段，对齐倍数为 2，因此，必须空出 1 个字节，偏移量才是 2 的倍数，从第 2 个位置开始占据 2 字节。
>- c 是第三个字段，对齐倍数为 4，此时，内存已经是对齐的，从第 4 个位置开始占据 4 字节即可。
>
>因此 demo1 的内存占用为 8 字节。
>
>其实是 demo2：
>
>- a 是第一个字段，默认是已经对齐的，从第 0 个位置开始占据 1 字节。
>- c 是第二个字段，对齐倍数为 4，因此，必须空出 3 个字节，偏移量才是 4 的倍数，从第 4 个位置开始占据 4 字节。
>- b 是第三个字段，对齐倍数为 2，从第 8 个位置开始占据 2 字节。
>
>demo2 的对齐倍数由 c 的对齐倍数决定，也是 4，因此，demo2 的内存占用为 12 字节。
>
>![memory alignment](https://geektutu.com/post/hpg-struct-alignment/memory_alignment_order.png)
>
>因此，在对内存特别敏感的结构体的设计上，我们可以通过调整字段的顺序，减少内存的占用。
>
>### 3.2 空 struct{} 的对齐
>
>空 `struct{}` 大小为 0，作为其他 struct 的字段时，一般不需要内存对齐。但是有一种情况除外：即当 `struct{}` 作为结构体最后一个字段时，需要内存对齐。因为如果有指针指向该字段, 返回的地址将在结构体之外，如果此指针一直存活不释放对应的内存，就会有内存泄露的问题（该内存不因结构体释放而释放）。
>
>因此，当 `struct{}` 作为其他 struct 最后一个字段时，需要填充额外的内存保证安全。我们做个试验，验证下这种情况。
>
>```
>type demo3 struct {
>	c int32
>	a struct{}
>}
>
>type demo4 struct {
>	a struct{}
>	c int32
>}
>
>func main() {
>	fmt.Println(unsafe.Sizeof(demo3{})) // 8
>	fmt.Println(unsafe.Sizeof(demo4{})) // 4
>}
>```
>
>可以看到，`demo4{}` 的大小为 4 字节，与字段 c 占据空间一致，而 `demo3{}` 的大小为 8 字节，即额外填充了 4 字节的空间。

## goroutine && 协程

>https://www.cnblogs.com/liang1101/p/7285955.html
>
>```go
>go func()  开一个goroutine 是一个用户级别的协程 
>```
>
>- **go协程工作原理：很重点**
>
>​        他和线程的原理是一样的，当 a线程 切换到 b线程 的时候，需要将 a线程 的相关执行进度压入栈，然后将 b线程 的执行进度出栈，进入 b线程 的执行序列。协程只不过是在 应用层 实现这一点。但是，协程并不是由操作系统调度的，而且应用程序也没有能力和权限执行 cpu 调度。怎么解决这个问题？
>
>　　答案是，协程是基于线程的。内部实现上，维护了一组数据结构和 n 个线程，真正的执行还是线程，协程执行的代码被扔进一个待执行队列中，由这 n 个线程从队列中拉出来执行。这就解决了协程的执行问题。那么协程是怎么切换的呢？答案是：golang 对各种 io函数 进行了封装，这些封装的函数提供给应用程序使用，而其内部调用了操作系统的异步 io函数，当这些异步函数返回 busy 或 bloking 时，golang 利用这个时机将现有的执行序列压栈，让线程去拉另外一个协程的代码来执行，基本原理就是这样，利用并封装了操作系统的异步函数。包括 linux 的 epoll、select 和 windows 的 iocp、event 等。
>
>------
>
>```go
>
>------------------  chan 作为参数进行 ch chan *Person 可以进行写操作-------------
>type Person struct {
>	age  int
>	name string
>}
>
>func main() {
>	//TODO goroutine记得return或者中断，不然容易造成goroutine占用大量CPU。 这句话是啥意思呢
>	//go func() 这里边是没有返回值的呢 开启一个goroutine 在这里就是返回也不行呗
>	ch := make(chan *Person)
>	go printStr("age18", ch)
>	value := <-ch
>	fmt.Println(value)
>}
>
>//这里边就是管道作为参数 读还是写 一定要想明白呗
>func printStr(str string, ch chan *Person) {
>	ch <- &Person{
>		age:  18,
>		name: str,
>	}
>	return
>}
>
>--------------------chan 作为参数 进行读操作  --------------------------
>func main() {
>	wg := &sync.WaitGroup{}
>	wg.Add(1)
>	ch := make(chan *Person, 1) //这里边如果ch作为的需要进行写操作么
>	ch <- &Person{
>		age:  17,
>		name: "whig",
>	}
>	go printStr("a", ch, wg)
>	wg.Wait()
>}
>
>//这里边就是管道作为参数 读还是写 一定要想明白呗
>func printStr(str string, ch chan *Person, wg *sync.WaitGroup) {
>	value := <-ch
>	fmt.Println(value)
>	wg.Done()
>}
>
>```



## Channel

>https://colobu.com/2016/04/14/Golang-Channels/
>
>https://blog.csdn.net/zhonglinzhang/article/details/83959974  这个不错
>
>**明白channel是通过注册相关goroutine id实现消息通知的。**
>
>**不要通过共享内存的方式进行通信，而是应该通过通信的方式共享内存  这个就是channel的设计理念呗 **
>
>
>
>协程需要并发通信模型呗 一共有两种并发通信模型  **共享内存  消息**
>
>共享内存：` sync-->mutex.lock`
>
>消息：       ` make(chan 类型， 缓存)`
>
>```go
>// 将一个数据value写入至channel，这会导致阻塞，直到有其他goroutine从这个channel中读取数据
>ch <- value
>
>// 从channel中读取数据，如果channel之前没有写入数据，也会导致阻塞，直到channel中被写入数据为止
>value := <-ch
>```
>
>
>
>- 有缓存和无缓存的区别
>
>如果没有设置容量，或者容量设置为0, 说明Channel没有缓存，只有sender和receiver都准备好了后它们的通讯(communication)才会发生(Blocking)。如果设置了缓存，就有可能不发生阻塞， 只有buffer满了后 send才会阻塞， 而只有缓存空了后receive才会阻塞。一个nil channel不会通信。
>
>- 无缓冲 chan 的发送和接收是否同步？
>
>-----
>
>```go
>func main() {
>	group := &sync.WaitGroup{}
>	chanA := make(chan struct{}, 1)
>	chanB := make(chan struct{}, 1)
>	chanC := make(chan struct{}, 1)
>	chanA <- struct{}{}
>	group.Add(3)
>	go printABC(chanA, chanB, group, "A")
>	go printABC(chanB, chanC, group, "B")
>	go printABC(chanC, chanA, group, "C")
>	group.Wait()
>}
>
>// chan 来实现进程之间的通信呗
>func printABC(now chan struct{}, next chan struct{}, group *sync.WaitGroup, str string) {
>	for i := 0; i < 2; i++ {
>		<-now
>		fmt.Println(str)
>		next <- struct{}{}
>	}
>	group.Done()
>	return
>}
>```
>
>利用`chan`来实现多协程来打印字母
>
>-----
>
>在创建的时候 `ch:=make(chan int,1)` 其实就是创建一个指向chan的指针
>
>```go
>func main() {
>	ch := make(chan int, 3)
>	ch <- 1
>	ch <- 2
>	ch <- 3
>	fmt.Println(ch)
>	chanTest(ch)
>	val1 := <-ch
>	val2 := <-ch
>	fmt.Println(val1)
>	fmt.Println(val2)
>}
>
>func chanTest(ch chan int) {
>	fmt.Println(ch)
>	val := <-ch
>	fmt.Println(val)
>}
>
>0x1400013a000
>0x1400013a000
>1
>2
>3
>
>```
>

# ==-- 多协程 --==

# 生产者消费者模型

>```go
>import "fmt"
>
>func producer(out chan<- int) {
>	for i := 0; i < 10; i++ {
>		data := i * i
>		fmt.Println("生产者生产数据:", data)
>		out <- data // 缓冲区写入数据
>	}
>	close(out) //写完关闭管道
>}
>
>func consumer(in <-chan int) {
>
>	// 无需同步机制，先做后做
>	// 没有数据就阻塞等
>	for data := range in {
>		fmt.Println("消费者得到数据：", data)
>	}
>
>}
>
>func main() {
>	// 传参的时候显式类型像隐式类型转换，双向管道向单向管道转换  这里边就是添加缓冲区呗 在这里哈呢
>	ch := make(chan int, 5) // 添加缓冲区，5
>	go producer(ch) // 子go程作为生产者
>	consumer(ch)    // 主go程作为消费者
>}
>```
>
>上述就是存在有缓冲 的生产者和消费者模型



# 多协程累加数字



>开启三个协程 累加数字到1000
>
>```go
>// 三个协程累加数字  重0累加到3000
>var num int = 0
>func main() {
>	mutex := &sync.Mutex{}
>	waitGroup := &sync.WaitGroup{}
>	for i := 0; i < 3; i++ {
>		waitGroup.Add(1)		//这里边就是先添加 不要在addNum里边添加 否则就是main函数执行完毕了
>		go addNum(mutex, waitGroup)
>	}
>	waitGroup.Wait()
>	fmt.Println(num)
>	fmt.Println("三个线程累加数字")
>}
>
>func addNum(mutex *sync.Mutex, waitGroup *sync.WaitGroup) {
>	for i := 0; i < 1000; i++ {
>		mutex.Lock()
>		num++
>		mutex.Unlock()
>	}
>	waitGroup.Done()
>	return
>}
>```
>
>这里边涉及知识点：---》 `sync.mutex  sync.WaitGroup`  





# 顺序打印

>- 使用 `sync`  以及 `int`变量
>
>```go
>var time int = 2
>var state int = 0
>func printString(str string, targetNum int, mutex *sync.Mutex, waitGroup *sync.WaitGroup) {
>	for i := 0; i < time; {
>		mutex.Lock()
>		if state%3 == targetNum {
>			state++ //以及这个state++
>			i++     //这里边i++是精髓呗 如果在这里就不是i++ 三个协程很快就是执行完毕了呢
>			fmt.Println(str)
>		}
>		mutex.Unlock()
>	}
>	waitGroup.Done()
>}
>func main() {
>	mutex := &sync.Mutex{}
>	waitGroup := &sync.WaitGroup{}
>	waitGroup.Add(3)
>	go printString("A", 0, mutex, waitGroup)
>	go printString("B", 1, mutex, waitGroup)
>	go printString("C", 2, mutex, waitGroup)
>	waitGroup.Wait()
>}
>```
>
>------
>
>- 使用`chan`来进行通信 
>
>```go
>func main() {
> group := &sync.WaitGroup{}
> chanA := make(chan struct{}, 1)   //后边必须要跟1 否则就是报错呢
> chanB := make(chan struct{}, 1)
> chanC := make(chan struct{}, 1)
> chanA <- struct{}{}
> group.Add(3)
> go printABC(chanA, chanB, group, "A")
> go printABC(chanB, chanC, group, "B")
> go printABC(chanC, chanA, group, "C")
> group.Wait()
>}
>
>// chan 来实现进程之间的通信呗
>func printABC(now chan struct{}, next chan struct{}, group *sync.WaitGroup, str string) {
> for i := 0; i < 2; i++ {
>    <-now								           //当前进行读
>    fmt.Println(str)
>    next <- struct{}{}						 //下一个进行写入
> }
> group.Done()
> return
>}
>```





# ==--垃圾回收--==

>当前Golang使用的垃圾回收机制是**三色标记发**配合**写屏障**和**辅助GC**，三色标记法是**标记-清除法**的一种增强版本。简单地说，**垃圾回收(GC)是在后台运行一个守护线程，它的作用是在监控各个对象的状态，识别并且丢弃不再使用的对象来释放和重用资源。**



# 垃圾回收算法

## 标记-清除法（mark and sweep）

>原始的标记清楚法分为两个步骤：
>
>1. 标记。先STP(Stop The World)，暂停整个程序的全部运行线程，将被引用的对象打上标记
>2. 清除没有被打标机的对象，即回收内存资源，然后恢复运行线程。
>
>这样做有个很大的问题就是要通过STW保证GC期间标记对象的状态不能变化，整个程序都要暂停掉，在外部看来程序就会卡顿。



## 三色标记法

>三色标记法是对标记阶段的改进，原理如下：
>
>1. 初始状态所有对象都是白色。
>2. 从root根出发扫描所有根对象（下图a,b），将他们引用的对象标记为灰色（图中A，B）
>
>> 那么什么是root呢？
>
>root区域主要是程序运行到当前时刻的栈和全局数据区域。
>
>3. 分析灰色对象是否引用了其他对象。如果没有引用其它对象则将该灰色对象标记为黑色（上图中A）；如果有引用则将它变为黑色的同时将它引用的对象也变为灰色（上图中B引用了D）
>4. 重复步骤3，直到灰色对象队列为空。此时白色对象即为垃圾，进行回收。



![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/16/16c9aba51c025700~tplv-t2oaga2asx-watermark.awebp)

也可以参考下面的动图辅助理解：

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/8/16/16c9abaa4032c7ea~tplv-t2oaga2asx-watermark.awebp)

## Go GC如何工作

>上面介绍的是GO GC采用的三色标记算法，但是好像并没有体现出来怎么减少STW对程序的影响呢？其实是因为**Golang GC的大部分处理是和用户代码并行的**。
>
>GC期间用户代码可能会改变某些对象的状态，如何实现GC和用户代码并行呢？先看下GC工作的完整流程：
>
>1. Mark: 包含两部分:
>
>- Mark Prepare: 初始化GC任务，包括开启写屏障(write barrier)和辅助GC(mutator assist)，统计root对象的任务数量等。**这个过程需要STW**
>- GC Drains: 扫描所有root对象，包括全局指针和goroutine(G)栈上的指针（扫描对应G栈时需停止该G)，将其加入标记队列(灰色队列)，并循环处理灰色队列的对象，直到灰色队列为空。**该过程后台并行执行**
>
>1. Mark Termination: 完成标记工作，重新扫描(re-scan)全局指针和栈。因为Mark和用户程序是并行的，所以在Mark过程中可能会有新的对象分配和指针赋值，这个时候就需要通过写屏障（write barrier）记录下来，re-scan 再检查一下。**这个过程也是会STW的。**
>2. Sweep: 按照标记结果回收所有的白色对象，**该过程后台并行执行**
>3. Sweep Termination: 对未清扫的span进行清扫, 只有上一轮的GC的清扫工作完成才可以开始新一轮的GC。
>
>如果标记期间用户逻辑改变了刚打完标记的对象的引用状态，怎么办呢？





## 写屏障(Write Barrier)

>写屏障：该屏障之前的写操作和之后的写操作相比，先被系统其它组件感知。 好难懂哦，结合上面GC工作的完整流程就好理解了，就是在每一轮GC开始时会初始化一个叫做“屏障”的东西，然后由它记录第一次scan时各个对象的状态，以便和第二次re-scan进行比对，引用状态变化的对象被标记为灰色以防止丢失，将屏障前后状态未变化对象继续处理。



## 辅助GC

>从上面的GC工作的完整流程可以看出Golang GC实际上把单次暂停时间分散掉了，本来程序执⾏可能是“⽤户代码-->⼤段GC-->⽤户代码”，那么分散以后实际上变成了“⽤户代码-->⼩段 GC-->⽤户代码-->⼩段GC-->⽤户代码”这样。如果GC回收的速度跟不上用户代码分配对象的速度呢？ Go 语⾔如果发现扫描后回收的速度跟不上分配的速度它依然会把⽤户逻辑暂停，⽤户逻辑暂停了以后也就意味着不会有新的对象出现，同时会把⽤户线程抢过来加⼊到垃圾回收⾥⾯加快垃圾回收的速度。这样⼀来原来的并发还是变成了STW，还是得把⽤户线程暂停掉，要不然扫描和回收没完没了了停不下来，因为新分配对象⽐回收快，所以这种东⻄叫做辅助回收。



## 如何进行GC调优

>衡量GC对程序的影响可以参考这篇文章，[Go 程序的性能调试问题](https://link.juejin.cn?target=https%3A%2F%2Fwww.oschina.net%2Ftranslate%2Fdebugging-performance-issues-in-go-programs)。
>
>减少对象的分配，合理重复利用； 避免string与[]byte转化；
>
>> 两者发生转换的时候，底层数据结结构会进行复制，因此导致 gc 效率会变低。
>
>少量使用+连接 string；
>
>> Go里面string是最基础的类型，是一个只读类型，针对他的每一个操作都会创建一个新的string。 如果是少量小文本拼接，用 “+” 就好；如果是大量小文本拼接，用 strings.Join；如果是大量大文本拼接，用 bytes.Buffer。





## GC触发条件

>自动垃圾回收的触发条件有两个：
>
>1. 超过内存大小阈值
>2. 达到定时时间
>
>阈值是由一个gcpercent的变量控制的,当新分配的内存占已在使用中的内存的比例超过gcprecent时就会触发。比如一次回收完毕后，内存的使用量为5M，那么下次回收的时机则是内存分配达到10M的时候。也就是说，并不是内存分配越多，垃圾回收频率越高。 如果一直达不到内存大小的阈值呢？这个时候GC就会被定时时间触发，比如一直达不到10M，那就定时（默认2min触发一次）触发一次GC保证资源的回收。



## 

# 栈内存分析 是否`stw`



# ==-- GO连接使用中间件 --==



# ==rpc实现==

>`rpc`是一种进程间的通信方式
>
>

## 安装grpc  && protocbuf

>https://www.jianshu.com/p/24ac2300bf1d                                   在这里就是推荐mac brew安装方式呗 protoc 并配置环境变量
>
>https://grpc.io/docs/languages/go/quickstart/                              grpc官网地址
>
>https://developers.google.com/protocol-buffers/docs/gotutorial  proto3地址 简要说明使用proto 
>
>为什么要使用proto这种中间文件并使用protobuf编译器来生成指定语言的文件     其实就是类似于xml文件 

>创建项目的时候 需要导入 grpc的包呗 在这里哈呢
>
>```go
>require (
>	github.com/gin-contrib/sse v0.1.0 // indirect
>	github.com/go-playground/locales v0.13.0 // indirect
>	github.com/go-playground/universal-translator v0.17.0 // indirect
>	github.com/go-playground/validator/v10 v10.4.1 // indirect
>	github.com/golang/protobuf v1.5.2 // indirect
>	github.com/json-iterator/go v1.1.9 // indirect
>	github.com/leodido/go-urn v1.2.0 // indirect
>	github.com/mattn/go-isatty v0.0.12 // indirect
>	github.com/modern-go/concurrent v0.0.0-20180228061459-e0a39a4cb421 // indirect
>	github.com/modern-go/reflect2 v0.0.0-20180701023420-4b7aa43c6742 // indirect
>	github.com/ugorji/go/codec v1.1.7 // indirect
>	golang.org/x/crypto v0.0.0-20200622213623-75b288015ac9 // indirect
>	golang.org/x/net v0.0.0-20220401154927-543a649e0bdd // indirect
>	golang.org/x/sys v0.0.0-20220330033206-e17cdc41300f // indirect
>	golang.org/x/text v0.3.7 // indirect
>	google.golang.org/genproto v0.0.0-20220401170504-314d38edb7de // indirect
>	google.golang.org/grpc v1.45.0 // indirect
>	google.golang.org/protobuf v1.28.0 // indirect
>	gopkg.in/yaml.v2 v2.2.8 // indirect
>)
>```
>
>编译 proto文件 在这里就是使用   `protoc --go_out=plugins=grpc:../services prod.proto`     ../services 是输出目录     prod.proto是原文件 需要进入原文件目录进行编译呗 在这里哈呢





## 为什么需要rpc这种框架

>Remote Procedure Call，远程过程调用)是一种计算机通信协议，允许调用不同进程空间的程序。RPC 的客户端和服务器可以在一台机器上，也可以在不同的机器上。程序员使用时，就像调用本地程序一样，无需关注内部的实现细节。
>
>不同的应用程序之间的通信方式有很多，比如浏览器和服务器之间广泛使用的基于 HTTP 协议的 Restful API。与 RPC 相比，Restful API 有相对统一的标准，因而更通用，兼容性更好，支持不同的语言。HTTP 协议是基于文本的，一般具备更好的可读性。但是缺点也很明显：
>
>- Restful 接口需要额外的定义，无论是客户端还是服务端，都需要额外的代码来处理，而 RPC 调用则更接近于直接调用。
>- 基于 HTTP 协议的 Restful 报文冗余，承载了过多的无效信息，而 RPC 通常使用自定义的协议格式，减少冗余报文。
>- RPC 可以采用更高效的序列化协议，将文本转为二进制传输，获得更高的性能。
>- 因为 RPC 的灵活性，所以更容易扩展和集成诸如注册中心、负载均衡等功能。
>
>----------
>
>简单来说成熟的rpc库相对http容器，跟多的是封装了“服务发现”，"错误重试"一类面向服务的高级特性。可以这么理解，rpc框架是面向服务的更高级的封装。如果把一个http server容器上封装一层服务发现和函数代理调用，那它就已经可以做一个rpc框架了。
>
> **所以为什么要用rpc调用？**
> 因为良好的rpc调用是面向服务的封装，针对服务的可用性和效率等都做了优化。单纯使用http调用则缺少了这些特性。
>
>并且如果服务端的实例很多，客户端并不关心这些实例的地址和部署位置，只关心自己能否获取到期待的结果，那就引出了注册中心(registry)和负载均衡(load balance)的问题。简单地说，即客户端和服务端互相不感知对方的存在，服务端启动时将自己注册到注册中心，客户端调用时，从注册中心获取到所有可用的实例，选择一个来调用。这样服务端和客户端只需要感知注册中心的存在就够了。注册中心通常还需要实现服务动态添加、删除，使用心跳确保服务处于可用状态等功能。

## 01-- 服务端与消息编码

>一个 rpc 调用过程可以分配 客户端调用服务端方法 可以说是服务名称、方法名、参数  返回值是 err、以及调用返回值呗   
>
>```go
>func call ("服务名称",methodName, Args) err,reply  
>```
>
>
>
>

## 02 -- 高性能客户端

## 03 -- 服务注册

## 04 -- 超时处理

## 05 -- 支持HTTP协议

## 06 -- 负载均衡

## 07 -- 服务注册与发现中心





# ==Gin==

>相关 import 包 `"github.com/gin-gonic/gin"`  导入包来使用gin呗
>
>- request数据是如何流转的
>- gin框架到底扮演了什么角色
>- 请求从gin流入net/http, 最后又是如何回到gin中
>- gin的context为何能承担起来复杂的需求
>- gin的路由算法
>- gin的中间件是什么
>- gin的Engine具体是个什么东西
>- net/http的requeset, response都提供了哪些有用的东西
>
>------------------
>
>net/http 是如何直接就是进行传输数据的呗 在这里哈呢 




## Gin的Next() 和 Abort()

>https://blog.dianduidian.com/post/gin-%E4%B8%AD%E9%97%B4%E4%BB%B6next%E6%96%B9%E6%B3%95%E5%8E%9F%E7%90%86%E8%A7%A3%E6%9E%90/
>
>这里边中间件其实也就是  `gin.HandlerFunc`处理函数
>
>`Next:` 其实就是挂起当前中间件的后续代码的处理逻辑，再执行后续的中间件。内部实现就是利用 **index索引 和[]handlerFunc 来遍历实现**
>
>`Abort:`执行当前中间件的逻辑代码， 后续的中间件不在执行。
>
>```go
>func main() {
>	r := gin.New()
>	r.Use(midOne())
>	r.Use(midTwo())
>	r.Use(midThree())
>	r.GET("/ping", func(c *gin.Context) {
>		c.JSON(200, "ok")
>	})
>	r.Run(":8080")
>
>}
>
>func midOne() gin.HandlerFunc {
>	return func(context *gin.Context) {
>		log.Println(0)
>		context.Abort()					//执行  0 1     		 如果是 Next 执行 0231
>		log.Println("1")
>	}
>}
>
>func midTwo() gin.HandlerFunc {
>	return func(context *gin.Context) {
>		log.Println("2")
>	}
>}
>
>func midThree() gin.HandlerFunc {
>	return func(context *gin.Context) {
>		log.Println("3")
>	}
>}
>```
>
>------
>
>这种实现原理：
>
>```go
>我们之前的框架设计是这样的，当接收到请求后，匹配路由，该请求的所有信息都保存在Context中。中间件也不例外，接收到请求后，应查找所有应作用于该路由的中间件，保存在Context中，依次进行调用。为什么依次调用后，还需要在Context中保存呢？因为在设计中，中间件不仅作用在处理流程前，也可以作用在处理流程后，即在用户定义的 Handler 处理完毕后，还可以执行剩下的操作。
>为此，我们给Context添加了2个参数，定义了Next方法：
>type Context struct {
>	// origin objects
>	Writer http.ResponseWriter
>	Req    *http.Request
>	// request info
>	Path   string
>	Method string
>	Params map[string]string
>	// response info
>	StatusCode int
>	// middleware
>	handlers []HandlerFunc
>	index    int
>}
>
>func newContext(w http.ResponseWriter, req *http.Request) *Context {
>	return &Context{
>		Path:   req.URL.Path,
>		Method: req.Method,
>		Req:    req,
>		Writer: w,
>		index:  -1,
>	}
>}
>
>func (c *Context) Next() {
>	c.index++
>	s := len(c.handlers)
>	for ; c.index < s; c.index++ {
>		c.handlers[c.index](c)
>	}
>}
>index是记录当前执行到第几个中间件，当在中间件中调用Next方法时，控制权交给了下一个中间件，直到调用到最后一个中间件，然后再从后往前，调用每个中间件在Next方法之后定义的部分
>```
>
>index是记录当前执行到第几个中间件，当在中间件中调用Next方法时，控制权交给了下一个中间件，直到调用到最后一个中间件，然后再从后往前，调用每个中间件在Next方法之后定义的部分

## HTTP

>HTTP请求 概括来说就是两个点：
>
>1. 路由 请求路径
>2. 该路由下的处理函数
>
>-----
>
>基于以上两点就是可以简单完成一个HTTP请求
>
>如果我们要是进行封装
>
>就是可以定义一个结构体 实现net/http 里边的 ServeHTTP   之后所有的请求都会到这个函数里边来。
>
>```go
>func (engine *Engine) ServeHTTP(w http.ResponseWriter, req *http.Request) 
>```
>
>在进行封装一下：
>
>可以在结构体里边增加字段： router map[string]handleFunc  映射路径+处理函数









## Context  上下文

>上下文： 主要封装 Request 和 Response ，提供对 JSON、HTML 等返回类型的支持。
>
>1. 对Web服务来说，无非是根据请求`*http.Request`，构造响应`http.ResponseWriter`。但是这两个对象提供的接口粒度太细，比如我们要构造一个完整的响应，需要考虑消息头(Header)和消息体(Body)，而 Header 包含了状态码(StatusCode)，消息类型(ContentType)等几乎每次请求都需要设置的信息。因此，如果不进行有效的封装，那么框架的用户将需要写大量重复，繁杂的代码，而且容易出错。针对常用场景，能够高效地构造出 HTTP 响应是一个好的框架必须考虑的点。
>
>```go
>type Context struct {
>	// origin objects
>	Writer http.ResponseWriter
>	Req    *http.Request
>	// request info
>	Path   string
>	Method string
>	// response info
>	StatusCode int
>}
>
>对Json数据进行编码 并进行返回呗 
>func (c *Context) JSON(code int, obj interface{}) {
>	c.SetHeader("Content-Type", "application/json")
>	c.Status(code)
>	encoder := json.NewEncoder(c.Writer)
>	if err := encoder.Encode(obj); err != nil {
>		http.Error(c.Writer, err.Error(), 500)
>	}
>}
>```
>
>路由的话： 暂时就是一个map 结构 `key:path  value:handleFunc 处理方法`





## 路由

>如果我们不支持动态路由就是可以采用 `map[string] handleFunc` 这种就是 路径对处理函数即可
>
>
>
>假如支持 动态路由 `/hello/:name`，可以匹配`/hello/geektutu`、`hello/jack`等。 我们就是可以使用前缀树这种数据结构来实现



## Next Abort





# ==--编码遇到问题--==

# slice 二维数组初始化

>必须要先指定多少行 
>
>如果`make([][]byte,0)` 这时候在添加的时候就是会报错呗  



# int32 运算时超出范围如何处理

>

# ==--面试--==

>```go
>1. 二维数组  i j读取的顺序哪个更快 顺序读取 利用到了cpu 缓存cache 
>2. 如果是多核CPU  读取缓存发生冲突会怎么办  IMSI 2个bit 4个状态位 共享、独占、私有。。
>
>3. 程序打印结果
> func test(){
> var a uint=1
> var b uint=2
> fmt.println(a-b)  结果应该是2^32-1  为啥是这个呢 好好想-1的补码
> }
>
>
>3. 使用Goroutine 依次打印 cat dog fish   每一个都打印100次  好难
>
>3. channel 在golang里边如何实现的 有缓冲和无缓冲的区别？ 为什么是线程安全的
> 有缓存：放在缓存队列里边
> 无缓存：一次只能存放一个元素
>```
>
>1. uint不能直接相减，结果是负数会变成一个很大的uint，这点对动态语言出身的会可能坑。
>
>2. 从slice创建slice的时候，注意原slice的操作可能导致底层数组变化。
>
>3. 如果你要创建一个很长的slice，尽量创建成一个slice里存引用，这样可以分批释放，避免gc在低配机器上stop the world
>4. 尽量了解golang的内存模型，知道多小才是小对象，为什么小对象多了会造成gc压力。
>
>-----
>
>1、空struct{}是否使用过？会在什么情况下使用，举例说明一下。 
>
>2、在Go语言中，结构体是否能够比较？该如何比较两个结构体？如何比较两个接口？可以顺便查考一下代码实现。 
>
>3、使用Go语言编程实现堆栈和队列这两个数据结构，该如何实现。可以只说实现思路。 
>
>4、var a []int和a := []int{}是否有区别？如果有的话，具体有什么区别？在开发过程中使用哪个更好，为什么？ 
>
>5、Go中，如何复制切片内容？如何复制map内容？如何复制接口内容？编程时会如何操作实现。



# go显示指定某个类型实现接口

>```go
>package main
>
>import "io"
>
>type myWriter struct {
>
>}
>
>/*func (w myWriter) Write(p []byte) (n int, err error) {
>	return
>}*/
>
>func main() {
>    // 检查 *myWriter 类型是否实现了 io.Writer 接口
>    var _ io.Writer = (*myWriter)(nil)
>
>    // 检查 myWriter 类型是否实现了 io.Writer 接口
>    var _ io.Writer = myWriter{}
>}
>
>```
>
>实际上，上述赋值语句会发生隐式地类型转换，在转换的过程中，编译器会检测等号右边的类型是否实现了等号左边接口所规定的函数。



# 空struct{}是否使用过？会在什么情况下使用，举例说明一下

>因为空结构体不占据内存空间，因此被广泛作为各种场景下的占位符使用。一是节省资源，二是空结构体本身就具备很强的语义，即这里不需要任何值，仅作为占位符。
>
>比如：
>
>1. 使用信道(channel)控制并发时，我们只是需要一个信号，但并不需要传递值，这个时候，也可以使用 struct{} 代替。`ch := make(chan struct{}, `1)
>2. 声明只包含方法的结构体。 结构体是空的 但是带有方法的结构体

# init() 函数是什么时候执行的？

>每个包首先初始化包作用域的常量和变量（常量优先于变量），然后执行包的 `init()` 函数。同一个包，甚至是同一个源文件可以有多个 `init()` 函数。`init()` 函数没有入参和返回值，不能被其他函数调用，同一个包内多个 `init()` 函数的执行顺序不作保证。
>
>一句话总结： import –> const –> var –> `init()` –> `main()`
>
>

# 内存溢出 案例

https://blog.rexskz.info/trip-for-finding-golang-memory-leak.html



# go如何实现定时任务

>time.sleep，追问别的方法：应该是要问Timer和Ticker，当时没反应过来（本来也不熟悉这个），就开始说用WaitGroup和defer，应该是答偏了…… 
