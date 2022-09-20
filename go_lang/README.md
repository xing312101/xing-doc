# Go Lang
> reference: https://golang.org/

## install
> reference: https://golang.org/doc/install

Download: https://golang.org/dl/
```
$ sudo tar -C /usr/local -xzf go1.12.linux-amd64.tar.gz

在$HOME/.profile 或 .bashrc_profile 加入
export PATH=$PATH:/usr/local/go/bin

可以考慮連workspace的bin也加入$PATH
```

## Hello go
```
package main

import "fmt"

func main() {
	fmt.Printf("hello, world\n")
}
```
```
go run   # 編譯及執行
go build # 在當下位置編譯出專案執行檔
go install # 編譯出專案執行檔，並在workspace/bin放置執行檔
```

## Sendbox
> https://play.golang.org/

## Package
> reference: https://tour.golang.org/basics/1

```
package main

import (
	"fmt"
	"math/rand"
)

func main() {
	fmt.Println("My favorite number is", rand.Intn(10))
}

```
每個GO都是個packages，起始程式都是從package main開始。
當要使用其他package時要使用import，使用上程式只要呼叫路徑上最後的package name，比如上面的rand。

## Functions
> reference: https://tour.golang.org/basics/4

```
package main
import "fmt"

func add(x int, y int) int {
    return x + y
}

func main(){
    fmt.Println(add(2, 3))
}

# function的參數的型態定義可以連續定義
func add(x , y int) int {
	return x + y
}

# function回傳值可以多個
func swap(x, y string) (string, string) {
	return y, x
}
func main() {
	a, b := swap("hello", "world")
	fmt.Println(a, b)
}

# function回傳值先決定好變數名，後續只需要return就好不用帶值
func split(sum int) (x, y int) {
	x = sum * 4 / 9
	y = sum - x
	return
}

```

## Variables
> reference: https://tour.golang.org/basics/8

```
package main

import "fmt"

var c, python, java bool // 僅宣告
var i, j int = 1, 2 // 宣告且給預設值

func main() {
	var i2 int
	var c2, python2, java2 = true, false, "no!"

	fmt.Println(i, c, python, java)
	fmt.Println(i2, c2, python2, java2)

	k := 3 // 短宣告，不能放在外層宣告，需要放進function
}

```

### Type
> reference: reference: https://tour.golang.org/basics/11

```
bool

string

int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // alias for uint8

rune // alias for int32
     // represents a Unicode code point

float32 float64

complex64 complex128

#####
package main

import (
	"fmt"
	"math/cmplx"
)

var (
	ToBe   bool       = false
	MaxInt uint64     = 1<<64 - 1
	z      complex128 = cmplx.Sqrt(-5 + 12i)
)

func main() {
	fmt.Printf("Type: %T Value: %v\n", ToBe, ToBe)
	fmt.Printf("Type: %T Value: %v\n", MaxInt, MaxInt)
	fmt.Printf("Type: %T Value: %v\n", z, z)

	### zero values
	# 數值都是0
	#布林是false
	# 字串是空字串
	var i int
	var f float64
	var b bool
	var s string
	fmt.Printf("%v %v %v %q\n", i, f, b, s)
}

```

### 轉型態
> reference: https://tour.golang.org/basics/13

```
var i int = 42
var f float64 = float64(i)
var u uint = uint(f)

i := 42
f := float64(i)
u := uint(f)

######
package main

import (
	"fmt"
	"math"
)

func main() {
	var x, y int = 3, 4
	var f float64 = math.Sqrt(float64(x*x + y*y))
	var z uint = uint(f)
	fmt.Println(x, y, z)
}
```

## Constants 常數
> reference: https://tour.golang.org/basics/15

```
package main

import "fmt"

const Pi = 3.14

func main() {
	const World = "世界" // 定義常數
	fmt.Println("Hello", World)
	fmt.Println("Happy", Pi, "Day")

	const Truth = true
	fmt.Println("Go rules?", Truth)
}

```

## For
> reference: https://tour.golang.org/flowcontrol/1

```
package main

import "fmt"

func main() {
	sum := 0
	for i := 0; i < 10; i++ {
		sum += i
	}
	fmt.Println(sum)
}
```

### For is Go's "while"
> reference: https://tour.golang.org/flowcontrol/3

