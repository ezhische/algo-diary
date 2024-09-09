## Valid Sudoku (leetcode 36)  

```go
func isValidSudoku(board [][]byte) bool {
    for i:=0;i<9;i++{
        line:=make(map[byte]struct{})
        for _,cell:=range board[i]{
            if cell!='.'{
                if _,ok:=line[cell];ok{
                    return false
                }
                line[cell]=struct{}{}
            }
        }
    }
    for j:=0;j<9;j++{
        collum:=make(map[byte]struct{})
        for i:=0;i<9;i++{
            cell:=board[i][j]
            if cell!='.'{
                if _,ok:=collum[cell];ok{
                    return false
                }
                collum[cell]=struct{}{}
            }
        }
    }
    if !sectorValid(board) {
        return false
    }
	return true
}

func sectorValid(board [][]byte) bool {
    	for x := 0; x < 9; x += 3 {
        for y := 0; y < 9; y += 3 {
            sector := make(map[byte]struct{})
			for j := 0; j < 3; j++ {
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

**Оценка по времени**: О(1)  
Так как у нас фикс матрица и количество операций константно

**Оценка по памяти**: О(1)  
В не зависимости от входа выделаяем одинаковое количество памяти

**Описание решения**  
сначала проверим по линиям и по вертикалям в циклах будем добавлять в каждой линии в хеш сет и во время добавления проверять что нет повторений, то же самое для колонок
Потом пройдём по секторам и проверим каждый сектор