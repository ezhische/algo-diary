## Line reflection (leetcode 356)  

**Решение**
```go
func isReflected(points [][]int) bool {
	maxX := math.MinInt64
	minX := math.MaxInt64
	pointsMap := make(map[[2]int]struct{})
	for _, point := range points {
		if point[0] > maxX {
			maxX = point[0]
		}
		if point[0] < minX {
			minX = point[0]
		}
		var pointArr [2]int
		copy(pointArr[:], point)
		pointsMap[pointArr] = struct{}{}
	}
	for point := range pointsMap {
		if _, ok := pointsMap[[2]int{maxX + minX - point[0], point[1]}]; !ok {
			return false
		}
	}
	return true
}
```

**Оценка по времени**: О(n)  
Проходим 1 раз по массиву потом 1 раз по сету n+n

**Оценка по памяти**: О(n)  
выделяем доп память на массив и 2 переменных

**Описание решения**  
Найдём крайние значения X минимум и максимум, паралельно сохраним каждую точку в hash-set, пройдём по set и проверим что существует точка с maxX+minX-X для каждой точки. 
Во время сохранения в hash set дублирующие точки уберутся
