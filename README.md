# JS-intensive-33

## HomeWork №1

  1\. Options - метод, который представляет запрос информации об опциях соединения, доступных в цепочке запросов/ответов, идентифицируемой запрашиваемым URI (Request-URI). Этот метод позволяет клиенту определять опции и/или требования, связанные с ресурсом, или возможностями сервера, но не производя никаких действий над ресурсом и не инициируя его загрузку.
Использается в качестве предварительного запроса (CORS), помогая браузеру узнать, можно ли осуществить запрос до его обработки.

  У OPTIONS нет тела, но есть три заголовка:  
   - Origin содержит именно источник (домен, протокол или порт), без пути.  
   - Access-Control-Request-Method содержит HTTP-метод «прочего» запроса.  
   - Access-Control-Request-Headers предоставляет список его «непростых» HTTP-заголовков.
    
  Если сервер согласен принять такой запрос, то он должен ответить без тела, со статусом 200 и с заголовками, которые должны содержать:  
  - Access-Control-Allow-Origin — разрешенный источник.  
  - Access-Control-Allow-Methods — разрешенные методы.  
  - Access-Control-Allow-Headers — список разрешенных заголовков.
    
  Кроме того, заголовок Access-Control-Max-Age может указывать количество секунд, на которое нужно кешировать разрешения. 

  2\. Протокол QUICK построен поверх протокола UDP. Поверх же QUIC работает небольшая прослойка HTTP/2 API, используемая для общения с удалёнными серверами. Она меньше полной реализации HTTP/2, поскольку мультиплексирование и установка соединения уже реализованы в QUIC. Остаётся лишь реализация протокола HTTP. Данный протокол имеет следующие ключевые особенности:  
    - QUIC безопасен по умолчанию, что делает соединение всегда шифрованным, а также позволяет быстрее делать первоначальное соединение (вместо трёхстороннего рукопожатия TCP и TLS - трёхстороннее рукопожатие только QUIC);  
    - Протокол QUIC решает проблему блокировки начала очереди, который не требует соблюдения порядка обработки принимаемых пакетов;  
    - Также фичей QUIC является превентивная коррекция ошибок (Forward Error Correction, FEC). Каждый пересылаемый пакет содержит в себе некоторое количество данных других пакетов, что позволяет реконструировать любой потерянный пакет по данным в его соседях, без необходимости запрашивать переотправку потерянного пакета и дожидаться его содержимого;  
    - QUIC вводит понятие идентификатора соединения, называемого Connection UUID. Появляется возможность перейти с WiFi на LTE с сохранением Connection UUID, таким образом избежав затрат на пересоздание соединения;  
  
  3\. Для отмены http-запроса существует специальный встроенный объект: AbortController, который можно использовать для отмены не только fetch, но и других асинхронных задач.
  Использовать его достаточно просто. Cоздаётся контроллер. Он имеет единственный метод abort() и единственное свойство signal. Далее передается свойство signal опцией в метод fetch. Затем, чтобы прервать выполнение fetch, необходимо вызвать controller.abort(): 

  ```javascript
    let controller = new AbortController();
    
    fetch(url, { signal: controller.signal });
    controller.abort();*
  ```
  
  4\.
  ```javascript
      const stringOne = 'str';
      const stringTwo = String(1);

      const numOne = 1;
      const numTwo = Number(1);

      const boolOne = true;
      const boolTwo = Boolean('');

      const nullOne = null;

      const undefinedOne = undefined;
      let undefinedTwo;

      const bigIntOne = 1000n;
      const bigIntTwo = BigInt(1000);

      const symbolOne = Symbol('Sym');

  ```

  5\. Во время инициализации переменные объявленные через let и const попадают во временную мёртвую зону, поэтому они не видны интерпретатору до их объявления.

  6\.
  ```javascript
    const res = "B" + "a" + (1 - "hello");
    console.log(res); //'BaNaN - результатом выражения (1 - "hello") будет NaN так как JS пытается строку преобразовать в число'

    const res2 = (true && 3) + "d";
    console.log(res2); //'3d - оператор && вернет значение последнего операнда, то есть 3' 

    const res3 = Boolean(true && 3) + "d";
    console.log(res3); //'trued - функция Boolean(3) вернет true';
  ```
      

## HomeWork №2

1\.
```javascript
const counterOne = { count: 1 };  // создание объекта литеральным способом

// Создание объектов с помощью встроенных методов объекта
const counterTwo = Object.create(null);
counterTwo.count = 1;

const counterThree = Object.create({}, {
  count: {
    value: 1,
    configurable: true,
    enumerable: true,
    writable: true,
  }
})

const counterFour = Object.assign({}, { count: 1 });
const counterFive = Object.assign({}, counterFour);



const counterSix = Object.defineProperty({}, 'count', {
  value: 1,
  configurable: true,
  enumerable: true,
  writable: true,
});

const counterSeven = Object.defineProperties({}, {
  count: {
    value: 1,
    configurable: true,
    enumerable: true,
    writable: true,
  },
});


//Создание объектов с помощью конструктора объекта
const counterEight = new Object();
counterEight.count = 1;

function CreateCounter() {
  this.count = 1;
}
const counterNine = new CreateCounter();

class Counter {
  constructor() {
    this.count = 1;
  }
}
const counterTen = new Counter();

```

