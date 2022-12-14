# TypeScript

#### 1. 타입스크립트를 쓰는 이유
     function add(num1, num2) {
     return num1 + num2
     }
     
     add();   // NaN
     add(1);  // NaN
     add(3,4);  // 7
     add(4,5,6);  //9
     add('hello','world');  // "helloworld"
     
     처럼 add(3,4)를 제외하곤 나머지것들은 실수가 분명한 코드인 것에도 불구하고 실행되었다.
     
    JavaScript(동적언어) => 런타임에 타입 결정 / 오류 발견
    TypeScript(정적언어) => 컴파일 타임에 타입 결정 /오류 발견 ==> 초기에 오류를 잡아두면 안정적이고 빠름.\\
    
    
    TypeScript
    
    function add(num1 : number, num2:number) {
    console.log(num1 + num2);
    }
    
    
    #### 2.기본 타입 
         let car:string = 'bmw';
         
         car = 'benz' (error x)
         car = 3      (error o)
         
         example
         let age:number = 30
         let isAdult:boolean = true
         let a:number[] = [1,2,3] 아래랑 같음
         let a2:Array<number> = [1,2,3]
         
         let week:string[] = ['mom']
         
         //튜플
         let b : [string,number]; 첫번째는 string, 두번째는 number;
         
         b = ['z',1];
         
         b[0].toLowerCase(); (ok) typescript는 컴파일할때 오류가 나와서 런타임되기전에 오류가 뭔지 알수있다.
         
         
         //void
         function sayHello():void{
         console.log('hello') //return 되는 값이 없을때 void라고 적어줌
         
         //never : 에러를 반환하거나 영원히 끝나지 않는 함수에
         function showError():never{
         throw new Error();
         }
         
         function infLoop():never{
         while(true) {
         //do something..
         } 
         }
         
         //enum // 비슷한것끼리 묶어둔것.
         enum Os {
         Window,
         Ios,
         Android
         }
         
         let myOs:Os;
         myOs = Os.Window
         
         
         //null, undefinded
         
         let a:null = null;
         let b:undefinded = undefinded;
         
#### 3.인터페이스
      let user:object;
      
      user ={
      name : "xx",
      age : 30
      }
      
      console.log(user.name)
      
      type Score = 'A' | 'B' | 'C' | 'D'  
    
      interface User{
      name : string;
      age:number;
      gender? : string; // ?은 option
      readonly birthYear : number; //읽기전용 속성 바꾸기 x
      [grade : number] : string;   //여러개 쓸 수 있음 grade
      }
      
      객체를 만들때 interface로 미리 형식을 만들어줘야한다.
      
      let user : User = {
      name: "xx",
      age: 30,
      birthYear : 2000,
      1 : 'A',
      2 : 'B',
      3 : 'C',
      }
      
      
      //함수 
      interface Add{
      (num1 : number,num2 :number
      
      }
      
      
      const add : Add = function(x,y) {
      return x+y;
      }
      
      add(10,20)
      
      interface IsAdult{
        (age:number):boolean;
        }
        
      const a:IsAdult = (age) => {
      return age>19;
      }
      
      
      //class 
      
      interface Car {
        color : string;
        wheels:number;
        start(): void;
        }
        
       // class에는 implements를 사용한다.
     
       
      class Bmw implements Car{
        color = 'red'
        wheels = 4;
        start() {
        console.log('go..')
        }
        };
        
        ===
        
      class Bmw implements Car{
      color;
      wheels = 4;
      constructor(c:string){
      this.color = c;
      }
      start() {
        console.log('go..');
      }
      }
      
      const b = new Bmw('green')
      console.log(b);
      b.start();  ==> "go.."
      
#### 4.함수
     function hello(name?: string){
          return `Hello, ${name || 'world'};
     }
     
     function hello2(name = "world"){
     return `Hello, ${name}`;
     }
     
     const result = hello();
      //name이 option 이라 필요없을수도 있음.
     const result2 = hello('Sam')
     
    //////////////////이쪽 위에/////// 
     /////////////////이해 잘 안됨////////////////
     
     function add(...nums:numbers[]) {
          return nums.reduce((result,num) => result + num , 0);
          }
          
          //reduce first argument accumulate, second currentValue
      add(1,2,3);
      add(1,2,3,4,5,6,7,8);
      
      
      //객체
      interface User {
          name : string;
          }
          
       const Sam : User = {name: 'Sam'}
       
       function showName(age :number, gender: 'm' | 'f') {
          console.log(this.name, age, gender)


### 5 리터럴, 유니온/교차 타입

```jsx
//Literal Types

const userName1 = "Bob"  // userName1 은 string으로 받는다.
let userName2 ="Tom" //userName2도 string

userName2 = 3;   //이렇게 숫자로 받으면 오류가 나오는데
// let userName2 : string | number = "Tom" 으로 바꿔주면 오류x

type Job = "student" | "developer" | "engineer"
//Job은 옆 세개밖에 못쓴다!

interface User{
	name : string;
  job : Job;
}

//interface는 객체를 만들기전에 미리 적어줘야한다.

const user:User = {
	name : "Bob",
	job : "student"	
};

interface HighSchoolStudent {
	name : number | string //유니온타입
	grade : 1 | 2 | 3;
}

interface Car{
	name : "car"
	color : string;
	start(): void;
}

interface Mobile{
	name : "mobile";
	color : string;
	call() : void;
}

function getGift(gift : Car | Mobile){
	console.log(gift.color);

	if ( gift.name === "car")
		gift.start()
	else 
		gift.call()
}

//intersection Types

interface Car{
	name : string
	start() : void;
}

interface Toy{
	name : string;
	color : string;
	price : number;
}

const toyCar: Toy & Car = {
	name : "타요",
	start() {},
	color : "blue",
	price : 1000,
};  //이런식으로 intersection을 해주면 모든 것을 다 적어주어야 한다.
		// name, start, color, price

```

### 6 클래스

```jsx
class Car{
	color : string;
	//여기에 이렇게 꼭 적어줘야한다.

	constructor(color : string){ //매개변수 타입도 string으로 적어줘야함
		this.color = color;
}
start() {
console.log('start');
}
}
const bmw = new Car('red')

//접근 제한자 - public private protected

public - 자식 클래스, 클래스 인스턴스 모두 접근 가능
private - 
protected - 자식 클래스 접근 가능

//추상 클래스
	다시 듣기..

```
