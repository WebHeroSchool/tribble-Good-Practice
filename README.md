# JS Style Guide

**Всем привет! В этом небольшой гайде я хочу рассказать о тех практиках при написании кода в Java Script, которые я считаю наиболее удачными.** 

Поехали :) 

### 1. Не надо использовать короткую запись
Несмотря на то, что большинство браузеров смогут воспринять следующую запись:  
```
if(someVariableExists)  
  x = false
```
Пожалуйста, не делайте так. Отсутствие фигурных скобок создает огромную путаницу и делает код нечитабельным. Поэтому остановимся на такой записи:  
```
if(someVariableExists) {  
  x = false;  
}  
```
  
### 2. Скрипты - вниз!
Когда браузер грузит скрипт, он не продолжит рендеринг пока весь файл не будет загружен. Таким образом пользователю придется ждать дольше.
Для ускорения загрузки страницы, вам стоит перенести скрипты вниз поставив их перед закрывающимся тегом body.
Пример:
```
<p>Карл у Клары украл кораллы.</p>  
<script type="text/javascript" src="path/to/file.js"></script>  
<script type="text/javascript" src="path/to/anotherFile.js"></script>  
</body>  
</html>
```

### 3. Поменьше глобальных переменных
Это нужно для того, чтобы уменьшить риск нежелательного взаимодействия с "с другими приложениями, виджетами или библиотеками". (с) Douglas Crockford
Поэтому вместо этого: 
```
const name = 'Шерлок';  
const lastName = 'Холмс';  
  
function doSomething() {...}  

console.log(name); // Шерлок -- or window.name
``` 
Лучше сократим число глобальных переменных, записав следующим образом:
```
const DudeNameSpace = {  
  name : 'Шерлок',  
  lastName : 'Холмс',  
  doSomething : function() {...}  
  }  
console.log(DudeNameSpace.name); // Шерлок
```

### 4. === вместо ==
В случае, если вам нужно провести сравнение двух операндов, лучше использовать === и !==, а не == и !=. Операторы строгого сравнения не позволят появиться ошибке: если операнды   разных типов, то всегда будет возвращаться false.
Пример: 
```
console.log("3" === 3);           // false
console.log(true === 1);          // false
console.log(null === undefined);  // false
```
*При этом обратим внимание, что:*  
```
null == undefined;    // true
```

### 5. Не бойтесь комментировать части кода
Это может быть полезно как для ваших коллег, которые будут делать ревью кода или работать с ним, так и вам самим - потому что через пару месяцев вы вполне можете забыть, за что отвечала та или иная часть кода. Поэтому комментируйте важное.
Пример: 
```
// Перебирает массив и выводит каждый элемент.    
for(let i = 0, len = array.length; i < len; i++) {  
  console.log(array[i]);  
}  
```

### 6. {} вместо New Object()
Один из традиционных путей создания объекта выглядит так:
```
let o = new Object();  
o.name = 'Шерлок';  
o.lastName = 'Холмс';  
o.someFunction = function() {  
  console.log(this.name);  
} 
``` 
Однако более надежным следует считать объявление с помощью литералов объекта:
```
let o = {  
  name: 'Шерлок',  
  lastName = 'Холмс',  
  someFunction : function() {  
    console.log(this.name);  
  }  
}
```
Таким же образом можно создать и пустой объект:
```
let o = {};  
```

### 7. [] вместо new Array()
Аналогично поступим и с массивами. Вместо:
```
let a = new Array();  
a[0] = 'Джон';  
a[1] = 'Ватсон';
``` 
Запишем так:
```
let a = ['Джон','Ватсон'];
```

### 8. Любите точку с запятой
Чтобы не провоцировать позникновение проблем, которые потом к тому же будет сложно отследить, используйте точку с запятой.
Вместо:
```
const someItem = 'какая-то строка'
function doSomething() {  
  return 'something'  
}  
```
Запишем так:
```
let someItem = 'some string';  
function doSomething() {  
  return 'something';  
}  
```

### 9. Много переменных - используем запятую
Код будет выглядеть чище и элегантнее, когда мы упустим лишние var или let и воспользуемся запятыми.
Пример:
```
let someItem = 'строчка раз',  
  anotherItem = 'строчка два',  
  oneMoreItem = 'строчка три';  
```

### 10. Не объявляйте ненужные переменные
Если вам не нужно впоследствии возвратиться к этим данным, ни к чему забивать память браузера ненужными переменными. Кроме того, это поможет сделать код более чистым. 
Например, если мы хотим добавить текст в следующую часть кода:
```
<div id="foo">
  <p>
	
  </p>
</div>
```
Мы можем действовать так:
```
const foo = document.querySelector('#foo');
const p = foo.querySelector('p');
p.textContent = 'foo';
```
Но лучше и проще будет записать это другим образом, избегая ненужных переменных:
```
document.querySelector('#foo p').textContent = 'foo';
```

Надеюсь эти практики будут полезны :) Спасибо!