2\.
```javascript
const counter = {count: 1};

const counterCloneOne = Object.assign({}, counter); //поверхностное копирование

const counterCloneTwo = { ...counter }; //поверхностное копирование

const counterDeepCloneOne = structuredClone(counter); //глубокое копирование 

const counterDeepCloneTwo = JSON.parse(JSON.stringify(counter)) //глубокое копирование

```

3\.
```javascript
// Function Declaration
function makeCounterOne() {
  return { count: 1 };
}

// Function Expression
const makeCounterTwo = function() {
  return { count: 1 };
}

// Arrow Function
const makeCounterThree = () => { count: 1 };

// Named Function Expression
const makeCounterFour = function makeCounter() {
  return { count: 1 };
}

```

4\.
```javascript
const deepEqual = (obj1, obj2) => {
  if(typeof obj1 !== 'object' || typeof obj2 !== 'object') return false;
  if(Object.keys(obj1).length !== Object.keys(obj2).length) return false;
  if(obj1 === obj2) return 'Ссылаются на один и тот же объект';

  for(key in obj1) {
    if(typeof obj1[key] === 'object') {
      if(deepEqual(obj1[key], obj2[key])) continue

      return false
    }
    if(obj1[key] !== obj2[key]) {
      return false
    }
  }

  return true
}


const obj1 = {
  here: {
    is: 'on',
    other: '1',
  },
  object: 'X',
};

const obj2 = {
  here: {
    is: 'on',
    other: '2',
  },
  object: 'X',
};

console.log(deepEqual(obj1, obj2)) //false

```
5\.
```javascript
const reverseStr1 = str => {
  let resStr = '';
  str.split('').forEach(char => resStr = char + res);

  return res;
}

const reverseStr2 = str => str.split('').reverse().join('');

const reverseStr3 = str => str.split('').reduce((resStr, char) => char + resStr, '')

```


## HomeWork №3

1\. Массивы в Javascript являются неправильными и совмещают в себе сразу несколько структур данных(стеки, очереди, упорядоченные списки), так как по задумке длина массива должна быть неизменной, т.е для того чтобы добавить элемент в массив, нужно создать новый массив длиннее старого на один элемент, затем скопировать в него все значения старого массива и качестве нового элемента указать новое значение.

2\.
```javascript
const obj = { 
  item: "some value" 
};

function logger() {
  console.log(`I output only external context: ${this.item}`);
};

logger.apply(obj);

logger.call(obj);

const bindedLogger = logger.bind(obj);
bindedLogger();

```

3\.
```javascript
Function.prototype.myBind = function(context) {
  const thisFunc = this;
  const args = Array.from(arguments).slice(1);
 
  return function() {
    return thisFunc.apply(context, args);
  }
}

```


## HomeWork №4

1\.
 - Сортировка выбором (Selection sort) - асимптотика O(n^2) в лучшем, среднем и худшем случае.
 - Сортировка вставками (Insertion sort) - асимптотика в среднем и худшем случае – O(n^2), в лучшем – O(n);
 - Пузырьковая сортировка (Bubble sort) - асимптотика в худшем и среднем случае – O(n^2), в лучшем случае – O(n);
 - Шейкерная сортировка (Shaker sort) - асимптотика у алгоритма такая же, как и у сортировки пузырьком, однако реальное время работы лучше;
 - Сортировка расческой (Comb sort) - в лучшем случае асимптотика равна O(n*logn), в худшем – O(n^2);
 - Сортировка деревом (Tree sort) - асимптотика будет равна O(n*logn) в худшем, среднем и лучшем случае;
 - Сортировка слиянием (Merge sort) - слияние работает за O(n), уровней всего logn, поэтому асимптотика O(n*logn);
 - Timsort - гибридная сортировка, совмещающая сортировку вставками и сортировку слиянием. Асимптотика: O(n) в лучшем случае и O(n*logn) в среднем и худшем случае;
 - Сортировка кучей (Heap sort) - асимптотика O(n*logn) в худшем, среднем и лучшем случае.
 - Быстрая сортировка (Quick sort) - асимптотика O(n*logn) в среднем и лучшем случае, в худшем - O(n^2).
 - Гномья сортировка (Gnome sort) - алгоритм похож на сортировку вставками. Поддерживаем указатель на текущий элемент, если он больше предыдущего или он первый — смещаем указатель на позицию вправо, иначе меняем текущий и предыдущий элементы местами и смещаемся влево.

 2\.

