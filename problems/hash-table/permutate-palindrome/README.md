## Palindrome Permutation (leetcode 266)  

**Решение**
```go
func canPermutatePalindrome(s string) bool {
	letters := make(map[byte]int)
	for i := 0; i < len(s); i++ {
		letters[s[i]]++
	}
	notOven := 0
	for _, val := range letters {
		notOven += val % 2
	}
	return notOven <= 1
}
```

**Оценка по времени**: О(n)  
где n- длина строк потому что проходим по строке 1 

**Оценка по памяти**: О(k)  
где k количество символов в строке 

**Описание решения**  
Соберу в Map все буквы а потом посчитаю количество посчитаю количество чётных и если нечётных будет больше 1 то false 
