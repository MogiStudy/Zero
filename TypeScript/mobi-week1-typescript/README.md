## **TASK.1** **타입스크립트란 무엇일까요?**

(1) JavaScript and More

(2) A Result yo Can Trust

(3) Safety at Scale

**Q. 타입스크립트란? (300자 이내)**

>자바스크립트의 슈퍼 셋 (자바스크립트를 포함하는 확장된 버전). 자바스크립트의 확장된 버전으로서 기존에 있던 자바스크립트에 타입을 명시함으로서 컴파일 이전에 오류를 파악하고 개발자에게 오류를 알려줍니다. 또한 타입을 지정해줌으로서 타입 추론과 같이 자동 완성과 같은 생산성이 증가하고 다른 개발자들과 개발을 함에 있어서 가독성이 좋아집니다.

---

---

## **TASK.2** 실무에서 자주 사용하는 타입 바로 알기

### 타입스크립의 기본 타입

### number

number 타입은 정수나 소수를 나타내기 위해서 사용합니다.

```tsx
const user_age: number = 20;
console.log(user_age); // 20

```

### string

string 타입은 문자열을 나타내기 위해서 사용합니다. 문자열 안에는 숫자가 들어갈 수도 있습니다.

```tsx
const user_name: string = "zero";
console.log(user_name); // zero

```

### boolean

boolean 타입은 참 또는 거짓을 나타내기 위해서 사용이 됩니다.

```tsx
const isMale: boolean = true;
console.log(isMale) // true

```

### any

any 타입은 타입스크립트가 오류를 검사하지 않습니다. 따라서 무슨 타입이 들어갈 수 있습니다.

```tsx
let isAnyThing: any = "zero";
isAnyThing = false;
isAnyThing = "one";
isAnyThing = undefined;
isAnyThing = null;
isAnyThing = "zero";
console.log(isAnyThing); // zero

let isNumber: number = isAnyThing; // 다른 타입에도 할당이 가능합니다.
// 타입 검사를 진행하지 않습니다.
```

### object

object 타입은 안에 여러가지 키를 가지고 있는 값을 넣을 수 있습니다.

```tsx
const isObject: object = {
    user_name: "zero",
    user_age: 20,
    user_gender: 'male'
}
console.log(isObject) // { user_name: 'zero', user_age: 20, user_gender: 'male' }

```

### array

array 타입은 기존 타입처럼 따로 지정을 할 수가 없습니다.

```tsx
const isArray: string[] = [];
isArray.push("z")
isArray.push("e")
isArray.push("r")
isArray.push("o")
console.log(isArray) // [ z, e, r, o]
isArray.push(3) // TS2345: Argument of type 'number' is not assignable to parameter of type 'string'

```

### unknown

unknown 타입은 any타입과 유사하지만 typeGuard를 할 수 있습니다.

```tsx
let isUnknown : unknown = 2;
isUnknown = {};

let isString: string = isUnknown; // TS2322: Type 'unknown' is not assignable to type 'object'.
let isNumber: number = isAnyThing;
// isAnyThing 같은 경우 위에서 any type으로 지정을 하였기 때문에 마지막이 문자열임에도 할당이 됩니다.
// 하지만 isString의 경우 isUnkown의 값을 모르므로 isString에 할당이 되지 않습니다.

```

### union

유니온 타입은 해당 값이 아닐 경우 지정하지 못하게 고정 시켜줄 수 있습니다. 또한 자동완성도 가능하게 만들어줘서 생산성이 좋습니다.

```tsx
let union : "top" | "left" | "right" | "bottom";
union = "right";
union = "left";
union = "top";
union = "right";
union = "center"; // TS2322: Type '"center"' is not assignable to type '"top" | "left" | "right" | "bottom"'.

```

### conditional

conditional 타입은 조건부 타입으로서 조건에 따라 타입이 지정이 됩니다.

```tsx
type Man = true
type Girl = false

type Gender<T> = T extends boolean & true ? Man : Girl

type ZeroGender = Gender<true>

const zeroGender: ZeroGender = true;

```

### type alias

type alias는 타입에 이름을 정해줄 수 있습니다. 가독성이 증가하고 문서화 작업에 수월합니다.

```tsx
type UserName : String
type UserAge : number
type userGender : boolean
type userAddress : string

type UserInfoType = {
    userName: UserName,
    userAge: UserAge,
    userGender: userGender,
    userAddress: userAddress,
}
```

### interface

Interface는 선언전 병합이 가능합니다. 동일한 이름의 인터페이스가 선언될 경우 병합이 됩니다. 확장성이 좋습니다.
또 클래스를 사용할 경우 상속이 가능합니다.