#### ВЫРАЖЕНИЯ:

Выражение - любой корректный блок кода, который возвращает значение.

Категории выражений:
|||
|:-|:-|
|`Арифметические`|вычисляются в число, используют арифметические операторы|
|`Строковые`|вычисляются в текстовую строку, используют строковые операторы|
|`Логические`|вычисляются в true или false, используют логические операторы|
|`Основные`|базовые ключевые слова (`this`) и основные выражения в JavaScript|
|`Левосторонние`|значениям слева назначаются значения справа|


#### ОПЕРАТОРЫ:

Оператор - это символы или ключевые слова, которые указывают движку JavaScript на выполнение каких-либо действий.

По количеству операндов:
|||
|:-|:-|
|`Унарные`| `+` (приведение к числу), `-` (противоположное число), `++` , `delete`, ...|
|`Бинарные`|`===`, `+` (сложение), ...|
|`Тернарные`|`? :`|

По внешнему представлению:
|||
|:-|:-|
|`символьные`| `*`, `!` `<<`, ...|
|`текстовые`| `instanceof`, `delete`, `new`, `typeof`, `void` (определяет выражение, которое должно быть вычислено без возвращения результата), `break`, ...|

По функции:
|||
|:-|:-|
|`Присваивания`| `=`, `+=`, `-=`, `%=`, `\|\|=`, ...|
|`Cравнения`|`==`, `===`, `!=`, `!==`, `>`, `<`, `>=`, `<=`.
|`Арифметические`| `+` (унарный и бинарный), `-` (унарный и бинарный), `*`, `/`, `%`, `**`, `++`, `--`
|`Логические`| `&&`, `\|\|`,`!`,`??` (оператор нулевого слияния)|
|`Строковые`| операторы сравнения, бинарный `+`, `+=`|
|`Битовые (поразрядные)`|`~` ('не'),  `<<`, `>>`, `>>>` (сдвиг вправо с заполнением нулями), `&` (возвращает единицу в каждой битовой позиции, для которой соответствующие биты обеих операндов являются единицами), `^` (возвращает единицу в каждой битовой позиции, для которой только один из соответствующих битов операндов является единицей) и др.
|`Операторы отношения` - сравнивает свои операнды и возвращает результат сравнения в виде булева значения|`in` (возвращает `true`, если указанный объект имеет указанное свойство), `instanceof` - возвращает true, если заданный объект является объектом указанного типа.
|`Удаления`|`delete` - выполняет удаление объекта, свойства объекта, или элемента массива с заданным индексом, а так же переменных, объявленных неявно. Возвращает `true` если выполнение операции возможно, иначе - `false`.
|`Создания объекта`| `new`|
|`Группировки`|`( )`|
|`Оператор запятая`|`,` - вычисляет оба операнда и возвращает значение последнего|


#### ЦИКЛЫ:

Цикл — это повторяющаяся последовательность действий.\
Цикл состоит из условия и тела цикла.

- `for` - для выполнения блока кода заданное количество раз.
- `while` - для выполнения блока кода пока заданное условие остается истинным.
- `do ... while` - выполнится минимум 1 раз, далее выполняется, пока заданное условие остается истинным.
- `for ... in` - для итерации свойств объекта, проходит по именам свойств. В цикле будут перечислены не только собственные свойства объекта, но и все перечисляемые свойства из прототипа объекта и прототипа прототипа и т.д.
- `for ... of` - для перебора итерируемых сущностей, проходит по значениям свойств


3\.
```javascript
// создаем объект person литеральным способом
const person = {
  name: 'Persie',
}

// с помощью сеттера __proto__ устанавливаем свойство [[Prototype]] в значение person
const person2 = {
  name: 'Peter'
  __proto__: person,
}

// либо создаем объект person2 и устанавливаем свойство [[Prototype]] с помощью встроенного метода Object.create

const person2 = Object.create(person, {
  name: {
    value: 'Peter',
  }
})

//Также еще можно установить свойство [[Prototype]] с помощью метода setPrototypeOf
Object.setPrototypeOf(person2, person)

person.logInfo = function() {
  return `name: ${this.name}`;
}

//Теперь создадим объект person с помощью конструктора

function Person(name) {
  this.name = name
}

const person = new Person('Persie')

function Person2(name) {
  Person.call(this, name);
}

//реализуем прототипное наследование

Person2.prototype = Object.create(Person.prototype);

Person2.prototype.construtor = Person2 //Так как перезаписали выше Person2.prototype нужно восстановить свойство construtor, чтобы оно снова ссылалось на Person2

Person.prototype.loginfo = function() {
  return `name: ${this.name}`;
}

const person2 = new Person2('Peter');

```
4\.
```javascript
class Person {
  constructor(name) {
    this.name = name;
  }

  logInfo() {
        return `name: ${this.name}`;
  }
}

class PersonThree extends Person {
  constructor(name) {
    super(name);
  }
      
  get name() {
    return this.name;
  }

  set name(value) {
    this.name = value;
  }
}
```

