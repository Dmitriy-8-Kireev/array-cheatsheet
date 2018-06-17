# `Array<T>`

Шпаргалка по методам для работы с массивами в JavaScript.

Обозначения:

* ✏️ метод изменяет `this`  - изменяет/модифицирует исходный массив
* 🔒 метод не меняет `this` - не меняет исходный массив / возвращает новый массив на базе исходного
* `callback` - функция обратного вызова, которая передается в массив в качестве аргумента. Используется для обработки очередного элемента массива. 
    
    Стандарт ES3/ES5
    ```js
    var arr = ['яблоко', 'груша', 'колбаса']
    
    arr.forEach(function(element){
        element.toUpperCase(); // ['ЯБЛОКО', 'ГРУША', 'КОЛБАСА']
    })
    ```
    
    Стандарт ES6 и новее
    ```js
    const arr = ['рыба', 'овощи', 'молоко']

    arr.forEach(element => element.toUpperCase()) // ['РЫБА', 'ОВОЩИ', 'МОЛОКО']
    ```


`Array<T>.prototype.*`:

* `concat(...items: Array<T[] | T>): T[]` 🔒 <sup>ES3</sup>

    Метод возвращает новый массив, который образуется от слияния исходного массива ( `this` ) и массивов, переданных в метод в качестве параметров. Параметры без массива обрабатываются так, как если бы они были массивами с 1 элементом.

  ```js
  ['a'].concat('b', ['c', 'd']) //[ 'a', 'b', 'c', 'd' ]
  ```

* `copyWithin(target: number, start: number, end=this.length): this` ✏️ <sup>ES6</sup>

    Метод копирует элементы массива внутри него в позицию, начинающуюся по индексу target. Копия берётся по индексам, задаваемым вторым и третьим аргументами start и end. `arr.copyWithin(target, start, end)`

  ```js
  ['a', 'b', 'c', 'd'].copyWithin(0, 2, 4) // [ 'c', 'd', 'c', 'd' ]
  ```

* `entries(): Iterable<[number, T]>` 🔒 <sup>ES6</sup>

  Метод возвращает итератор с парой [индекс, элемент], или [ключ, значение]

  ```js
  Array.from(['a', 'b'].entries()) // [ [ 0, 'a' ], [ 1, 'b' ] ]
  ```

* `every(callback: (value: T, index: number, array: Array<T>) => boolean, thisArg?: any): boolean` 🔒 <sup>ES5</sup>

    Метод обрабатывает все элементы массива. Возвращает `true` если коллбэк вернет `true` для каждого элемента. Останавливается как только какой-либо элемент вернет `false`.

  ```js
  [1, 2, 3].every(x => x > 0)   // true
  [1, -2, 3].every(x => x > 0)  // false
  ```

* `fill(value: T, start=0, end=this.length): this` ✏️ <sup>ES6</sup>

    Данный Метод заполняет все элементы массива от начального до конечного значением, переданным в качестве параметра.

  ```js
  [0, 1, 2].fill('a') // [ 'a', 'a', 'a' ]
  ```

* `filter(callback: (value: T, index: number, array: Array<T>) => any, thisArg?: any): T[]` 🔒 <sup>ES5</sup>

    Возвращает массив, который состоит из тех элементов, для которых `callback` вернет `true`

  ```js
  [1, -2, 3].filter(x => x > 0) // [ 1, 3 ]
  ```

* `find(predicate: (value: T, index: number, obj: T[]) => boolean, thisArg?: any): T | undefined` 🔒 <sup>ES6</sup>

    Возвращает первое найденное значение, которое удовлетворяет условию, переданному в `callback`, в противном же случае, метод вернет `undefined`

  ```js
  [1, -2, 3].find(x => x < 0) // -2
  [1, 2, 3].find(x => x < 0)  // undefined
  ```

* `findIndex(predicate: (value: T, index: number, obj: T[]) => boolean, thisArg?: any): number` 🔒 <sup>ES6</sup>

    Результатом выполнения данного метода будет индекс первго элемента в массива, который удовлетворяет условию в `callback`. Если условие не выполнено, вернется `-1`

  ```js
  [1, -2, 3].findIndex(x => x < 0) // 1
  [1, 2, 3].findIndex(x => x < 0)  //-1
  ```

