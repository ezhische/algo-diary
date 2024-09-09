## Top K Frequent Elements (leetcode 347)  

```go
func topKFrequent(nums []int, k int) []int {
    var result []int
    freq:=make(map[int]int)
    for _,val:=range nums {
        freq[val]++
    }
    stat:=make([][]int,len(nums)+1)
    for key,val := range freq {
        stat[val]=append(stat[val],key)
    }
    n:=k
    for i:=len(stat)-1;i>0;i--{
        if len(stat[i])>0{
            n=n-len(stat[i])
            result=append(result,stat[i]...)
            if n<=0 {
                break
            }
        }
    }
    return result[:k]
}
```

**Оценка по времени**: О(n)  
Проходим по массиву 1 раз потом ещё раз по результируещему всего 2n проходов

**Оценка по памяти**: О(n)  
Выделяем памяти дл мамы и для массива в зависимости от n

**Описание решения**  
создаём хештаблицу из значение=сколько раз встретилось
создаём срез срезов длиной как количество элементов +1 и кладём туда элементы где индекс это количество вхождений
Проходим от конца среза и забираем элементы пока не получим k значений