5\.
```javascript
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9];
const total = 13;

function firstSum(numsArr, total) {
  for(let i = 0; i < numsArr.length; i++) {
    for(let j = i+1; j < numsArr.length; j++) {
      if(numsArr[i] + numsArr[j] === total) {
        return [numsArr[i], numsArr[j]]
      }
    }
  }
    
  return [];
}

firstSum(arr, total) // [4, 9]

//Сложность данного алгоритма O(n^2)

//Также есть решение с использованием hash-таблицы, которая будет заполняться по мере
//прохождения масссива, соотвественно ожидаемый ответ будет иной по сравнению с решением выше

function firstSum(numsArr, total) {
  const hash = {};

  for(let i = 0; i < numsArr.length; i++) {
    if(hash[total - numsArr[i]] !== undefined) {
      return [total - numsArr[i], numsArr[i]]
    }
    hash[numsArr[i]] = numsArr[i];
  }

  return [];
}

firstSum(arr, total) //[6, 7]

//Сложность данного алгоритма O(n), но есть у данного решения минус это создание hash-таблицы, которая будет занимать память
```

## HomeWork №5

1\.
```javascript
let promiseTwo = new Promise((resolve, reject) => {
  resolve("a"); // промис зарезолвится со значением 'a'
});

promiseTwo
  .then((res) => { // res = 'a'
    return res + "b"; // вернёт промис со значением 'ab'
  })
  .then((res) => {
    return res + "с"; // вернёт промис со значением 'abc'
  })
  .finally((res) => {
    return res + "!!!!!!!"; // finally ничего не принимает и не возвращает
  })
  .catch((res) => {
    return res + "d"; // catch будет пропущен, ошибок нет
  })
  .then((res) => {
    console.log(res); // выведет в консоль 'abc', вернёт промис со значением undefined
  });
```
2\.
```javascript
function doSmth() {
  return Promise.resolve("123");
}

doSmth()
  .then(function (a) {
    console.log("1", a); // выведет в консоль '1 123'
    return a; // вернёт промис со значением '123'
  })
  .then(function (b) {
    console.log("2", b); // выведет в консоль '2 123'
    return Promise.reject("321"); // отклонит промис со значением '321'
  })
  .catch(function (err) {
    console.log("3", err); // выведет в консоль '3 321', вернёт промис со значением undefined
  })
  .then(function (c) {
    console.log("4", c); // выведет в консоль '4 undefined'
    return c; // вернёт промис со значением 'undefined'
  });

// порядок вывода в консоль: 
// '1 123'
// '2 123'
// '3 321'
// '4 undefined'
```
3\.
```javascript
function printArrElemWithDelay(arr, delayMs = 3000) {
  for(let i = 0; i < arr.length, i++) {
    setTimeout(() => console.log(i), delayMs*(i+1))
  }
}
```

4\. Мы можем использовать await на верхнем уровне модуля. Наш модуль не завершит загрузку, пока не будет выполнен promise (это означает, что любой модуль, ожидающий загрузки нашего модуля, не завершит загрузку, пока не будет выполнен promise). Если promise отклонен, наш модуль тоже не загрузится. 
  Как правило, top-level await используется в ситуациях, когда мы 
хотим, чтобы модуль не  выполнялся до тех пор, пока promise не будет выполнен. Если мы хотим чтобы модуль выполнился даже если promise отклонен, можно обернуть top-level await в кострукцию try/catch

5\.
```javascript
//Решим задачу с помощью цикла for и await
async function fetchUrl(url) {
  for(let attemptsCount = 1; attemptsCount <= 5; attemptsCount++) {
    try {
      const res = await fetch(url);
      if (res.ok) { 
        return res;
      } else {
        Promise.reject(res.status)
      }  
    } catch(e) {
      if(attemptsCount <= 4) {
        continue
      }
      return Promise.reject(e)
    }
  }
}

//Решим задачу с помощью рекурсии и promise.chaining
function fetchUrl(url, attemptsCount = 5) {
  return fetch(url).then((res) => {
    if(res.ok) {
      return res
    } else {
      return Promise.reject(res.status)
    }
  }).catch((er) => {
    if(attemptsCount === 1) {
      return Promise.reject(er);
    }
    return fetchUrl(url, --attemptsCount)  
  })
}

//Для проверки
fetchUrl('https://google/com&#39').then(res => {
 console.log(res);
}).catch((er) => {
 console.log(`Error: ${er}`)
})
```
