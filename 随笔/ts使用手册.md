## typeScript 简介
+ TypeScript 并不是一个完全新的语言, 它是 JavaScript 的超集，为 JavaScript 的生态增加了类型机制，并最终将代码编译为纯粹的 JavaScript 代码。

### TypeScript 简介
+ TypeScript 由 Microsoft(算上 Angular 2 的话加上 Google)开发和维护的一种开源编程语言。 它支持 JavaScript 的所有语法和语义，同时通过作为 ECMAScript 的超集来提供一些额外的功能，如类型检测和更丰富的语法。下图显示了 TypeScript 与 ES5，ES2015，ES2016 之间的关系。
+ ![](./image/ts与ecma的关系.png)

### 使用 TypeScript 的原因
+ 1、TypeScript 可以使用 JavaScript 中的所有代码和编码概念，TypeScript 是为了使 JavaScript 的开发变得更加容易而创建的。例如，TypeScript 使用类型和接口等概念来描述正在使用的数据，这使开发人员能够快速检测错误并调试应用程序
+ 2、TypeScript 从核心语言方面和类概念的模塑方面对 JavaScript 对象模型进行扩展。
+ 3、JavaScript 代码可以在无需任何修改的情况下与 TypeScript 一同工作，同时可以使用编译器将 TypeScript 代码转换为 JavaScript。
+ 4、TypeScript 通过类型注解提供编译时的静态类型检查。
+ 5、TypeScript 中的数据要求带有明确的类型，JavaScript不要求。
+ 6、TypeScript 引入了 JavaScript 中没有的“类”概念。
+ 7、TypeScript 中引入了模块的概念，可以把声明、数据、函数和类封装在模块中。
+ 8、类型注释是 TypeScript 的内置功能之一，允许文本编辑器和 IDE 可以对我们的代码执行更好的静态分析。 这意味着我们可以通过自动编译工具的帮助，在编写代码时减少错误，从而提高我们的生产力