```
package main

import "fmt"

func main() {
	sum := 1
	for sum < 1000 {
		sum += sum
	}
	fmt.Println(sum)
}
```

### 無窮迴圈
> reference: https://tour.golang.org/flowcontrol/4

```
package main

func main() {
	for {
	}
}
```

## if
> reference: https://tour.golang.org/flowcontrol/5

```
package main

import (
	"fmt"
	"math"
)

func sqrt(x float64) string {
	if x < 0 {
		return sqrt(-x) + "i"
	}
	return fmt.Sprint(math.Sqrt(x))

	/** if else

	if v := math.Pow(x, n); v < lim {
		return v
	} else {
		fmt.Printf("%g >= %g\n", v, lim)
	}
	// can't use v here, though
	return lim

	*/

}

func main() {
	fmt.Println(sqrt(2), sqrt(-4))
}

```

### Exercise: Loops and Functions
> https://tour.golang.org/flowcontrol/8

```
package main

import (
	"fmt"
	"math"
)

func Sqrt(x float64) float64 {
	z := x

	for (z * z) > x {
		z -= (z * z - x) / (2 * z)
	}

	return z
}

func main() {
	fmt.Println(Sqrt(2))
	fmt.Println(math.Sqrt(2))
}

```

## switch
> reference: https://tour.golang.org/flowcontrol/9

```
package main

import(
    "fmt"
    "runtime"
 )

 func main() {
     fmt.Print("Go runs on ")
     switch os := runtime.GOOS; os {
     case "darwin":
         fmt.Println("OS X.")
     case "linux":
         fmt.Println("Linux.")
     default:
         // freebsd, openbsd, plan9, windows...
         fmt.Printf("%s.", os)
     }
 }
```

### switch with no condition
> reference: https://tour.golang.org/flowcontrol/11

沒有條件等同於 switch true
```
package main

import (
	"fmt"
	"time"
)

func main() {
	t := time.Now()
	switch {
	case t.Hour() < 12:
		fmt.Println("Good morning!")
	case t.Hour() < 17:
		fmt.Println("Good afternoon.")
	default:
		fmt.Println("Good evening.")
	}
}

```

## Defer
> reference: https://tour.golang.org/flowcontrol/12

defer的function會在return時才執行，且最早的程式碼會在最後才執行

```
package main

import "fmt"

func main() {
	defer fmt.Println("world1")

	defer fmt.Println("world2")
	fmt.Println("hello")

	defer fmt.Println("world3")

	defer fmt.Println("world4")
}

/*
hello
world4
world3
world2
world1
*/
```

### stacking defers
> reference: https://tour.golang.org/flowcontrol/13

```
package main

import "fmt"

func main() {
	fmt.Println("counting")

	for i := 0; i < 10; i++ {
		defer fmt.Println(i)
	}

	fmt.Println("done")
}

```

## Pointers
> reference: https://tour.golang.org/moretypes/1

```
package main

import "fmt"

func main() {
	// 指標未指定時default為nil
	var b *int
	fmt.Println(b) // nil

	i, j := 42, 2701

	p := &i         // point to i
	fmt.Println(*p) // read i through the pointer
	*p = 21         // set i through the pointer
	fmt.Println(i)  // see the new value of i

	p = &j         // point to j
	*p = *p / 37   // divide j through the pointer
	fmt.Println(j) // see the new value of j
}

```

## Array
> reference: https://tour.golang.org/moretypes/6

Array不能resize

```
package main

import "fmt"

func main() {
	var a [2]string
	a[0] = "Hello"
	a[1] = "World"
	fmt.Println(a[0], a[1])
	fmt.Println(a)

	primes := [6]int{2, 3, 5, 7, 11, 13}
	fmt.Println(primes)
}

```

### slices
> reference: https://tour.golang.org/moretypes/7

