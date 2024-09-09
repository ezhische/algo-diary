```go
func isValidSudoku(board [][]byte) bool {
	for x := 0; x < 9; x += 3 {
		for y := 0; y < 9; y += 3 {
			for j := 0; j < 3; j++ {
				sector := make(map[byte]struct{})
				for i := 0; i < 3; i++ {
					cell := board[x+i][y+j]
					if cell != '.' {
						if _, ok := sector[cell]; ok {
							return false
						}
						sector[cell] = struct{}{}
					}
				}
			}
		}
	}
	return true
}
```

Проверял только сектора, неправильно понял условие задачи.