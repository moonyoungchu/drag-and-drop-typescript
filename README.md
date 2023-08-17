# Typescript

---

typescript를 터득해보자💪

---
</br>

![localstorageimg](./dragdrop.gif)

- 실행 명령

```jsx
npm start

tsc -w
```

</br>

### 타입 (type)

1. **원시 타입 (Primitive Types):**
    - `number`: 숫자를 나타내는 타입입니다. 부동소수점 숫자와 정수를 모두 포함합니다.
    - `string`: 문자열을 나타내는 타입입니다.
    - `boolean`: 참(`true`) 또는 거짓(`false`) 값을 나타내는 타입입니다.
    - `null`: 값이 없음을 나타내는 타입입니다. 변수에 명시적으로 할당되는 값으로 사용됩니다.
    - `undefined`: 값이 할당되지 않음을 나타내는 타입입니다.
    - `symbol`: 고유하고 변경 불가능한 값을 나타내는 타입입니다. 주로 객체 속성의 식별자로 사용됩니다.
    - `bigint`: 매우 큰 정수 값을 나타내는 타입입니다.
2. **객체 관련 타입 (Object-related Types):**
    - `object`: 비원시 값을 가지는 모든 객체를 나타내는 타입입니다.
    - `array`: 배열을 나타내는 타입입니다. `number[]`, `string[]` 등과 같이 타입 뒤에 `[]`를 붙여서 사용합니다.
    - `tuple`: 고정된 요소 수와 각 요소의 타입을 미리 지정한 배열을 나타내는 타입입니다.
    - `enum`: 열거형을 나타내는 타입으로, 숫자나 문자열 값 집합에 이름을 부여할 수 있습니다.
    - `any`: 모든 타입을 허용하는 동적 타입입니다. 타입 검사를 우회하거나 필요한 경우에 사용됩니다.
3. **함수 관련 타입 (Function-related Types):**
    - `function`: 함수를 나타내는 타입입니다. 매개변수와 반환 타입을 명시할 수 있습니다.
    - `void`: 반환값이 없음을 나타내는 타입입니다. 함수의 반환 타입으로 사용됩니다.
4. **변수 타입 결합 (Variable Type Combinations):**
    - `union`: 여러 타입 중 하나를 가질 수 있는 타입입니다. `number | string`와 같이 사용합니다.
    - `intersection`: 두 개 이상의 타입을 조합하여 새로운 타입을 만드는 타입입니다.
5. **기타 타입 (Miscellaneous Types):**
    - `never`: 절대로 발생하지 않는 값을 나타내는 타입입니다. 예를 들어 항상 예외가 발생하는 함수의 반환 타입으로 사용됩니다.
    - `unknown`: `any`와 유사하지만, `unknown`은 더 엄격한 타입 검사를 받아야 합니다.
    - `null`과 `undefined`의 타입은 각각 `null`과 `undefined`로 사용됩니다.

### 배열 타입

```tsx
let list = number[] = [1,2,3];
let member: string[]=["일","이","삼"];
```

### 함수 표현

매개변수 뒤에 :타입 을 입력하고, 괄호 뒤에는 함수가 반환하는 :타입 을 입력한다. 반환 타입이 없는 경우 :void로 입력한다.

```tsx
function inChildren(age:number):boolean{
	return age<19;
}
```

### Decorator

- 데코레이터는 클래스, 메서드, 속성 등에 추가적인 기능을 부여하는 데 사용.

`@autobind` 데코레이터는 클래스의 메서드에 적용됩니다. 
주어진 코드에서 `@autobind`가 `submitHandler` 메서드 위에 적용되어 있기 때문에 `submitHandler` 메서드에 대해 자동 바인딩이 수행됩니다.

따라서, `@autobind` 데코레이터를 사용하면 `submitHandler` 메서드가 항상 현재 인스턴스에 바인딩된 채로 호출되게 됩니다. 이는 주로 이벤트 핸들러와 같이 메서드가 다른 문맥(context)에서 호출될 때, 원본 메서드와 바인딩을 유지하고자 할 때 유용합니다.

