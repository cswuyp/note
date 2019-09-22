单元测试是质量保证十分重要的一环，好的单元测试不仅能及时地发现问题，更能够方便地调试，提高生产效率，所以很多人认为写单元测试是需要额外的时间，会降低生产效率，是对单元测试最大的偏见和误解

go 语言原生支持了单元测试，使用上非常简单，测试代码只需要放到以 _test.go 结尾的文件中即可。golang的测试分为单元测试和性能测试，单元测试的测试用例以 Test 开头，性能测试以 Benchmark 开头

举个例子
实现排列组合函数对应的单元测试和性能测试

实现排列组合函数
```
// combination.go

package hmath

func combination(m, n int) int {
    if n > m-n {
        n = m - n
    }

    c := 1
    for i := 0; i < n; i++ {
        c *= m - i
        c /= i + 1
    }

    return c
}
```
实现单元测试
选择准备单元测试的代码段右键Go:Generate Unit Tests for Function,会自动生成以下文件，我们只需要在 TODO: Add test cases. 
里面加上我们的测试用例就行了
```
// combination_test.go

package hmath

import "testing"

func Test_combination(t *testing.T) {
	type args struct {
		m int
		n int
	}
	tests := []struct {
		name string
		args args
		want int
	}{
		// TODO: Add test cases. 在这里添加你的单元测试用例
		//添加用例，格式一
		{"1", args{m: 1, n: 0}, 1},
		//添加用例，格式二
		{name: "1", args: args{m: 1, n: 0}, want: 1},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			if got := combination(tt.args.m, tt.args.n); got != tt.want {
				t.Errorf("combination() = %v, want %v", got, tt.want)
			}
		})
	}
}

```

运行测试
```
go test combination_test.go combination.go           # 单元测试
go test --cover combination_test.go combination.go   # 单元测试覆盖率
```

增加性能测试
```
// combination_test.go

package hmath

import "testing"

func Test_combination(t *testing.T) {
	type args struct {
		m int
		n int
	}
	tests := []struct {
		name string
		args args
		want int
	}{
		// TODO: Add test cases. 在这里添加你的单元测试用例
		//添加用例，格式一
		{"1", args{m: 1, n: 0}, 1},
		//添加用例，格式二
		{name: "1", args: args{m: 1, n: 0}, want: 1},
	}
	for _, tt := range tests {
		t.Run(tt.name, func(t *testing.T) {
			if got := combination(tt.args.m, tt.args.n); got != tt.want {
				t.Errorf("combination() = %v, want %v", got, tt.want)
			}
		})
	}
}
// 性能测试
func BenchmarkCombination(b *testing.B) {
    // b.N会根据函数的运行时间取一个合适的值
    for i := 0; i < b.N; i++ {
        combination(i+1, rand.Intn(i+1))
    }
}

// 并发性能测试
func BenchmarkCombinationParallel(b *testing.B) {
    // 测试一个对象或者函数在多线程的场景下面是否安全
    b.RunParallel(func(pb *testing.PB) {
        for pb.Next() {
            m := rand.Intn(100) + 1
            n := rand.Intn(m)
            combination(m, n)
        }
    })
}
```
运行测试：
```
go test -bench=. combination_test.go combination.go  # 性能测试
```

