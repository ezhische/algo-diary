## Group Anagram (leetcode 49)  

**Решение**
```go
func groupAnagrams(strs []string) [][]string {
	var result [][]string
	groups := make(map[[26]int][]string)
	for _, word := range strs {
		var dict [26]int
		for _, letter := range word {
			dict[letter-'a']++
		}
		groups[dict] = append(groups[dict], word)
	}
	for _, group := range groups {
		result = append(result, group)
	}
	return result
}
```

**Оценка по времени**: О(n*k)  
где n это количество слов и k - длина слов

**Оценка по памяти**: О(n*k)  
выделю память для словарей и результруещей мапы опять же количество зависит от длины слов

**Описание решения**  
Сделаю словарь в виде массива из 26 элементов по 1 на каждую букву, все слова с одинаковыми массивами будут анаграмами. Сложу все слова в мапу где ключ это словарь, пройду по мапе и добавлю все группы в результат.