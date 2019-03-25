# My best practicesy

On this article I would like to give good and
modern solution of some problem

Lets go.

### Debuging

For example we have 3 objects

```
const foo = {
    name: 'this is object foo',
};

const bar = {
    name: 'this is object bar',
};

const baz = {
    name: 'this is object baz',
};
```

How can you getting debugging


Bad code 💩

```
console.log(foo);
console.log(bar);
console.log(baz);
```

![alt text](http://joxi.net/D2Pvp0QUqj3gXr.jpg)


Good code 😎

```
console.log({foo, bar, baz});
```

![alt text](http://dl4.joxi.net/drive/2019/02/23/0035/3004/2296764/64/de0423927e.jpg)


+ Bonus 

Good code 😎

```
function Person(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
}

var family = {};

family.mother = new Person("Jane", "Smith");
family.father = new Person("John", "Smith");
family.daughter = new Person("Emily", "Smith");

console.table(family);

```

![alt text](http://joxi.net/Rmz3lVkHYXo4L2.jpg)

Very well read. isn't it?

We can also give your custom style in the console, such as the message 
in console when wi open it in facebook page.

![alt text](http://joxi.ru/Q2KvMB7ULbDPNm.jpg)

That's how it's done 

```
var cssRule =
    "color: rgb(189, 7, 7);" +
    "font-size: 60px;" +
    "font-weight: bold;" +
    "text-shadow: 1px 1px 5px rgb(103, 0, 0);" +
    "filter: dropshadow(color=rgb(249, 162, 34), offx=1, offy=1);";

console.log("%cStop!", cssRule);
```

+ Bonus

```
function foo() {
  function bar() {
    console.trace('i am here');
  }
  bar();
}

foo();

```

Here we can see all calls before `console.trace`

![alt text](http://joxi.ru/DmBvk0DUJdeL7m.jpg)


### Spred

For example we have this objects

```
const student = { name: 'Poxos', age: 19}
const info = { iq: 120, country: 'Yerevan' }
```

How we can connect student and her info

Bad code 💩

```
student['country'] = info.country;
student['iq'] = info.iq;
```

Or

```
const newStudent = Object.assign(student, info);
```

Good code 😎

```
const newStudent = {...student, ...info}

```

Push / Unshift

```
const arr = [ 2, 3, 4 ];
```

Bad code 💩

```
arr.push(5);
arr.push(6);
arr.push(7);
```


Good code 😎

```
arr = [ ...arr, 4, 5, 6 ]; 

///unshift

arr = [ 0, 1, ...arr ]; 
```

Delete element.

```
const arr = { title: 'title', info: 'info' };

```

Bad code 💩

```
delete arr.info;
```

Good code 😎

```

const {
    info,
    ...newObject
} = arr;
arr = newObject,
```

### Loops


```
const orders = [ 123, 22, 8, 400, 32 ]

```

Bad code 💩

```
const total = 0;
const withTax = [];
const highValue = [];

for (i = 0; i < orders.length; ++i) {
    //reduce
    total += orders[i];

    //map
    withTax.push(orders[i] * 1.1);

    //filter
    if(orders[i] > 100) {
        highValue.push(orders[i]);
    }

}
```

Good code 😎

```
const total = orders.reduce((acc, cur) => acc + cur);

const withTax = orders.map(v => v * 1.1);

const highValue = orders.filter(v => v > 100);

```

### Async await 

```
const random = () => {
    return Promise.resolve(Math.random())
}
```

Bad code 💩

```
    const sumRandomAsyncNums = () => {
        let first;
        let second;
        let third;

        return random()
            .then(v => {
                first = v;
                return random();
            })
            .then(v => {
                second = v;
                return random();
            })
            .then(v => {
                third = v;
                return ` ${first} ${second} ${third}`;
            })
            .then(v => {
                console.log(`Result ${v}`);
            })
    }
```

![alt text](http://joxi.ru/p27Vd37iKnZjZm.jpg)


Good code 😎

```
    const sumRandomAsyncNums = async() => {
        const first = await random();
        const second = await random();
        const third = await random();

        console.log(`Result ${first} ${second} ${third}`);
    }
```


Good code 😎 ++

```
    const sumRandomAsyncNums = async() => {
        const randos = Promise.all([random(), random(), random()]);
        let result = 0;
        for(const r of await randos) {
            result += r;
        }
        console.log(`Result ${result}`);
    }
```

### Callbacks

For example we have one store in your parent component.
And they are `good` and `bad` properties, and we have 2 child component.

```
class Parent extends React.Component {

    this.state = {
        bad: [],
        good: [],
    }

    <Child
    />

    <Child
    />

}
```

```
function Child(props) {

    addItem() {
        return Math.random();
    }

}
```

How you can create your collback function for add `bad` or `good` propartyes.



Bad code 💩

```
class Parent extends React.Component {

    this.state = {
        bad: [],
        good: [],
    }

    const addItemByType = (type, item) {
        this.setState({[type]: [...this.state[type], item]});
    }

    <Child
        type='bad'
        addItemByType={this.addItemByType}
    />

    <Child
        type='good'
        addItemByType={this.addItemByType}
    />

}
```

```
function Child(props) {

    addItem() {
        return props.addItemByType(props.type, Math.random())
    }

}
```

Good code 😎

```
class Parent extends React.Component {

    this.state = {
        bad: [],
        good: [],
    }

    const addItemByType = type => item => {
        this.setState({[type]: [...this.state[type], item]});
    }

    <Child
        addItemByType={this.addItemByType('bad')}
    />

    <Child
        addItemByType={this.addItemByType('good')}
    />

}
```

```
function Child(props) {

    addItem() {
        return props.addItemByType(Math.random())
    }

}
```
