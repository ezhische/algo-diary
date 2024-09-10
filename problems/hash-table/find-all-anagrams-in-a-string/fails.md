## Неудачные попытки  
```go
func findAnagrams(s string, p string) []int {
	result := []int{}
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

Не проверил что len(p)>len(s)