```tsx
interface IUserInfo {
    user_name: string
}

interface IUserInfo {
    user_age: number
}

interface IUserInfo {
    user_gender: boolean
}

const userInfo: IUserInfo = {
    user_name: "zero",
    user_age: 20,
    user_gender: true
}

```

### type

type도 병합이 가능합니다. 둘 다 병합에 사용할 수 있습니다.

```tsx
type UserInfoName = {
    user_name: string
}

type UserInfoAge = {
    user_age: number
}

const userInfo: UserInfoName & UserInfoAge = {
    user_name: "zero",
    user_age: 20,
}

```

확장성을 고려해..? API 같은 경우에는 Interface를 나머지는 type을 쓰는 경우도 있다고 합니다. 협업을 할 때 정해서 사용하면 될 것 같습니다.

## 타입스크립트의 유틸리티 타입

### enum

enum은 상수 값을 만들어줍니다. map과 같이 key와 value로 이루어집니다. key는 중복이 될 수 없습니다.
만약 value를 지정하지 않을 시 자동으로 위에서 부터 숫자로 지정이 되게 됩니다.
만약 맨 위에 값을 4로 지정해 둘시에는 그 뒤에 값부터는 5가 지정이 됩니다. 없을 경우 undefind가 반환 됩니다

대표적인 예시로는 boolean과 같은 타입이 있습니다.

만약 Enum을 사용하게 된다면 true, false만 하더라도 0과 1도 같이 상수 값으로 만들어지기 때문에 메모리 낭비가 있을 수 있습니다.

```tsx
enum booleanValue {
    false,
    true,
}

console.log(booleanValue[0]) // false
console.log(booleanValue['true']) // 1

```

### as const

as const는 해당 값을 상수로 바꿔줍니다. 객체와 같은 경우도 수정이 불가능해집니다.

```tsx
const userInfo = {
    name : "zero",
    age : 20,
    isMale : true
}

userInfo.name = "sugar"
// 일반적으로 선언한 객체의 경우 수정이 가능합니다.

```

```tsx
const userInfo = {
    name : "zero",
    age : 20,
    isMale : true
} as const;

userInfo.name = "sugar" // TS2540: Cannot assign to 'name' because it is a read-only property.
// as const의 경우 객체 자체가 상수가 되었기 때문에 수정이 불가능 합니다.

```

```tsx
const userInfo = {
    name : "zero",
    age : 20,
    isMale : true
}

```

특정 값만 상수로 바꿀수도 있습니다.

```tsx
const userInfo = {
    name: "zero" as const,
    age: 20,
    isMale: true
}
userInfo.name = "sugar" // TS2540: Cannot assign to 'name' because it is a read-only property.
userInfo.age = 30

```

### partial

partial은 일정한 부분만 추출해서 사용할 수 있습니다.

```tsx
type UserType = {
    name: string
    age: number
    isMale: boolean
}
// 타입들이 무조건 필요하지않고 있어도되고 없도도 됩니다. 옵셔널 타입과 같습니다.
const userPartial: Partial<UserType>[] = [
    {name: "sugar"},
    {age: 20},
    {isMale: false},
    {}
]

```

### omit

omit은 해당 타입을 제외한 나머지 부분만 사용을 합니다. 여러개를 제외하고 싶다면 `|` 연산자를 이용합니다. pick의 반대입니다.

```tsx
const userOmit1: Omit<UserType, "name"> = {
    isMale: false,
    age: 20
}

const userOmit2: Omit<UserType, "age" | "name"> = {
    isMale: false,
}

```

### pick

pick은 일정한 타입 부분만을 추출해서 사용하기 위해서 사용합니다. 여러개를 사용하고 싶다면 `|` 연산자를 이용합니다. omit의 반대입니다.

```tsx
const userName: Pick<UserType, "name"> = {
    name: "sugar"
}

const userNameWithAge: Pick<UserType, "name" | "age"> = {
    name: "sugar",
    age: 30,
}

```

### Extract

`Extract<T, U>` Extract에는 T에 포함되는 U중에 일치하는 않는 값만 들어갈 수 있습니다.
Type에는 Union타입들이 들어가고 해당 Union 들어갈 수 있는 값들이 들어갑니다. Union에 값을 `|`을 이용하여 추가할 수 있습니다.

```tsx
type arrayType = "top" | "left" | "right" | "bottom";
type topWithType = Extract<arrayType, "top"> // "top"

let isTop: topWithType = "top";
// arrayType에 "top"로 들어갈 수 있는건 "top" 뿐입니다.

```

