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


// Конструктор объекта
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
  if(typeof obj1 !== 'object' || typeof obj2 !== 'object') return false
  if(Object.keys(obj1).length !== Object.keys(obj2).length) return false
  if(obj1 === obj2) return 'Ссылаются на один и тот же объект'

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
const reverseString1 = str => {
  let resStr = '';
  str.split('').forEach(char => resStr = char + res);
  return res;
}

const reverseString2 = str => str.split('').reverse().join('');

const reverseString3 = str => str.split('').reduce((resStr, char) => char + resStr, '')

  ```