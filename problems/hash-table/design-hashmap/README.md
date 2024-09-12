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


## Попытка номер 2  

```go
const (
	N = 1007
    A = 7193
)

type KeyValue struct {
	Key   int
	Value int
}

type MyHashMap struct {
	store [N][]KeyValue
}

func Constructor() MyHashMap {
	return MyHashMap{}
}

func (this *MyHashMap) Put(key int, value int) {
	bucket := this.hashfunc(key)
	if len(this.store[bucket]) == 0 {
		this.store[bucket] = []KeyValue{{key, value}}
		return
	}
	for i:=0; i<len(this.store[bucket]);i++ {
		if this.store[bucket][i].Key == key {
			this.store[bucket][i].Value = value
			return
		}
	}
	this.store[bucket] = append(this.store[bucket], KeyValue{key, value})
}

func (this *MyHashMap) Get(key int) int {
	bucket := this.hashfunc(key)
	for _, kv := range this.store[bucket] {
		if kv.Key == key {
			return kv.Value
		}
	}
	return -1
}

func (this *MyHashMap) Remove(key int) {
	bucket := this.hashfunc(key)
	for i, kv := range this.store[bucket] {
		if kv.Key == key {
			this.store[bucket] = append(this.store[bucket][:i], this.store[bucket][i+1:]...)
			return
		}
	}
}

func (this *MyHashMap) hashfunc(key int) int {
	return A* key % N
}
```
**Оценка по времени**: О(1)-O(n) 
Все операции выполняются за константное время в лучшем случае, в худшем O(n) при большом количестве коллизий

**Оценка по памяти**: О(n)  
Выделяем память под N как размер массива и растём при большом количестве коллизий.


**Описание решения**  
1. Простая целочисленная хеш функция где A и N простые числа, позволяет уменьшить размер хранилища и более компактно распологать значения, при коллизиях добавляем в массив значения. Если в ячейке несколько значений ищем по всем значениеям линейным поиском.
