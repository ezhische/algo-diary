## Design HashMap (leetcode 706)  

```go
type MyHashMap struct {
    store [1000001]int
}


func Constructor() MyHashMap {
    var store [1000001]int 
    for i:=0 ; i < len(store) ; i++ {
        store[i]=-1
    }
    return MyHashMap{store}
}


func (this *MyHashMap) Put(key int, value int)  {
    this.store[key]=value
}


func (this *MyHashMap) Get(key int) int {
    return this.store[key]
}


func (this *MyHashMap) Remove(key int)  {
    this.store[key]=-1
}



/**
 * Your MyHashMap object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Put(key,value);
 * param_2 := obj.Get(key);
 * obj.Remove(key);
 */
```

**Оценка по времени**: О(1)  
Все операции выполняются за константное время

**Оценка по памяти**: О(n)  
Выделяем память под весь диапазон значений.


**Описание решения**  
1. Наивная реализация. На инициализации создаём массив размером max value + 1 и заполняем его -1.
