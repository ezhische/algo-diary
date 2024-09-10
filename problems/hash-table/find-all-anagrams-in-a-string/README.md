## Find All Anagrams in a String (leetcode 438)  

**Решение**
```go
func findAnagrams(s string, p string) []int {
	result := []int{}
	if len(p) > len(s) {
		return result
	}
	var dictP, slidingDict [26]int
	for _, letter := range p {
		dictP[letter-'a']++
	}
	for i := 0; i < len(p); i++ {
		slidingDict[s[i]-'a']++
	}
	if dictP == slidingDict {
		result = append(result, 0)
	}
	for l := 0; l < len(s)-len(p); l++ {
		slidingDict[s[l]-'a']--
		slidingDict[s[l+len(p)]-'a']++
		if dictP == slidingDict {
			result = append(result, l+1)
		}
	}
	return result
}
```

**Оценка по времени**: О(n)  
Проходим 1 раз по строке 1 раз

**Оценка по памяти**: О(1)  
выделяем доп память на 2 словаря и счётчики

**Описание решения**  
Буду использовать массив из 26 для хранения словаря p и массив в качестве скользящего окна. 
Сначала наберу в словарь первые len(p) символов потом буду сдвигать по 1 и добавять в словарь симол справа и удалять символ слева и сравнивать со словарём p если равен добавлять левый индекс в ответ.
После первой ошибки учёл корнер кейс когда вторая строка длиннее первой, возвращаем пустой массив ответов
