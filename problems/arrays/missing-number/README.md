## Missing Number (leetcode 268)  

```go
func missingNumber(nums []int) int {
    var result int
    for i:=1;i<=len(nums);i++ {
        result+=i
        result-=nums[i-1]
    }
    return result
}
```

**Оценка по времени**: О(n)  
Нужно пройтись по всему массиву

**Оценка по памяти**: О(1)  
Выделяем только переменные для хранения суммы, не зависит от размера входного массива

**Описание решения**  
Самый простой и быстрый способ это вычесть все числа в массиве и добавить туда все числа от 1 до n где n это длинна массива. Самый простой и очевидный вариант решения. 
Как второй вариант можно сложить все значения и вычесть из суммы арифметической последовательности расчитаную как n(1+n)/2 

## Второй вариант
```go
func missingNumber(nums []int) int {
    var numsSum int
    for i:=0;i<len(nums);i++ {
        numsSum+=nums[i]
    }
    return len(nums)*(len(nums)+1)/2 - numsSum
}
```
## Третий вариант использовать тот факт что a XOR a  = 0 и сделать XOR переменной элементами массива и всеми числами от 1 до n

```go
func missingNumber(nums []int) int {
    var missing int    
    for i:=1;i<=len(nums);i++{
        missing^=nums[i-1]
        missing^=i
    }
    return missing
}
```