### ExClude

`Exclude<T, U>` ExClude에는 T에 포함되는 U중에 일치하지 않는 값만 들어갈 수 있습니다.

```tsx
type topWithOutType = Exclude<arrayType, "top">

let isNotType: topWithOutType = "bottom";
isNotType = "right"
// "top"을 제외한 모든 값들이 들어갈 수 있습니다.

```

### returntype

~~함수의 설계서와 같이 함수의 인수부터 반환까지의 타입을 지정하여 추출해줍니다. 반환타입을 추론하거나 다른 곳에서 사용할 때 유용합니다~~

함수 `Type`의 반환 타입으로 구성된 타입을 생성합니다.

```tsx
type MakeUserType = ReturnType<(userInfo: UserType) => void> // 해당 타입은 void가 반환이 되었기 때문에 void타입으로만 사용할 수 있습니다.

function userMarker(newUser: UserType): MakeUserType {
    console.log(newUser)
    return;
}

userMarker({age: 20, isMale: true, name: "zero"});

// MakeUserType이라는 리턴타입의 지정된 인수와 다르거나 리턴타입이 다르면 오류가 발생합니다.
function coffeeMaker(coffee):MakeUserType{
    return "맛있는 커피" // TS2322: Type 'string' is not assignable to type 'void'.
}

type UserInfoName = ReturnType<(student: StudentType) => string>
// 해당 타입은 string을 반환을 받았습니다 때문에 string 타입입니다.
    
const std_name:UserInfoName = 'zero'

```

### optional

optional 타입은 해당 타입을 전달을 받아도되고 안받아도 상관이 없습니다.

```tsx
type StudentType = {
    number?: number,
    name: string,
}

const st_zero: StudentType = {
    number: 0, name: "zero"
}

const st_one: StudentType = {
    number: 1, name: "sugar"
}

const teacher: StudentType = {
    name: "zl존성용"
}

```

### satisfies

satisfies는 객체 타입의 검사용으로 사용이 됩니다. 이는 타입스크립트 4.9 버전에서 출시한 것으로 기존에는 Record 타입으로 검사가 가능하였습니다.

```tsx
const Human: Record<'name' | 'age' | 'wishMovieList', string | string[]> = {
    name: "zero",
    age: "30",
    wishMovieList: ["aboutTime", "noteBook"]
}

// 위 코드에서는 문제점을 발견하지 못합니다. 하지만 아래에서 문제가 발생합니다.
Human.name.toUpperCase()

// name의 타입이 string | number | string[] 타입으로 인식이 되는 바람에 toUpperCase()를 사용하지 못하는 것입니다.
// satisfies를 사용한다면 타입을 알려줄 수 있습니다.

const isHuman = {
    name: "zero",
    age: "30",
    wishMovieList: ["aboutTime", "noteBook"]
} satisfies Record<'name' | 'age' | 'wishMovieList', string | string[]>

isHuman.name.toUpperCase()
// isHuman.name을 string으로 인식을 하기 때문에 toUpperCase()를 사용할 수 있습니다.

```

### generic

generic은 전달받은 타입을 기준으로 정해진 위치에 해당 타입에 대한 정보를 넣어줍니다.

```typescript
type UserGenericType<T, U, C> = {
    name: T
    age: U,
    isMan: C
}

const newUser1: UserGenericType<string, number, boolean> = {
    name: "zero",
    age: 20,
    isMan: true
}

// 지금 같은 경우에는 T에 number가 들어갔기 때문에 name에서 number 타입의 값을 원하고 있습니다.
const newUser2: UserGenericType<number, string, boolean> = {
    name: "zero", // TS2322: Type 'string' is not assignable to type 'number'.
    age: "20",
    isMan: true
}

// 리액트의 useState의 타입을 보면 제네릭이 잘 적용되어있는 것을 볼 수 있습니다.
// 전달 받은 타입으로 값의 타입이 만들어지고 해당 값이 변환되는 함수가 있고 반환도 해당 타입으로 나와집니다.
type useStateType = ReturnType<<T>(initialState:T)=>[item:T, setItem:DisPatch<setStateAction<T>>]>
```


---

---

## **TASK.3** **타입스크립트 바로 잡기**

### 타입스크립트의 장점

1. 문서화 작업 : 개발 규모가 커질수록 해당 변수에 무슨 타입이 들어가 있는지 모르는 경우가 많습니다. 때문에 타입을 지정을 해둘 경우 @JSDOC 와 같이 문서화를 통해 어느 파일인지 설명 글을 달 수도 있고 타입을 통해서 해당 변수나 함수에 어느 파라미터 값이 들어가야 하는지 알 수도 있습니다. 이를 통해 다른 개발자와 소통하는데에 있어서 타입이 중요합니다.