```tsx
function autobind(
    _: any,
    _2: string,
    descriptor: PropertyDescriptor
) {
    const originalMethod = descriptor.value;
    const adjDescriptor: PropertyDescriptor = {
        configurable: true,
        get() {
            const boundFn = originalMethod.bind(this);
            return boundFn;
        }
    };
    return adjDescriptor;
}

class ProjectInput {
    ...

    **@autobind //**데코레이터(decorator)
    private submitHandler(event: Event) {
        event.preventDefault();
        ...
    }
}
```

### interface

- **`interface`**는 객체의 스펙. **상호간에 정의한 약속 혹은 규칙을 의미**
- 인터페이스를 인자로 사용할 때, 정의한 프로퍼티와 타입의 조건을 만족한다면, 인자로 받는 객체의 프로퍼티 개수나 순서는 같지 않아도 된다.

인터페이스는 속성, 메서드, 인덱서(indexer) 등으로 구성될 수 있으며, 이를 통해 개발자가 코드의 일관성과 타입 안정성을 유지할 수 있습니다. 인터페이스는 클래스, 객체, 함수 등 다양한 구조에 적용될 수 있습니다.
인터페이스는 타입 체크의 역할을 수행하며, 특정 타입이 인터페이스의 요구사항을 충족시키는지를 검사할 수 있습니다. 이를 통해 컴파일러가 코드를 분석하고 타입 에러를 포착하거나 자동 완성 기능 등을 제공할 수 있습니다.

```tsx
//객체의 스펙
interface User {
	name: string;
	age: number;
}

let user1: User{
	name: "영희",
	age: 20,
}

interface AddNumber {
	(x: number, y: number): number; // return 해주는 값이 없을 땐 void
}

let addNumber: AddNumber = (x,y)=>{
	return x+y;
}

addNumber(10,10);// result:20
```

### implements

- implements로 미리 정의된 인터페이스를 채택하여 클래스를 정의할 수 있다.
- 인터페이스로 정의한 프로퍼티나 메서드는 해당 클래스에 **필수적으로 들어가야하며**, 오버라이딩 해서 내용을 구현해야 한다.

**`implements`** 키워드는 TypeScript에서 클래스가 특정 인터페이스를 구현(Implement)한다는 것을 나타내는 역할을 합니다.

```tsx
interface MyInterface {
  method1(): void;
  method2(): string;
}

class MyClass implements MyInterface {
  method1() {
    // 구현 내용
  }

  method2() {
    // 구현 내용
    return "result";
  }
}
```

### ? (옵셔널(optional) 속성)

- 속성을 사용하지 않아도 무방

**`?`** 기호는 TypeScript에서 옵셔널(optional) 속성을 나타냅니다. 인터페이스 또는 타입에서 속성 뒤에 **`?`**를 붙이면 해당 속성은 선택적으로 사용할 수 있음을 의미합니다. **옵셔널 속성은 해당 속성의 값이 있을 수도 있고 없을 수도 있다는 것을 나타냅니다.** 즉, 해당 속성을 사용하는 코드에서 값이 제공되지 않으면 기본값이나 초기화되지 않은 값으로 처리될 수 있습니다.

### ! (non-null assertion operator)

**`!`**는 non-null assertion operator(비-널 어설션 연산자)라고 불리며, 타입스크립트에서 변수가 null 또는 undefined가 될 수 없음을 명시적으로 나타냅니다. 

즉, **`getElementById()`**의 결과가 null일 가능성을 제거하고, **`HTMLUListElement`** 타입으로 단언한다는 의미입니다.

```tsx
const listEl = document.getElementById("test")! as HTMLUListElement;
```

### readonly 읽기전용

