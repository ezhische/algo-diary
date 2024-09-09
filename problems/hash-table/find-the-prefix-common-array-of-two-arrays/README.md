## Find the Prefix Common Array of Two Arrays (leetcode  2657)  

```go
func findThePrefixCommonArray(A []int, B []int) []int {
	result := make([]int, 0, len(A))
	freq := make([]int, len(A)+1)
	count := 0
	for i := 0; i < len(A); i++ {
		freq[A[i]]++
		freq[B[i]]++
		if A[i] == B[i] {
			count++
			result = append(result, count)
			continue
		}
		count += freq[A[i]]/2 + freq[B[i]]/2
		result = append(result, count)
	}
	return result
}
```

**Оценка по времени**: О(n)  
Проходим по массиву 1 раз

**Оценка по памяти**: О(n)  
Выделяем памяти для массива как n

**Описание решения**  
Создаём массив из n+1 и счётчик проходим по двум массивам парралельно. При проходе +1 к индексу который равен значению элемента. 
Проверяем если элементы равны то добавляем +1 к счётчику и добавляем счётчик в массив ответа после идём на след итерацию, 
если нет, то проверяем каждый элемент его значение в массиве если == 2 то счётчик + 1 после проверки добавляем счётчик к ответу и идём дальше. 