### 数据类型
#### String 类型
+ 一个保存字符串的文本，类型声明为 string。可以发现类型声明可大写也可小写，后文同理。
```js
let name: string = 'aaaaaa'
let name2: String = 'aaaaaa'
```
#### Boolen 类型
+ boolean是 true 或 false 的值，所以 `let isBool: boolean = new Boolean(1)` 就会编译报错，因为 new Boolean(1) 生成的是一个 Bool 对象。
```js
let isBool1: boolean = false
```
#### Number 类型
```js
let number: number = 10
```
#### Array 类型
+ 数组是 Array 类型。然而，因为数组是一个集合，我们还需要指定在数组中的元素的类型。我们通过 Array\<type\> or type[] 语法为数组内的元素指定类型
```js
let arr:number[] = [1, 2, 3, 4, 5];
let arr2:Array<number> = [1, 2, 3, 4, 5];

let arr3:string[] = ["1","2"];
let arr4:Array<string> = ["1","2"];
```
#### Enums 类型
+ 列出所有可用值，一个枚举的默认初始值是0。你可以调整一开始的范围：
```js
enum Role {Employee = 3, Manager, Admin}
let role: Role = Role.Employee
console.log(role) // 3
```
#### Any 类型
+ any 是默认的类型，其类型的变量允许任何类型的值：
```js
let notSure:any = 10;
let notSure2:any[] = [1,"2",false];
```
#### Void 类型
+ JavaScript 没有空值 Void 的概念，在 TypeScirpt 中，可以用 void 表示没有任何返回值的函数：
```js
function alertName(): void {
  console.log('My name is muyy')
}
```
### 函数
#### 为函数定义类型
+ 我么可以给每个参数添加类型之后再为函数本身添加返回值类型。 TypeScript能够根据返回语句自动推断出返回值类型，因此我们通常省略它。下面函数 add, add2, add3 的效果是一样的，其中是 add3 函数是函数完整类型。
```js
function add(x: string, y: string): string{
    return "Hello TypeScript";
}

let add2 = function(x: string, y: string): string{
    return "Hello TypeScript";
}

let add3: (x: string, y: string) => string = function(x: string, y: string): string{
    return "Hello TypeScript";
}
```
#### 可选参数和默认参数
+ JavaScript 里，每个参数都是可选的，可传可不传。 没传参的时候，它的值就是 undefined 。 在 TypeScript 里我们可以在参数名旁使用 `?` 实现可选参数的功能。 比如，我们想让 lastname 是可选的：
```js
function buildName(firstName: string, lastname?: string){
    console.log(lastname ? firstName + "" + lastname : firstName)
}

let res1 = buildName("鸣","人"); // 鸣人
let res2 = buildName("鸣"); // 鸣
let res3 = buildName("鸣", "人", "君"); // Supplied parameters do not match any signature of call target.
```
+ 如果带默认值的参数出现在必须参数前面，用户必须明确的传入 undefined 值来获得默认值。 例如，我们重写上例子，让 firstName 是带默认值的参数：
```js
function buildName2(firstName = "鸣", lastName?: string){
    console.log(firstName + "" + lastName)
}

let res4 = buildName2("人"); // 人undefined
let res5 = buildName2(undefined, "人"); // 鸣人
```
### 类
+ 传统的 JavaScript 程序使用函数和基于原型的继承来创建可重用的组件，但对于熟悉使用面向对象方式的程序员来讲就有些棘手，因为他们用的是基于类的继承并且对象是由类构建出来的。从 ECMAScript 2015，也就是 ECMAScript 6 开始，JavaScript 程序员将能够使用基于类的面向对象的方式。 使用 TypeScript，我们允许开发者现在就使用这些特性，并且编译后的 JavaScript 可以在所有主流浏览器和平台上运行，而不需要等到下个 JavaScript 版本。
#### 类
```js
class Person{
    name:string; // 这个是对后文this.name类型的定义
    age:number;
    constructor(name:string,age:number){
        this.name = name;
        this.age = age;
    }
    print(){
        return this.name + this.age;
    }
}

let person:Person = new Person('liu',23)
console.log(person.print()) // liu23
```
+ 我们在引用任何一个类成员的时候都用了 this。 它表示我们访问的是类的成员。其实这本质上还是 ES6 的知识，只是在 ES6 的基础上多上了对 this 字段和引用参数的类型声明。
#### 继承
```js
class Person{
    public name:string;  // public、private、static 是 typescript 中的类访问修饰符
    age:number;
    constructor(name:string,age:number){
        this.name = name;
        this.age = age;
    }
    tell(){
        console.log(this.name + this.age);
    }
}

class Student extends Person{
    gender:string;
    constructor(gender:string){
        super("liu",23);
        this.gender = gender;
    }
    tell(){
        console.log(this.name + this.age + this.gender);
    }
}

var student = new Student("male");
student.tell();  // liu23male
```
+ 这个例子展示了 TypeScript 中继承的一些特征，可以看到其实也是 ES6 的知识上加上类型声明。不过这里多了一个知识点 —— 公共，私有，以及受保护的修饰符。TypeScript 里，成员默认为 public ；当成员被标记成 private 时，它就不能在声明它的类的外部访问；protected 修饰符与private 修饰符的行为很相似，但有一点不同，protected 成员在派生类中仍然可以访问。
#### 存储器
+ TypeScript 支持通过 getters/setters 来截取对对象成员的访问。 它能帮助你有效的控制对对象成员的访问。
+ 对于存取器有下面几点需要注意的：
  + 首先，存取器要求你将编译器设置为输出 ECMAScript 5 或更高。 不支持降级到 ECMAScript 3。 其次，只带有 get 不带有 set 的存取器自动被推断为 readonly。 这在从代码生成 .d.ts 文件时是有帮助的，因为利用这个属性的用户会看到不允许改变它的值。