此方法採reference的方式，所以沒有額外配置記憶體空間，因此修改時兩個array的值都是一樣的。
```
package main

import "fmt"

func main() {
	primes := [6]int{2, 3, 5, 7, 11, 13}

	var s []int = primes[1:4]
	fmt.Println(s)

	// slice
	names := [4]string{
		"John",
		"Paul",
		"George",
		"Ringo",
	}
	fmt.Println(names)

	a := names[0:2]
	b := names[1:3]
	fmt.Println(a, b)

	b[0] = "XXX"
	fmt.Println(a, b)
	fmt.Println(names)

	//這種宣告方式也是slice
	// []type: []int, []string, []struct....
	q := []int{2, 3, 5, 7, 11, 13}
	r := []bool{true, false, true, true, false, true}
	s := []struct {
		i int
		b bool
	}{
		{2, true},
		{3, false},
		{5, true},
		{7, true},
		{11, false},
		{13, true},
	}

	//也可以這樣宣告
	make([]int, 1, 5)

	var slice []int // nil slice
	slice := make([]int, 0) // empty slice
	slice := []int{} // empty slice

	// slice default
	var a [10]int
	a[0:10]//0到10
	a[:10]//到10
	a[0:]//0開始
	a[:] //全部

	// slice len, cap
	s := []int{2, 3, 5, 7, 11, 13}
	printSlice(s)

	// Slice the slice to give it zero length.
	s = s[:0]
	printSlice(s)

	// Extend its length.
	s = s[:4]
	printSlice(s)

	// Drop its first two values.
	s = s[1:3]
	printSlice(s)

}

func printSlice(s []int) {
	fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)

```

### slice make
> reference: https://tour.golang.org/moretypes/13

```
a := make([]int, 5)  // len(a)=5

b := make([]int, 0, 5) // len(b)=0, cap(b)=5

b = b[:cap(b)] // len(b)=5, cap(b)=5
b = b[1:]      // len(b)=4, cap(b)=4
```

### Appending to a slice
> reference: https://tour.golang.org/moretypes/15

```
package main

import "fmt"

func main() {
	var s []int
	printSlice(s)

	// append works on nil slices.
	s = append(s, 0)
	printSlice(s)

	// The slice grows as needed.
	s = append(s, 1)
	printSlice(s)

	// We can add more than one element at a time.
	s = append(s, 2, 3, 4)
	printSlice(s)
}

func printSlice(s []int) {
	fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)
}

```

## Range
> reference: https://tour.golang.org/moretypes/16

```
package main

import "fmt"

var pow = []int{1, 2, 4, 8, 16, 32, 64, 128}

func main() {
	for i, v := range pow {
		fmt.Printf("2**%d = %d\n", i, v)
	}
}
```

```
package main

import "fmt"

func main() {
	pow := make([]int, 10)
	for i := range pow {
		pow[i] = 1 << uint(i) // == 2**i
	}
	for _, value := range pow {
		fmt.Printf("%d\n", value)
	}
}

```

## Exercise: Slices
> reference: https://tour.golang.org/moretypes/18

```
package main

import "golang.org/x/tour/pic"

func Pic(dx, dy int) [][]uint8 {
	data := make([][]uint8, dx)

	for x := 0; x < dx; x++ {
		data[x] = make([]uint8, dy)
	}

	for x := 0; x < dx; x++ {
		for y := 0; y < dy; y++ {
			if x == 127 {
				data[y][x] = 255
			}
		}
	}

	return data
}

func main() {
	pic.Show(Pic)
}
```

## Maps
> https://tour.golang.org/moretypes/19

```
package main

import "fmt"

type Vertex struct {
	Lat, Long float64
}

var m map[string]Vertex

/*
var m = map[string]Vertex{
	"Bell Labs": Vertex{
		40.68433, -74.39967,
	},
	"Google": Vertex{
		37.42202, -122.08408,
	},
}
*/

/* top choice
var m = map[string]Vertex{
	"Bell Labs": {40.68433, -74.39967},
	"Google":    {37.42202, -122.08408},
}
*/

func main() {
	m = make(map[string]Vertex)
	m["Bell Labs"] = Vertex{
		40.68433, -74.39967,
	}
	fmt.Println(m["Bell Labs"])
	fmt.Println(m)
}
```

### Mutating Maps
> reference: https://tour.golang.org/moretypes/22

```
package main

import "fmt"

func main() {
	m := make(map[string]int)

	//新增
	m["Answer"] = 42
	fmt.Println("The value:", m["Answer"])

	//修改
	m["Answer"] = 48
	fmt.Println("The value:", m["Answer"])

	//刪除
	delete(m, "Answer")
	fmt.Println("The value:", m["Answer"])

	//elem, ok = m[key]
	v, ok := m["Answer"]
	fmt.Println("The value:", v, "Present?", ok)
}

```
