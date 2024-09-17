## Longest Continuous Increasing Subsequence (leetcode 674)  

```go
func findLengthOfLCIS(nums []int) int {
	maxCount, count := 1, 1
	for i := 1; i < len(nums); i++ {
		if nums[i-1] < nums[i] {
			count++
            maxCount = max(maxCount, count)
			continue
		}
		count = 1
	}
	return maxCount
}
func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}
```

**Оценка по времени**: О(n)  
Проходим по всему массиву, количество итераций, количество элементов в массиве

**Оценка по памяти**: О(1)  
Нужна память только для максимального значения и счётчика.

**Описание решения**  
Возмём счётчик и будем его увеличивать если выполняется условие возрастания, если не выполняется то обновляем максимум и сбрасываем счётчик
Минимально возможная последовательность это 1 она сразу как бы и возрастающая и не возрастающая потому изначально счётчик = 1 и сброс на 1
1. Счетчик 1
2. Идём по массиву если nums[i]< num[i-1] то плюсуюем счетчик  и сохраняем максимум иначае сбрасываем в 1
3. После прохода по массиву возвращаем счётчик


**Чуть более быстырй вариант за счёт уменьшения вызова max**
```go
func findLengthOfLCIS(nums []int) int {
    var maxCount int
    count:=1
    for i:=1;i < len(nums); i++{
        if nums[i-1]<nums[i] {
            count++
        } else {
            maxCount=max(maxCount,count)
            count = 1
        }
    }
    return max(maxCount,count)
}

func max(a,b int) int {
    if a>b {
        return a
    }
    return b
}
```