```js
class Hello{
    private _name: string;
    private _age: number;
    get name(): string {
        return this._name;
    }
    set name(value: string) {
        this._name = value;
    }
    get age(): number{
        return this._age;
    }
    set age(age: number) {
        if(age<0 && age>100){
            console.log("年龄在0-100之间"); // 年龄在0-100之间
            return;
        }
        this._age = age;
    }
}

let hello = new Hello();
hello.name = "liu";
hello.age = 23
console.log(hello.name); // liu
```
### 接口
#### 接口
+ TypeScript 的核心原则之一是对值所具有的结构进行类型检查。在 TypeScript 里，接口的作用就是为这些类型命名和为你的代码或第三方代码定义契约。
```js
interface LabelValue{
    label: string;
}

function printLabel(labelObj: LabelValue){
    console.log(labelObj.label);
}

let myObj = {
    "label":"hello Interface"
};
printLabel(myObj);
```
+ LabelledValue 接口就好比一个名字，它代表了有一个 label 属性且类型为 string 的对象。只要传入的对象满足上述必要条件，那么它就是被允许的。
+ 另外，类型检查器不会去检查属性的顺序，只要相应的属性存在并且类型也是对的就可以。
#### 可选属性
+ 带有可选属性的接口与普通的接口定义差不多，只是在可选属性名字定义的后面加一个 `?` 符号。可选属性的好处之一是可以对可能存在的属性进行预定义，好处之二是可以捕获引用了不存在的属性时的错误。
```js
interface Person{
    name?:string;
    age?:number;
}

function printInfo(info:Person){
    console.log(info);
}

let info = {
    "name":"muyy",
    "age":23
};

printInfo(info); // {"name": "muyy", "age": 23}

let info2 = {
    "name":"muyy"
};

printInfo(info2); // {"name": "muyy"}
```
#### 函数类型
+ 接口能够描述 JavaScript 中对象拥有的各种各样的外形。 除了描述带有属性的普通对象外，接口也可以描述函数类型。定义的函数类型接口就像是一个只有参数列表和返回值类型的函数定义。参数列表里的每个参数都需要名字和类型。定义后完成后，我们可以像使用其它接口一样使用这个函数类型的接口。
```js
interface SearchFunc{
    (source: string, subString: string): boolean;
}

let mySearch: SearchFunc;
mySearch = function(source: string,subString: string){
    return source.search(subString) !== -1;
};

console.log(mySearch("鸣人","鸣")); // true
console.log(mySearch("鸣人","缨")); // false
```
#### 可索引类型
+ 与使用接口描述函数类型差不多，我们也可以描述那些能够“通过索引得到”的类型，比如 a[10] 或 ageMap["daniel"]。 可索引类型具有一个索引签名，它描述了对象索引的类型，还有相应的索引返回值类型。 让我们看如下例子：
```js
interface StringArray{
    [index: number]: string;
}

let MyArray: StringArray;
MyArray = ["是","云","随","风"];
console.log(MyArray[2]); // 随
```
#### 类类型
+ 与 C# 或 Java 里接口的基本作用一样，TypeScript 也能够用它来明确的强制一个类去符合某种契约。
+ 我们可以在接口中描述一个方法，在类里实现它，如同下面的 setTime 方法一样：
```js
interface ClockInterface{
    currentTime: Date;
    setTime(d: Date);
}

class Clock implements ClockInterface{
    currentTime: Date;
    setTime(d: Date){
        this.currentTime = d;
    }
    constructor(h: number, m: number) {}
}
```
#### 继承接口
+ 和类一样，接口也可以相互继承。 这让我们能够从一个接口里复制成员到另一个接口里，可以更灵活地将接口分割到可重用的模块里。
```js
interface Shape{
    color: string;
}

interface PenStroke{
    penWidth: number;
}

interface Square extends Shape,PenStroke{
    sideLength: number;
}

let s = <Square>{};
s.color = "blue";
s.penWidth = 100;
s.sideLength = 10;
```
### 模块
+ TypeScript 与 ECMAScript 2015 一样，任何包含顶级 import 或者 export 的文件都被当成一个模块。
```js
export interface StringValidator{
    isAcceptable(s:string): boolean;
}

var strReg = /^[A-Za-z]+$/;
var numReg = /^[0-9]+$/;

export class letterValidator implements StringValidator{
    isAcceptable(s:string): boolean{
        return strReg.test(s);
    }
}

export class zipCode implements StringValidator{
    isAcceptable(s: string): boolean{
        return s.length == 5 && numReg.test(s);
    }
}
```
### 泛型
+ 软件工程中，我们不仅要创建一致的定义良好的 API ，同时也要考虑可重用性。 组件不仅能够支持当前的数据类型，同时也能支持未来的数据类型，这在创建大型系统时为你提供了十分灵活的功能。在像 C# 和 Java 这样的语言中，可以使用泛型来创建可重用的组件，一个组件可以支持多种类型的数据。 这样用户就可以以自己的数据类型来使用组件。
#### 初探泛型
+ 如下代码，我们给 Hello 函数添加了类型变量 T ，T 帮助我们捕获用户传入的类型（比如：string）。我们把这个版本的 Hello 函数叫做泛型，因为它可以适用于多个类型。 代码中 output 和 output2 是效果是相同的，第二种方法更加普遍，利用了类型推论 —— 即编译器会根据传入的参数自动地帮助我们确定T的类型：
```js
function Hello<T>(arg:T):T{
    return arg;
}

let outPut = Hello<string>('Hello Generic');
let output2 = Hello('Hello Generic')

console.log(outPut);
console.log(outPut2);
```
#### tsconfig.json
```js
  "noImplicitAny": false, // 不需要显示的指定 any
  "strictNullChecks": false, // 不需要强制对 null 类型检测
  "rootDir": "./src", // 输入文件路劲
  "outDir": "./build", // 输入文件路劲
  "incremental": true, // 增量编译
  "target": "es5", // 编译为指定版本
  "allowJs": true, // 编译 js 文件
  "checkJs": true, // 对 js 进行语法检测
  "noUnusedLocals": true, // 没有用到的变量有警告提示
  "noUnusedParameters": true, // 没有用到的函数参数会警告提示
```



