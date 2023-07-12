# Typescript

---

2시간 40분짜리 강의를 통해 typescript를 터득해보자💪

---
</br>

- 실행 명령

```jsx
npm start

tsc -w
```

</br>

### Decorator

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
    templateElement: HTMLTemplateElement;

    constructor() {
        ...
    }

    **@autobind**
    private submitHandler(event: Event) {
        event.preventDefault();
        ...
    }
}
```

위의 코드에서 `@autobind`는 데코레이터(decorator)로 사용되고 있습니다. 

데코레이터는 클래스, 메서드, 속성 등에 추가적인 기능을 부여하는 데 사용됩니다.

`@autobind` 데코레이터는 해당 메서드가 호출될 때 자동으로 바인딩(bind)되도록 도와줍니다.

`@autobind` 데코레이터는 클래스의 메서드에 적용됩니다. 주어진 코드에서 `@autobind`가 `submitHandler` 메서드 위에 적용되어 있기 때문에 `submitHandler` 메서드에 대해 자동 바인딩이 수행됩니다.

따라서, `@autobind` 데코레이터를 사용하면 `submitHandler` 메서드가 항상 현재 인스턴스에 바인딩된 채로 호출되게 됩니다. 이는 주로 이벤트 핸들러와 같이 메서드가 다른 문맥(context)에서 호출될 때, 원본 메서드와 바인딩을 유지하고자 할 때 유용합니다.


</br>

### private method

TypeScript에서 **`private`** 키워드는 클래스 멤버인 메서드나 속성을 선언할 때 사용됩니다. 

**`private`**로 선언된 멤버는 해당 클래스 내에서만 접근할 수 있으며, 클래스 외부에서는 접근할 수 없습니다.

```tsx
class ProjectInput {
    templateElement: HTMLTemplateElement;
    descriptionInputElement: HTMLDivElement;

    constructor() {
        this.titleInputElement = document.getElementById('project-input')! as HTMLTemplateElement;
        this.descriptionInputElement = document.getElementById('app')! as HTMLDivElement;

    }

    **private clearInputs() {**
        this.titleInputElement.value = '';
        this.descriptionInputElement.value = '';
    }

		...

}
```


</br>

### interface

```tsx
interface Validatable {
    value: string | number;
    required?: boolean;
    minLength?: number;
    maxLength?: number;
    min?: number;
    max?: number;
}
```

**`interface`**는 객체의 구조를 정의하기 위해 사용되는 개념입니다. 

인터페이스는 속성, 메서드, 인덱서(indexer) 등으로 구성될 수 있으며, 이를 통해 개발자가 코드의 일관성과 타입 안정성을 유지할 수 있습니다. 인터페이스는 클래스, 객체, 함수 등 다양한 구조에 적용될 수 있습니다.인터페이스는 타입 체크의 역할을 수행하며, 특정 타입이 인터페이스의 요구사항을 충족시키는지를 검사할 수 있습니다. 이를 통해 컴파일러가 코드를 분석하고 타입 에러를 포착하거나 자동 완성 기능 등을 제공할 수 있습니다.



</br>

### ? (옵셔널(optional) 속성)

**`?`** 기호는 TypeScript에서 옵셔널(optional) 속성을 나타냅니다. 인터페이스 또는 타입에서 속성 뒤에 **`?`**를 붙이면 해당 속성은 선택적으로 사용할 수 있음을 의미합니다. **옵셔널 속성은 해당 속성의 값이 있을 수도 있고 없을 수도 있다는 것을 나타냅니다.** 즉, 해당 속성을 사용하는 코드에서 값이 제공되지 않으면 기본값이나 초기화되지 않은 값으로 처리될 수 있습니다.


</br>

### ! (non-null assertion operator)

```tsx
const listEl = document.getElementById("test")! as HTMLUListElement;
```

**`!`**는 non-null assertion operator(비-널 어설션 연산자)라고 불리며, 타입스크립트에서 변수가 null 또는 undefined가 될 수 없음을 명시적으로 나타냅니다. 

즉, **`getElementById()`**의 결과가 null일 가능성을 제거하고, **`HTMLUListElement`** 타입으로 단언한다는 의미입니다.



</br>

### enum

Enum은 특정 값들의 집합을 나타냅니다.

```tsx
//프로젝트의 상태를 "Active"와 "Finished"로 나타내기 위해 다음과 같이 Enum을 사용할 수 있습니다
enum ProjectStatus{
    Active,
    Finished
}
```


</br>


### type

새로운 타입을 정의하기 위해 사용됩니다. `type`을 사용하여 타입 별칭(Type Alias)을 생성하거나, 유니온 타입(Union Type), 인터섹션 타입(Intersection Type), 제네릭 타입(Generic Type) 등을 정의할 수 있습니다. 

타입 별칭(Type Alias)은 기존 타입에 대해 새로운 이름을 지정하는 것으로, 코드의 가독성을 높이고 반복적인 타입 정의를 줄이는 데 도움을 줍니다.

```tsx
//**type Listener**는 **Project[]** 형식의 매개변수를 받아들이고 아무 것도 반환하지 않는 함수 타입입니다.
type Listener = (items: Project[]) => void;
```



</br>


### Generic

```jsx
type Listener<T> = (items: T[]) => void;
```

`<T>`는 TypeScript에서 제네릭(Generic) 타입을 나타냅니다.

주어진 코드에서 `<T>`는 제네릭 타입 매개변수로 사용되며, 이는 **사용자가 지정한 타입**을 나타냅니다.

제네릭 타입 `T`는 실제 사용자가 타입을 정의할 때 구체적인 타입으로 대체되며, 이를 통해 타입 안정성과 재사용성을 보장할 수 있습니다. `T`와 `U`는 일반적으로 제네릭 타입 변수로 사용되는 식별자입니다.

제네릭을 사용하기 시작하면, 제네릭 함수를 만들 때, 컴파일러가 함수 본문에 제네릭 타입화된 매개변수를 쓰도록 강요합니다. 즉, 이 매개변수들은 실제로 `any` 나 모든 타입이 될 수 있는 것처럼 취급할 수 있게 됩니다.

</br>

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