- 인터페이스를 사용하여 객체를 생성할 때, 값 할당후 변경 불가 속성을 의미.

```tsx
interface User{
	readonly name: string;
}

let person:User = {
	name: "Jin"
};

person.name = "Jimin"; //Error!!
```

### enum

Enum은 특정 값들의 집합을 나타냅니다.

```tsx
//프로젝트의 상태를 "Active"와 "Finished"로 나타내기 위해 다음과 같이 Enum을 사용할 수 있습니다
enum ProjectStatus{
    Active,
    Finished
}
```

### type (커스텀타입)

- 새로운 타입을 정의하기 위해 사용됩니다.

 `type`을 사용하여 타입 별칭(Type Alias)을 생성하거나, 유니온 타입(Union Type), 인터섹션 타입(Intersection Type), 제네릭 타입(Generic Type) 등을 정의할 수 있습니다. 
타입 별칭(Type Alias)은 기존 타입에 대해 새로운 이름을 지정하는 것으로, 코드의 가독성을 높이고 반복적인 타입 정의를 줄이는 데 도움을 줍니다.

```tsx
//**type Listener**는 **Project[]** 형식의 매개변수를 받아들이고 아무 것도 반환하지 않는 함수 타입입니다.
type Listener = (items: Project[]) => void;

type Centimeeter = number;
```

### 인터페이스와 타입 별칭의 차이

- 가장 큰 차이 : 타입의 확장 가능 , 불가능 여부
- Typescript의 공식문서에서는 가능하다면 인터페이스를 사용하고, 인터페이스로 표현할수 없거나 유니온, 튜플을 사용해야하는 상황이라면 타입 별칭을 권장한다.
- 선언적 확장
    - 인터페이스 :
        - 새로운 속성을 추가하여 같은 이름으로 재정의하여 확장 가능.
        - extends를 사용하여 인터페이스 간 확장이 가능하다.
        - 인터페이스는 타입도 상속받을 수 있지만. 리터럴 타입은 불가능하다.
    - 타입 : 같은 이름으로 재정의 불가.
    
    ```tsx
    interface User {
    	name: string;
    }
    
    interface User{
    	age: number;
    } //같은 이름으로 정의하면 자동 확장됨.
    
    interface UserInfo extends User{
    	age: number;
    } //확장 가능
    ```
    
    ```tsx
    type User {
    	name: string;
    }
    
    type User{
    	age: number;
    } //Error!!!
    ```
    
- 타입의 확장
    
    extends 대신 **인터섹션(&)**을 사용하여 확장할 수 있다.
    
    타입을 상속받아 확장하는 개념이 아니라, **새로운 타입을 정의하는 것이다.**
    
    인터페이스도 확장이 가능하다.
    
    ```tsx
    type User {
    	name: string;
    }
    
    type UserInfo = User & {
    	age: number;
    } 
    
    let newUser: UserInfo = {
    	name: "Jin",
    	age : 20,
    }
    ```
    

### Generic(제네릭)

```jsx
type Listener<T> = (items: T[]) => void;
```

- T를 변수처럼 사용해 type을 지정해 줄 수 있다.

`<T>`는 TypeScript에서 제네릭(Generic) 타입을 나타냅니다.

주어진 코드에서 `<T>`는 제네릭 타입 매개변수로 사용되며, 이는 **사용자가 지정한 타입**을 나타냅니다.

제네릭 타입 `T`는 실제 사용자가 타입을 정의할 때 구체적인 타입으로 대체되며, 이를 통해 타입 안정성과 재사용성을 보장할 수 있습니다. `T`와 `U`는 일반적으로 제네릭 타입 변수로 사용되는 식별자입니다.

제네릭을 사용하기 시작하면, 제네릭 함수를 만들 때, 컴파일러가 함수 본문에 제네릭 타입화된 매개변수를 쓰도록 강요합니다. 즉, 이 매개변수들은 실제로 `any` 나 모든 타입이 될 수 있는 것처럼 취급할 수 있게 됩니다.

