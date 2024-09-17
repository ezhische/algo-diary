## Maximum Product of Two Elements in an Array (leetcode 1464)  

```go
func maxProduct(nums []int) int {
	var result int
	left, right := 0, len(nums)-1
	for left < right {
		result = max(result, (nums[left]-1)*(nums[right]-1))
		if nums[left] > nums[right] {
			right--
			continue
		}
		left++
	}
	return result
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}
```

**Оценка по времени**: О(n)
Проходим по массиву 1 раз

**Оценка по памяти**: О(1)  
Дополнительная память только на указатели и на произведение

**Описание решения**  
Используем метод двух указателей, один поставим на начало массива, второй на конец. Возмём произведение (nums[left]-1)(nums[rigth]-1). Проверим какой элемент меньше и сдвинем указатель. Сохраним максимальное произведение. Двигаем пока не встретятся указатели.