* `forEach(callback: (value: T, index: number, array: Array<T>) => void, thisArg?: any): void` 🔒 <sup>ES5</sup>

    Метод вызовет `callback` для каждого элемента массива

  ```js
  ['a', 'b'].forEach((x, i) => console.log(x, i))
  // 'a' 0
  // 'b' 1
  ```

* `includes(searchElement: T, fromIndex=0): boolean` 🔒 <sup>ES2016</sup>

    Метод вернет `true` или `false`, в зависимости от того содержится ли искомый элемент в массиве или нет. Элементы проверяется через строгое равенство `===`. NaN === NaN

  ```js
  [0, 1, 2].includes(1)   // true
  [0, 1, 2].includes(5)   // false
  ```

* `indexOf(searchElement: T, fromIndex=0): number` 🔒 <sup>ES5</sup>

  Вернет индекс первого подходящего элемента, равного (строгое равенство) искомому элементу. В противном случае вернет `-1`. Если указан параметр `fromIndex`, то поиск начинается с него, если не указан, то от начала массива. `arr.indexOf(searchElement, fromIndex)`

  ```js
  ['a', 'b', 'a'].indexOf('a')    // 0
  ['a', 'b', 'a'].indexOf('a', 1) // 2
  ['a', 'b', 'a'].indexOf('c')    // -1
  ```

* `join(separator = ','): string` 🔒 <sup>ES1</sup>

  Creates a string by concatenating string representations of all elements, separating by `separator`.
    Данный метод возвращает строку, в которой содержатся все элементы массива, разделенные `separator`. `arr.join(separator)`

  ```js
  ['a', 'b', 'c'].join()      // 'a,b,c'
  ['a', 'b', 'c'].join('##')  // 'a##b##c'
  ```

* `keys(): Iterable<number>` 🔒 <sup>ES6</sup>

    Метод возвращает итератор, содержащий ключи индекса в исходном массиве

  ```js
  ['a', 'b'].keys()]  // [ 0, 1 ]
  ```

* `lastIndexOf(searchElement: T, fromIndex=this.length-1): number` 🔒 <sup>ES5</sup>

    Вернет индекс последнего подходящего элемента, равного (строгое равенство) искомому элементу. В противном случае вернет `-1`. Если указан параметр `fromIndex`, то поиск начинается с него. `arr.indexOf(searchElement, fromIndex)`

  ```js
  ['a', 'b', 'a'].lastIndexOf('a')    // 2
  ['a', 'b', 'a'].lastIndexOf('a', 1) // 0
  ['a', 'b', 'a'].lastIndexOf('c')    // -1
  ```

* `map<U>(callback: (value: T, index: number, array: ReadonlyArray<T>) => U, thisArg?: any): U[]` 🔒 <sup>ES5</sup>

    Метод вернет новый массив, в котором к каждому элементу будет применен результат вызова `callback`

  ```js
  [1, 2, 3].map(x => x * 2)        // [ 2, 4, 6 ]
  ['a', 'b', 'c'].map((x, i) => i) // [ 0, 1, 2 ]
  ```

* `pop(): T | undefined` ✏️ <sup>ES3</sup>

    Удаляет из массива последний элемент, и затем возвращает его. То есть, метод по сути работает как стек(stack - структура данных).

  ```js
  const arr = ['a', 'b', 'c'];
  arr.pop()         // 'c'
  console.log(arr)  // [ 'a', 'b' ]
  ```

* `push(...items: T[]): number` ✏️ <sup>ES3</sup>

    Метод добавит элемент/элементы в конец массива. То есть, он обрабатывает конец массива как стек. Возвращает длинну массива после изменения.

  ```js
  const arr = ['a', 'b'];
  arr.push('c', 'd')  // 4
  console.log(arr)    // [ 'a', 'b', 'c', 'd' ]
  ```

* `reduce<U>(callback: (state: U, element: T, index: number, array: T[]) => U, firstState?: U): U` 🔒 <sup>ES5</sup>

    Данный метод по сути обрабатывает каждый элемент массива, с сохранением промежуточного состояния. Метод начинает работу с элемента с индексом 0, идя вперед. Если не указано `firstState`, отсчет идет с 0 индекса. Последнее значание является результатом вызова метода. 

  ```js
  [1, 2, 3].reduce((state, x) => state + String(x), '')   // '123'
  [1, 2, 3].reduce((state, x) => state + x, 0)            // 6
  ```

