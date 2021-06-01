# front-es6
前端es6知识

- 1、let
```
let 声明的变量有严格局部作用域,只能声明一次
var 声明的变量往往会越域,可以声明多次
const 常量,一但声明必须初始化,声明之后不允许改变
```
- 2、解构表达式
```
//1）数组解构
let arr = [1,2,3];
let [a,b,c] = arr;
console.log(a,b,c)

//2）对象解构
const person = {
   name: "jack",
   age: 21,
   language: ['java', 'js', 'css']
}

//3）name赋值给了abc
const { name: abc, age, language } = person;
console.log(abc, age, language)

//4）字符串扩展
let str = "hello.vue";
console.log(str.startsWith("hello"));//true
console.log(str.endsWith(".vue"));//true
console.log(str.includes("e"));//true

//5）字符串模板,``不是单引号，是~这个
let ss = `<div>
                    <span>hello world<span>
                </div>`;
console.log(ss);

//6）字符串插入变量和表达式。变量名写在 ${} 中，${} 中可以放入 JavaScript 表达式
let info = `我是${abc}，今年${age + 10}了, 我想说： ${fun()}`;
```
- 3、函数优化
```
//1）现在可以这么写：直接给参数写上默认值，没传就会自动使用默认值
        function add2(a, b = 1) {
            return a + b;
        }
        console.log(add2(20));
//2）、不定参数
        function fun(...values) {
            console.log(values.length)
        }
        fun(1, 2)      //2
        fun(1, 2, 3, 4)  //4
/3）、箭头函数
        //以前声明一个方法
        // var print = function (obj) {
        //     console.log(obj);
        // }
       var sum2 = (a, b) => a + b;
        console.log(sum2(11, 12));
```
- 4、对象优化
```
        const person = {
            name: "jack",
            age: 21,
            language: ['java', 'js', 'css']
        }


        console.log(Object.keys(person));//["name", "age", "language"]
        console.log(Object.values(person));//["jack", 21, Array(3)]
        console.log(Object.entries(person));//[Array(2), Array(2), Array(2)]

//1）合并对象
        const target = { a: 1 };
        const source1 = { b: 2 };
        const source2 = { c: 3 };


        //{a:1,b:2,c:3}
        Object.assign(target, source1, source2);

//2）、声明对象简写
        const age = 23
        const name = "张三"
        const person1 = { age: age, name: name }


        const person2 = { age, name }
        console.log(person2);

//3）、对象的函数属性简写
        let person3 = {
            name: "jack",
            // 以前：
            eat: function (food) {
                console.log(this.name + "在吃" + food);
            },
            //箭头函数this不能使用，对象.属性
            eat2: food => console.log(person3.name + "在吃" + food),
            eat3(food) {
                console.log(this.name + "在吃" + food);
            }
        }

//4）、对象拓展运算符


        // 1、拷贝对象（深拷贝）
        let p1 = { name: "Amy", age: 15 }
        let someone = { ...p1 }
        console.log(someone)  //{name: "Amy", age: 15}


        // 2、合并对象
        let age1 = { age: 15 }
        let name1 = { name: "Amy" }
        let p2 = {name:"zhangsan"}
        p2 = { ...age1, ...name1 }
        console.log(p2)
```
- 5、map和reduce
```
//数组中新增了map和reduce方法。
        //map()：接收一个函数，将原数组中的所有元素用这个函数处理后放入新数组返回。
         let arr = ['1', '20', '-5', '3'];
         
        //  arr = arr.map((item)=>{
        //     return item*2
        //  });
         arr = arr.map(item=> item*2);
         console.log(arr);
        //reduce() 为数组中的每一个元素依次执行回调函数，不包括数组中被删除或从未被赋值的元素，
        //[2, 40, -10, 6]
        //arr.reduce(callback,[initialValue])
        /**
         1、previousValue （上一次调用回调返回的值，或者是提供的初始值（initialValue））
    2、currentValue （数组中当前被处理的元素）
    3、index （当前元素在数组中的索引）
    4、array （调用 reduce 的数组）*/
        let result = arr.reduce((a,b)=>{
            console.log("上一次处理后："+a);
            console.log("当前正在处理："+b);
            return a + b;
        },100);
        console.log(result)
```
- 6、promise
```
   function get(url, data) {
            return new Promise((resolve, reject) => {
                $.ajax({
                    url: url,
                    data: data,
                    success: function (data) {
                        resolve(data);
                    },
                    error: function (err) {
                        reject(err)
                    }
                })
            });
        }

        get("mock/user.json")
            .then((data) => {
                console.log("用户查询成功~~~:", data)
                return get(`mock/user_corse_${data.id}.json`);
            })
            .then((data) => {
                console.log("课程查询成功~~~:", data)
                return get(`mock/corse_score_${data.id}.json`);
            })
            .then((data)=>{
                console.log("课程成绩查询成功~~~:", data)
            })
            .catch((err)=>{
                console.log("出现异常",err)
            });
```
- 7、模块化
```
user.js
var name = "jack"
var age = 21
function add(a,b){
    return a + b;
}
export {name,age,add}


main.js
import {name,add} from "./user.js"
abc.sum(1,2);
console.log(name);
add(1,3);
```
