## TypeScript

[toc]

### 基础类型

####  1. Number类型

> ```typescript
> let age: number = 18;
> ```

#### 2. String类型

> ```typescript
> let name: string = 'youngxin'
> ```

#### 3. Boolean类型

> ``` typescript
> let isMan: boolean = true;
> ```

#### 4. Array类型

> // 数字数组，`元素类型[]`
>
> ``` typescript
> let numberList: number[] = [1,2,3]; 
> ```
>
> // 数组泛型，`Array<元素类型>`
>
> ``` typescript
> let stringList: Array<string> = ['1','2','3'];
> ```

#### 5. Tuple类型

> 元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同。
>
> ``` typescript
> let mixArr:[string, number];
> mixArr = ['hello', 18];
> ```

#### 4. Enum类型

> 枚举类型是对JavaScript标准数据类型的一个补充。使用枚举类型可以为一组数值赋予友好的名字。
>
> * 基础用法
>
> ``` typescript
> enum Color {Red, Green, Blue}
> let c: Color = Color.Green;
> ```

#### 5. Any类型

> any类型标记的变量将跳过类型检查

#### 6. Void类型

> 通常用户函数返回值，表示没有任何类型，及当函数没有返回值的时候。
>
> ``` typescript
> function hellow(): void {
>     console.log('HELLO WORLD!');
> }
> ```

#### 7. Null 和 Undefined

> ``` typescript
> let u: undefined = undefined;
> let n: null = null;
> ```
>
> 默认情况下`null`和`undefined`是所有类型的子类型。
>
> 在项目中，推荐在配置文件中添加`strictNullChecks: true `，使使`null`和`undefined`只能赋值给`void`和它们各自，来避免很多常见问题。
>
> 如果需要使用`undefined`搭配其他的数据类型推荐使用联合类型：string | number | undefined；

#### 8. Nerver类型

> `never`类型表示的是那些永不存在的值的类型。
>
> 常见的有
>
> * 抛出异常
> * 死循环

#### 9. Object类型

#### 类型断言

​	在开发过程中，我们可能比TypeScript的类型推断更明确一个变量的值，可以通过类型断言的语法告诉编辑器，`相信我，我知道自己在干什么`。

* `<>`语法

  > ``` typescript
  > 
  > ```
  >
  
* `as`语法

### 接口

#### 接口的基础用法

```  {typescript
interface IPerson {
    name: string;
    age: number;
    gender: '男' | '女';
    hobby?: string;// 可选属性
   	readonly size: 18; // 只读属性
    [propName: string]: any; // 索引签名
    
}
let man: IPerson = {
    name: 'youngxin',
    age: 18,
    gender: '男'
}
```

#### 继承接口

接口是可以继承的，与ES6中类的继承类似，方便我们更加灵活地将接口分割到可重用的模块里。

``` typescript
interface IYoungxin extends IPerson {
   weight: number
}
```

一个接口可以继承多个接口，创建出一个多个接口的合成接口。

#### 混合类型

在JavaScript中有着丰富的类型。有时候你希望一个对象可以具备上面提到的多种类型

``` typescript
interface Counter {
    (start: number): string;
    interval: number;
    reset(): void;
}

function getCounter(): Counter {
    let counter = <Counter>function (start: number) { };
    counter.interval = 123;
    counter.reset = function () { };
    return counter;
}

let c = getCounter();
c(10);
c.reset();
c.interval = 5.0;
```



### 函数

常见的函数声明

``` typescript
function buildName(firstName: string, lastName: string = 'xin', ...restOfName: string[]): string {
    return firstName+ "" + lastName + "" + restOfName.join('');
}
```

这个声明中包含了`参数声明`，`参数默认值`，`剩余参数`，`函数返回` 的类型声明

### 泛型

泛型相当于一个类型变量，在定义时，无法预先知道具体的类型，可以用该变量来代替，只有到调用时，才能确定它的类型。来获取更加一致的类型推断。

#### 如何在类型别名、接口、类中使用泛型

``` typescript
// 类型别名
type TCallback<T> = (n: T, i:number) => boolean;
// 接口
interface ICallback<T> {
    (n:T, i: number): boolean;
}
// 我们希望函数中多个位置的类型保持一致或有关联的信息
function filter<T> (arr: T[], callback: TCallback<T>): T[] {
    const newArr:T[] = [];
    arr.forEach((n, i) => {
        if(callback(n, i)) {
            newArr.push(n);
        }
    })
    return newArr;
}
```

#### 泛型约束

用于限制泛型的取值。

``` typescript
interface IHasNamePoperty {
    name: string;
}

function nameToUpperCase<T extends IHasNamePoperty>(obj: T): T {
    obj.name = obj.name.split(' ').map(s=>s[0].toUpperCase() + s.substr(1)).join(' ');
    return obj
}
```



#### 多泛型

将两个相同长度的数组进行混合

``` typescript
// [1,2,3] + ['a','b','c'] => [1,'a',2,'b',3,'c']
function mixinArray<T, Kz> (arr1: T[], arr2: K[]): (T | K)[] {
    if(arr1.length !== arr2.length) {
        throw new Error('两个数组长度不一致')
    }
    let result:(T | K)[] = [];
    for(let i = 0; i < arr1.length, i++){
        result.push(arr1[i]);
        result.push(arr2[i])
    }
    return result;
}
```



