* `reduceRight<U>(callback: (state: U, element: T, index: number, array: T[]) => U, firstState?: U): U` 🔒 <sup>ES5</sup>

    Метод работает аналогично `.reduce()`, но отсчет элементов идет начиная с конца массива.

  ```js
  [1, 2, 3].reduceRight((state, x) => state + String(x), '') // '321'
  ```

* `reverse(): this` ✏️ <sup>ES1</sup>

    Перписывает массив, меняя индексы элементов местами, т.е. последний = первый, второй = предпоследний и т.д.

  ```js
  const arr = ['a', 'b', 'c'];
  arr.reverse()     // [ 'c', 'b', 'a' ]
  console.log(arr)  // [ 'c', 'b', 'a' ]
  ```

* `shift(): T | undefined` ✏️ <sup>ES3</sup>

    Удаляет и затем возвращает первый жлемент массива. Противополжен методу `.unshift()`.

  ```js
  const arr = ['a', 'b', 'c'];
  arr.shift()       // 'a'
  console.log(arr)  // [ 'b', 'c' ]
  ```

* `slice(start=0, end=this.length): T[]` 🔒 <sup>ES3</sup>

    Возвращает новый массив, который содержит элементы исходного, начиная со `start` по (не вкл.) `end`. `arr.slice(start,end)`

  ```js
  ['a', 'b', 'c', 'd'].slice(1, 3)  // [ 'b', 'c' ]
  ['a', 'b'].slice()                // копия [ 'a', 'b' ]
  ```

* `some(callback: (value: T, index: number, array: Array<T>) => boolean, thisArg?: any): boolean` 🔒 <sup>ES5</sup>

    Метод вернет `true` если хотя бы один элемент удовлетворит условию в `callback`. Останавливается, как только возвращается `true`

  ```js
  [1, 2, 3].some(x => x < 0)    // false
  [1, -2, 3].some(x => x < 0)   // true
  ```

* `sort(compareFn?: (a: T, b: T) => number): this` ✏️ <sup>ES1</sup>

    Метод сортирует элементы массива и возвращает его.  Порядок сортировки задается с помощью функции сравнения, которая возвращает число:

        * Отрицательное, если `a < b`
        * Ноль, если `a === b`
        * Положительное, если`a > b`

    *Примечание: в движке V8, в качестве алгоритма сортировки используется 2 метода. Для больших массивов - быстрая сортировка, для небольших - сортировка вставками*

  ```js
  [3, 1, 2].sort((a, b) => a - b)                               // [ 1, 2, 3 ]
  ['b', 'a', 'c'].sort((a, b) => a < b ? -1 : a > b ? +1 : 0)   // [ 'a', 'b', 'c' ]
  ```

* `splice(start: number, deleteCount=this.length-start, ...items: T[]): T[]` ✏️ <sup>ES3</sup>

    Начиная с индекса `start` он удаляет опрпделенное кол-во элементов `deleteCount`, и вставляет `items`. Возвращает измененный исходный массив `array.splice(start, deleteCount,[item1])`
  ```js
  const arr = ['a', 'b', 'c', 'd'];
  arr.splice(1, 2, 'x', 'y')    // [ 'b', 'c' ]
  console.log(arr)              // [ 'a', 'x', 'y', 'd' ]
  ```

* `toString(): string` 🔒 <sup>ES1</sup>

    Метод возвращает строку, которя включает все элементы массива, разделенные запятой.

  ```js
  [1, 2, 3].toString()        // '1,2,3'
  ['a', 'b', 'c'].toString()  // 'a,b,c'
  [].toString()               //''
  ```

* `unshift(...items: T[]): number` ✏️ <sup>ES3</sup>
  
    Вставляет элемент/элементы в начало массива и возвращает его длинну после каких-либо действий с ним.
  ```js
  const arr = ['c', 'd'];
  arr.unshift('e', 'f')     // 4
  console.log(arr)          //[ 'e', 'f', 'c', 'd' ]
  ```

## Подробная инофрмация

* Детальное опписание методов для работы с массивами в ECMAScript можно найти тут: http://exploringjs.com
* Методы работы с массивами в ES6 “[Array operations and holes](http://exploringjs.com/es6/ch_arrays.html#_array-operations-and-holes)”.

<!-- TODO: @@iterable, constructor, .length -->

## Источники

* https://github.com/Microsoft/TypeScript/blob/master/lib/lib.es6.d.ts
* MDN - [Mozilla Development Network](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Array/prototype)
* Специализации языка ECMAScript (JavaScript)