2. 생산성 : 타입이 지정이 되어있을 경우 자동 완성을 지원합니다.

    다음과 같이 인터페이스가 지정이 되어있다고 가정을 해보겠습니다.
    ```typescript
    interface IUserInfo {
    userName : string,
    userAge : number,
    userGender : boolean
    }
    ```
   객체를 만들 때 무슨 값이 있어야 하는지 안 넣은 게 없는지 헷갈린다면 type을 지정해주면 됩니다.

    그럴 경우 다음과 같이 객체에 대해 자동 완성이 가능하고 타입까지 확인할 수 있습니다. 만약 안 넣은 객체의 키 값이 있다면 오류를 통해서 넣어 달라고 알려줍니다. 이 상황에서는 그저 객체의 값 하나만 넣는다고 가정을 하고 만들었지만 만약 배열을 통해 목 데이터와 같이 반복되는 값들을 설정 해야 한다면 유용하게 사용할 수 있습니다.


4. 안정적인 개발 환경 : 타입스크립트는 컴파일 이전에 에러를 검사하고 알려줍니다. 리액트나 자바스크립트를 사용할 때는 코드에서 에러를 알려주지 않았습니다. (알려주긴 하더라도 친절하게 알려주진 않았습니다) 하지만 타입스크립트를 통해 개발을 하게된다면 컴파일 이전에 자동으로 타입검사를 해주고 이건 나올 수 없는 타입이야 처럼 알려주기도 합니다.

#### 타입스크립트의 단점
1. 어려운 언어 : 자바스크립트는 동적 언어로 선언시에 타입이 정해지는 것이 아닌 할당시에 타입이 정해졌습니다. 하지만 타입스크립트는 선언시에 타입이 정해지므로 자바스크립트이고 기존에 보지 못한 유틸리티 타입으로 인해 자바스크립트가 익숙한 개발자들에게는 어렵게 다가올 수 있습니다.


2. 타입 정의로 인한 시간 소모 : 가벼운 프로젝트를 할 경우 타입이 굳이 필요한가 생각이 들 때가 있습니다. 예를 들어 이름과 전화번호만 가지고 있는 타입이 있다고 하면 일일이 타입을 지정을 해줘야 하다는 것이 있겠죠 함수마다, 컴포넌트마다, 객체마다, 변수마다 하나씩 만들고나면 프로젝트의 크기가 커지고 이에 많은 시간을 소모하게 됩니다. 하지만 이로인해 얻을 수 있는 장점이 더 많은 것 같습니다. (ex : 타입 추론, 자동 완성)

---

---

## **TASK.4 React의 Typescript**

### 1. React.FC를 사용을 지양해야 하는 이유?

