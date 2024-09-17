##  Range Sum Query - Immutable (leetcode 303)  

```go
type NumArray struct {
	store []int
}

func Constructor(nums []int) NumArray {
	store := make([]int, len(nums)+1) // Создаём префиксный массив длинной n+1
	for i := 1; i < len(store); i++ {
		store[i] = store[i-1] + nums[i-1]
	}
	return NumArray{store: store}
}

func (this *NumArray) SumRange(left int, right int) int {
	return this.store[right+1] - this.store[left]
}

/**
 * Your NumArray object will be instantiated and called as such:
 * obj := Constructor(nums);
 * param_1 := obj.SumRange(left,right);
 */
```

**Оценка по времени**: О(n) создание O(1) выполнение  
Для создания префиксного массива нам необходимо пройти весь исходный массив. Получение сумм происходит за константное время  

**Оценка по памяти**: О(n)  
Создаётся префиксный массив по размеру как исходный  

**Описание решения**  
Для быстрого вычисления сумм при создании структуры запишем в массив store[i] сумму до i элемента, тогда получение суммы на дистанции можно будет
вычислить как store[right+1]-store[left]