### Getter

- 클래스의 멤버로서, 해당 멤버에 접근할 때 특정 동작을 수행하는 함수입니다.
- 멤버 변수의 값을 반환하거나, 멤버 변수를 가공하여 반환하는 등의 역할을 할 수 있습니다.
- 메서드 형태로 정의되며, 속성 접근자(property accessor)로 사용됩니다.
- 인스턴스를 생성하고 Getter에 접근할 때는 함수 형태로 호출하는 것이 아니라 속성에 접근하는 것처럼 사용합니다. Getter는 멤버 변수에 직접 접근하지 않고 Getter 메서드를 호출하여 값을 얻습니다.

```tsx
get propertyName(): propertyType {
  // getter의 동작을 구현
  return propertyValue;
}

//propertyName: 접근하고자 하는 속성의 이름
//propertyType: 속성의 타입
//propertyValue: Getter가 반환하는 값
```

```tsx
class Product {
  private _price: number;
  private _discountRate: number;

  constructor(price: number, discountRate: number) {
    this._price = price;
    this._discountRate = discountRate;
  }

  get price(): number {
    return this._price;
  }

  get discountRate(): number {
    return this._discountRate;
  }

  get discountedPrice(): number {
    const discountAmount = this._price * (this._discountRate / 100);
    return this._price - discountAmount;
  }
}

const myProduct = new Product(1000, 20);
console.log(myProduct.price); // 1000
console.log(myProduct.discountRate); // 20
console.log(myProduct.discountedPrice); // 800
```

### Record

**`Record`**는 TypeScript에서 제공하는 내장 유틸리티 타입 중 하나입니다. 
**`Record<K, T>`**는 키 **`K`**와 값 **`T`**의 쌍으로 이루어진 객체를 나타내는 타입입니다.

예를 들어,
- **`Record<string, number>`**는 문자열 키와 숫자 값을 가지는 객체를 의미합니다. 
- **`Record<string, any>`**는 문자열 키와 어떤 타입의 값이든 허용하는 객체를 의미합니다.

**`Record`** 유틸리티 타입은 주로 객체의 타입을 명시할 때 사용됩니다. 특히, 객체의 키와 값의 타입이 일정한 패턴을 가지는 경우에 유용합니다.

```tsx
const myObj: Record<string, number> = {
  "a": 1,
  "b": 2,
  "c": 3,
};
```

### protected

- 해당클래스 내부와 상속받은 하위 클래스 내부에서만 접근

### public

- 클래스 내부/외부 어디에서나

### private

- 해당 클래스 내부에서만 접근 가능

```tsx
class ProjectInput {
    ...
    **private clearInputs() {**
        this.titleInputElement.value = '';
        this.descriptionInputElement.value = '';
    }
		...
}
```

### abstract class

- 상속용으로만 가능. 객체 인스턴스 생성이 불가능.
- 상속받은 클래스에서는 해당 추상 메서드를 반드시 구현(오버라이딩) 해야한다.
- 추상 클래스는 일종의 설계 틀로 사용되며, 하위 클래스들이 **어떤 메서드를 반드시 구현해야 하는 경우에** 유용하게 활용될 수 있습니다.

**`abstract class`**는 인스턴스를 생성할 수 없는 클래스입니다. 

이 클래스는 주로 하위 클래스에서 공통된 특성을 정의하고, 해당 클래스를 상속받은 하위 클래스에서 반드시 구현해야 하는 추상 메서드를 정의하는 데 사용됩니다. 추상 클래스 자체로는 직접 인스턴스를 생성할 수 없지만, 하위 클래스에서 이를 상속받아 기능을 확장하고 구현함으로써 사용됩니다.

### 유니온 타입

typescript 타입 중 하나로. 하나의 값이 여러개의 타입을 가지는 경우이다.

```tsx
let text: string | number = 22;
text = "22";
```