이전에 Meta 팀에 올라왔던 [PR 문서](https://github.com/facebook/create-react-app/pull/8177)입니다. 해당 문서는 승인되어 이제 React.FC를 사용하지 않더라도 컴포넌트를 만들 수 있게 되었습니다. 해당 링크에서는 다음과 같은 이유로 FC를 지양해야 한다고 말을 하고 있습니다.

1. React.FC의 children 속성을 암시적으로 허용합니다.

   React.FC를 사용하면 children 속성을 암시적으로 허용합니다. 이는  모든 컴포넌트들이 children을 허용하지 않더라도 아래와 같은 코드를 허용한다는 얘기입니다.

    ```tsx
    const App: React.FC = () => { /*... */ };
    const Example = () => {
    	<App><div>Unwanted children</div></App>
    }
    ```

   이는 타입이 정확해야하는 타입스크립트의 목적과 맞지 않는 방법으로 children이 사용안되는 컴포넌트가 있음에도 불구하고 다음과 같이 React.FC를 정의하면 사용할 수 있게 됩니다.


2. 제네릭을 지원하지 않습니다.

   다음과 같은 타입이 있습니다.

    ```tsx
    type GenericComponentProps<T> = {
       prop: T
       callback: (t: T) => void
    }
    const GenericComponent = <T>(props: GenericComponentProps<T>) => {/*...*/}
    ```

   제네릭으로 타입과 해당 타입을 인자로 받는 함수가 있습니다.

    ```tsx
    const GenericComponent: React.FC<GenericComponentProps<T>>=(props) => {/*...*/}
    ```

   하지만 React.FC를 사용하면 완성되지 않은 해당 제네릭을 컴포넌트를 만들 때 전달하지 못하게 됩니다.

    ```tsx
    const App = () => {
    	return <GenericComponent prop="example" callback={(value) => console.log(value)}/> // 제네릭에 대한 타입을 주지 못합니다.
    }
    ```

   해당 방법은 타입 추론을 통해 value의 값이 string으로 넘어가는 것은 확인할 수 있지만 명시적으로 전달을 하는 것은 힘듭니다.

   React.FC를 사용하지 않는 다면 다음과 같이 전달할 수 있습니다.

    ```tsx
    const MainPage = <T, >() => (
        <main>This is MainPage</main>
    );
    
    function App() {
      return (
        <div>
          <MainPage<string> />
        </div>
      );
    }
    
    export default App;
    ```


### 2.ReactNode

`ReactNode` 타입은 `children` 에 가장 많이 사용되는 타입 중 하나입니다.

```tsx
// ReactChild 타입에 string, number 타입이 포함되어 있습니다.
type ReactNode = 
ReactChild | 
ReactFragment | 
ReactPortal | 
boolean | 
null | 
undefined;
```

`jsx` 내에서 사용할 수 있는 모든 타입(원시타입까지 포함)들을 의미합니다. 즉 `string`, `null`, `undefined` 등을 포함하는 가장 넓은 범위를 갖는 타입입니다.


💡 함수형 컴포넌트의 반환 타입을 React.ReactNode로 교체하여 해당 유형을 수정해줄 수 있습니다.


### 3.ReactElement

`ReactElement` 는 `createElement` 함수를 통해 생성된 객체의 타입입니다. `ReactNode` 와 달리 원시타입을 허용하지 않고 완성된 `JSX` 요소만을 허용합니다.


💡 `ReactNode` 타입이 `ReactElement` 타입을 포함하고 있는 관계임을 확인할 수 있습니다.



원시타입 리터럴을 `children` 속성으로 사용하려면 에러를 출력합니다. 따라서 `ReactElement` 타입은 자식 요소로 하나의 “컴포넌트를” 받는 것을 강제해야 하는 상황에 사용할 수 있습니다.

### 4.PropsWithChildren

`PropsWithChildren` 은 해당 prop이 children을 가지고 있을 수도 있고 없을 수도 있다고 명시를 해주고있습니다.

아래는 실제로 사용된 코드입니다.

```tsx
type PropsWithChildren<P = unknown> = P & { children?: ReactNode | undefined };
```

하지만 typescript에서는 타입에 엄격해야하므로 children이 optional로 들어가있는 것은 좋지않다고 봅니다. 따라서 다음과 같이 children을 강제하는 타입을 따로 만들어서 사용하면 좋을 것 같습니다.

```tsx
import {ShouldHaveChildren} from "../types/customType";
import {ReactNode} from "react";

export type ShouldHaveChildren = {
    children: ReactNode
}

const MainPage = <T, >(props:ShouldHaveChildren) => (
    <main>This is MainPage</main>
);

export default MainPage;
```

### 5.PropsWithRef

`PropsWithRef`에 하기 전에 ref에 대해 먼저 생각을 해보았습니다. Ref란? html에서 참조. 이름표를 달기 위해 붙이는 속성으로 DOM 요소에 접근하기 위해서 사용하는 것으로 기억을 하고 있습니다. 한 페이지에서 있다고 생각하고 코드를 짜면 다음과 같습니다.

```tsx
import React from "react";

type InputComponentType = {
    ref: React.RefObject<HTMLInputElement>
}

const InputComponent = (props: InputComponentType) => {
    return <input ref={props.ref}/>
}

const MainPage = () => {
    const inputRef = React.useRef<HTMLInputElement>(null)

    const onSubmit = () => {
        console.log(inputRef.current?.value)
    }
    return (
        <main>
            <InputComponent ref={inputRef}/>
            This is MainPage
            <button type={"button"} onClick={onSubmit}>submit</button>
        </main>
    )
};

export default MainPage;
```
경고가 두 가지 나오는 것을 확인할 수 있습니다.

첫 번째 경고로는 `ref`를 컴포넌트의 속성(props)를 넘겼기 때문에 생기는 문제입니다. 리액트에서는 `ref`를 특별한 속성으로 취급을 하기 때문에 props로 넘길수가 없습니다. 따라서 다른 방법을 찾아보아야합니다.

두 번째 경고로는 함수 컴포넌트에 직접 `ref` 를 전달하였기 때문에 생기는 오류입니다. 함수 컴포넌트는 기본적으로 `ref` 를 받을수가 없습니다. 따라서 **친절하게** `React.forwardRef()`를 사용하는 것이 어때? 라고 알려주고 있습니다.

그럼 친절에 보답하는 형식으로 코드를 다음과 같이 수정하여 작성을 해줍니다.

```tsx
const InputComponent = React.forwardRef<HTMLInputElement>((props, ref) => {
    return <input ref={ref}/>
})
```

`forwardRef` 의 제네릭 인자로 ref의 타입을 넣어줍니다. 그럼 다음과 같이 정상적으로 나오는 것을 확인할 수 있습니다.

하지만 저희가 원하는 것은 `PropsWithRef` 바로 `Props`와 함께 `ref`를 넘기는 것입니다.

`PropsWithRef`를 공식문서를 읽지 않고 `PropsWithChildren` 처럼 사용해볼려고 했는데 막혔습니다 ㅠ. 코드는 다음과 같습니다.

```tsx
type PropsWithRef<P> =
    // Just "P extends { ref?: infer R }" looks sufficient, but R will infer as {} if P is {}.
    "ref" extends keyof P
        ? P extends { ref?: infer R | undefined }
            ? string extends R ? PropsWithoutRef<P> & { ref?: Exclude<R, string> | undefined }
            : P
        : P
        : P;
```

여기서 `PropsWithRef<P>`는 제네릭 타입 `P`를 입력으로 받고, `P` 타입에 `ref` 속성이 포함되어 있는지 확인합니다. ( ~~*아래 글은 다시봐도 잘 모르겠습니다.*~~ )

1. `if ("ref" extends keyof P)` 부분은 `P` 타입에 `ref` 속성이 존재하는지 확인합니다. 존재하면 `if` 블록 내부의 로직을 실행합니다.
2. `P extends { ref?: infer R | undefined }`는 `P` 타입이 `{ ref?: infer R | undefined }` 형태인지 확인합니다. 여기서 `infer R`은 `ref` 속성의 타입을 추론합니다.
3. `"string" extends R`는 `R`이 문자열로 추론되는 경우를 확인합니다. 문자열로 추론되면 `ref` 속성을 제외한 `props`를 반환하고 `ref` 속성의 타입은 `string`이 아닌 것으로 처리됩니다.
4. 그렇지 않으면 `ref` 속성을 포함한 `props`를 그대로 반환합니다.
5. 마지막으로, `if` 조건을 만족하지 않는 경우 `PropsWithRef<P>`는 입력된 `P` 타입을 그대로 반환합니다.

즉 props로 전달 받은 값 중에 ref가 있는지 검사하는 로직입니다. 또한 props 타입또한 같이 넘겨줄 수 있습니다.

사용 방법은 다음과 같습니다.

```tsx
import React, {PropsWithRef} from "react";

const InputComponent: React.FC<PropsWithRef<{
    num: number,
    ref: React.Ref<HTMLInputElement>
}>> = React.forwardRef((props, ref) => {
    return (
        <>
            제 나이는 {props.num}입니다.
            <input ref={ref}/>
        </>
    )
})

const MainPage = () => {
    const inputRef = React.useRef<HTMLInputElement>(null)

    const onSubmit = () => {
        console.log(inputRef.current?.value)
    }
    return (
        <main>
            <InputComponent num={20} ref={inputRef}/>
            This is MainPage
            <button type={"button"} onClick={onSubmit}>submit</button>
        </main>
    )
};

export default MainPage;
```

결론 props를 사용하는 경우 `PropsWithRef`를 props가 없는 경우 `forwardRef`만 사용하면 됩니다.

### 6. RefObject

useRef의 반환타입인 RefObject의 current 속성을 이용해서 Dom객체에 접근합니다. 아래는 타입스크립트 내장 코드입니다.

```tsx
interface RefObject<T> {
    readonly current: T | null;
}
```

여기서 의문점이 듭니다. 왜 current 속성이 있는 지를 확인을 하는거지? HTMLElement 타입은 애들만 받아서 사용하면 되는거 아닌가? current를 사용하면 되는거 아닌가?

⇒ 모든 HTMLElement에는 current 속성이 내장되어 있지 않습니다. current 속성은 useRef 또는 createRef와 같은 리액트 레퍼런스의 객체의 형식으로 사용이 됩니다. 또한 useRef를 만들 때 해당 값이 연결이 될 수 있지만 초기 값이 null 이기 때문에 `T | null` 형태로 받아옵니다.

이후 받아온 값 .current로 접근할 수 있습니다. *readonly 이기 때문에 수정은 불가능합니다.

### 7. SetStateAction

기존의 타입을 넘겨줄 때는 다음과 같이 전달을 하였습니다.

```tsx
const CountComponent = (props: { count: number }) => {
    return <div>{props.count}</div>
}

const CountAddButton = (props: { addHandling: () => void }) => {
    return <button onClick={props.addHandling}>add</button>
}

const MainPage = () => {
    const [count, setCount] = useState(0)
    return (
        <main>
            <CountComponent count={count}/>
            <CountAddButton addHandling={() => setCount((v) => ++v)}/>
        </main>
    )
};
```

여기서 유심히 봐야하는 부분이 있습니다 바로 count와 setCount 부분인데요. count는 상태로서 변경이 되는 값이고 setCount는 그런 상태 값인 count를 변경해주는 함수입니다. 리액트에서는 이렇게 변경이 되는 함수를 다음과 같이 `SetStateAction` type으로 정의를 해두었습니다. SetStateAction의 생김새는 다음과 같습니다.

```tsx
type SetStateAction<S> = S | ((prevState: S) => S);
```

초기 인자로서 초기 값을 불러올 수도 있고 아니면 정해진 값을 리턴 할 수 있습니다. 이를 통해 상태 값을 변경할 수 있습니다.

지금 위에 함수에서는 다음과 같이 전달을 받은 함수를 실행만 해주고 있습니다.

```tsx
const CountAddButton = (props: { addHandling: () => void }) => {
    return <button onClick={props.addHandling}>add</button>
}
```

만약 여기서 우리가 직접 값을 주고싶을땐 어떻게 해야할까요?

```tsx
const CountAddButton = (props: { addHandling: (num: number) => void }) => {
    return <>
        <button onClick={() => props.addHandling(1)}>1</button>
        <button onClick={() => props.addHandling(2)}>2</button>
        <button onClick={() => props.addHandling(3)}>3</button>
        <button onClick={() => props.addHandling(4)}>4</button>
    </>
}

const MainPage = () => {
    const [count, setCount] = useState(0)
    return (
        <main>
            <CountComponent count={count}/>
            <CountAddButton addHandling={setCount}/>
        </main>
    )
};
```

다음과 같이 설정할 수 있습니다. 지금은 손을 올려 두었을때 숫자를 입력받아 실행하는 함수 정도로만 표시가 되어있습니다.


이곳에서 우리는 addHandling이 그저 number를 입력을 받아 void 반환값을 갖는 함수라고만 알고있습니다. 하지만 실제로는 값을 입력을 받아 상태 값을 변경해주는 함수이지요.

리액트에서는 다음과 같이 상태를 업데이트 해주는 함수에 대해서 타입을 정의할 수 있게 설계를 해두었습니다.

```tsx
const CountAddButton = (props: { addHandling: SetStateAction<number> }) => {
    return <>
        <button onClick={() => props.addHandling(1)}>1</button>
        <button onClick={() => props.addHandling(2)}>2</button>
        <button onClick={() => props.addHandling(3)}>3</button>
        <button onClick={() => props.addHandling(4)}>4</button>
// TS2349: This expression is not callable.   Not all constituents of type 
// 'SetStateAction<number>' are callable.     Type 'number' has no call signatures.
    </>
}
```

SetStateAction을 통해서 전달받아야하는 값을 건네받을 수 있습니다. 하지만  이렇게만 사용을 한다면 에러가 납니다. Dispatch와 합쳐서 상태를 변경을 해주어야 합니다.

### 8. Dispatch

Dispatch를 통해서 상태 변경을 감싸줄 수 있습니다. 이는 SetStateAction을 인자로 받아서 값을 변경 시킬 수 있습니다. Dipatch는 액션을 처리하는 동작을 처리해주는 타입을 나타냅니다.  그래서 다음과 같이 사용 할 경우 상태를 변경하는 함수라는 것을 가독성 좋게 알려줄 수 있습니다.

```tsx
const CountAddButton = (props: { addHandling: Dispatch<SetStateAction<number>> }) => {
    return <>
        <button onClick={() => props.addHandling(1)}>1</button>
        <button onClick={() => props.addHandling(2)}>2</button>
        <button onClick={() => props.addHandling(3)}>3</button>
        <button onClick={() => props.addHandling(4)}>4</button>
    </>
}
```

---

---

## **TASK.5 문제 풀어보기**

1. 타입을 주어야하는 경우와 주지 않아도 되는 경우를 구분하여 타입을 정의하세요

```jsx
let seongyong = {
    age: 20,
  height: 190,
}

function log(obj){
	console.log(obj.height) // obj에 height라는 값이 있어? 오류가 나옵니다.
  return obj
}

const a = log(seongyong)
console.log(a.age) // log(seogyong)을 하면 age가 있는 값이 있어? 오류가 나옵니다.
```
따라서 오류가 나오지 않게 `seongyong` 값에 타입을 부여해줍니다.

```typescript
type UserType = {
    age: number
    height: number
    // 해당 타입을 받는 코드는 아 이 타입을 쓰는 객체는 다음과 같이 생겼구나 라는 사실을 알게됩니다.
}

function log(obj: UserType){
    // UserType만 파라미터로 받는 함수를 만듭니다. return 타입의 경우 타입추론이 가능하기 때문에 에러가 생기지 않습니다.
    console.log(obj.height)
    return obj
}

```

2. type alias와 interface의 차이를 이해해보기

```typescript
type Usertype = {
    userName: string
    userAge: number
    userGender: "male" | "female"
}

type StudentUser = Usertype & { // 여러개의 타입을 합칠 때에는 & 연산자를 사용합니다.
    schoolTitle: string
    schoolNumber: number
}

interface IUserInfo {
    userName: string
    userAge: number
    userGender: "male" | "female"
}

interface IStudentInfo extends IUserInfo { // 인스턴스를 상속을 받을 때에는 extends 키워드를 사용합니다.
    schoolTitle: string
    schoolNumber: number
}
```
둘의 차이는 선언적 병합을 하는 방식말고의 차이는 못느끼겠습니다. 실제로 컴파일을 하고난뒤에 속도같은 것을 비교를 해봐도 별 차이가 없습니다. 하지만 ```interface```의 경우 예로부터 설계도 라는 인식으로 사용이 되어왔습니다. 따라서 구분을 하기 위한 정도로 분리해서 사용하는 것도 좋을거 같긴 합니다만 굳이 안나눠도 될 꺼 같습니다.

```interface``` : api로 받아오는 객체의 타입의 경우(명세서의 역할) 사용합니다. interface임을 나타내기 위에 앞에 ```I``` 를 붙이는 것도 좋습니다.

```type``` : type의 경우 프로젝트를 하면서 직접 만들 타입의 경우 사용합니다.

3. react-typescript 적용하기

알맞은 타입을 부여하여 에러상황 해결하기

문제 1. main의 Button 컴포넌트에 정의되지 않은 Props 보낼 경우
해결 : onClick의 경우 ```...rest``` 받아오고 있습니다. 타입을 부여해줌으로서 사용이 가능합니다.

해결해야 하는 props는 variant, size, children과 같이 있습니다. 

children을 제외한 나머지 타입들은 받아와도되고 안받아와도 됩니다. 따라서 ```Partial```이라는 타입이 떠오릅니다.

다음과 같이 코드를 만들수 있습니다.

```typescript
import {PropsWithChildren} from "react";

type ButtonType = {
    variant: 'primary',
    size: 'small',
    onClick: () => void
}

const Button = ({variant, size, children, ...rest}: PropsWithChildren<Partial<ButtonType>>) => {
    return (
        <button ...
```

만약 children 타입을 강제로 주고싶다면 다음과 같이 주면됩니다.

```typescript
type NeedChildren = {
  children: ReactNode;
};

const Button = ({ variant, size, children, ...rest }: Partial<ButtonType> & NeedChildren) => {
  return (
```
문제 2. todo의 경우 useState의 타입이 지정이 안되어있기에 에러가 발생합니다. 따라서 useState의 어느 값이 들어갈 수 있는지 알려줘야합니다.

useState의 코드의 경우 다음과 같이 생겼습니다.
```typescript
function useState<S>(initialState: S | (() => S)): [S, Dispatch<SetStateAction<S>>];
```

전달 받은 타입의 변수로 해당 값들을 사용할 수 있고 설정을 할 수 있습니다.
```typescript
type Todo = {
  title: string,
  content: string,
  state: boolean
}

const Todo = () => {
  const [todoLsit, setTodoLsit] = useState<Todo[]>([]);
  ...
```
다음과 같이 작성을 할 시에 해당 todoLsit는 Todo type의 배열로 인식을 하고있기 때문에 객체의 키값을 가져올 때 오류가 나지 않습니다.

one-todo에서도 사용을 하기 때문에 ```export``` 하여 내보내줍니다.

```typescript
export type Todo ={
    ...
   
// one-todo.jsx
import { Todo } from '..';

const OneTodo = ({ todo }: { todo: Todo }) => {
   return (

```

다음과 같이 타입을 전달함으로서 에러를 해결 할 수 있습니다.

