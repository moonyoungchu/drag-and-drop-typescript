# Typescript

---

2시간 40분짜리 강의를 통해 typescript를 터득해보자💪

---

- 실행 명령

```jsx
npm start

tsc -w
```

<br/>

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

    @autobind
    private submitHandler(event: Event) {
        event.preventDefault();
        ...
    }
}
```

위의 코드에서 `@autobind`는 데코레이터(decorator)로 사용되고 있습니다. 데코레이터는 클래스, 메서드, 속성 등에 추가적인 기능을 부여하는 데 사용됩니다. `@autobind` 데코레이터는 해당 메서드가 호출될 때 자동으로 바인딩(bind)되도록 도와줍니다.

`@autobind` 데코레이터는 클래스의 메서드에 적용됩니다. 주어진 코드에서 `@autobind`가 `submitHandler` 메서드 위에 적용되어 있기 때문에 `submitHandler` 메서드에 대해 자동 바인딩이 수행됩니다.

`autobind` 함수는 세 개의 매개변수를 받습니다. 첫 번째 매개변수인 `_`는 사용되지 않으며, 두 번째 매개변수인 `_2`는 메서드의 이름을 나타냅니다. 세 번째 매개변수인 `descriptor`는 메서드의 속성을 나타내는 객체입니다.

`autobind` 함수의 내부에서는 원래의 메서드를 `originalMethod` 변수에 저장하고, 이후에 반환될 수정된 속성(descriptor) 객체를 생성합니다. 수정된 속성 객체(`adjDescriptor`)는 다음과 같은 속성을 갖습니다:

- `configurable: true`: 속성(descriptor)의 설정 가능 여부를 나타냅니다.
- `get()`: 접근자 함수로, 메서드가 호출될 때 원래 메서드가 현재 인스턴스(this)에 바인딩된 상태로 실행되도록 합니다. 이를 위해 `originalMethod`를 `this`에 바인딩한 함수를 생성하여 반환합니다.

따라서, `@autobind` 데코레이터를 사용하면 `submitHandler` 메서드가 항상 현재 인스턴스에 바인딩된 채로 호출되게 됩니다. 이는 주로 이벤트 핸들러와 같이 메서드가 다른 문맥(context)에서 호출될 때, 원본 메서드와 바인딩을 유지하고자 할 때 유용합니다.

<br/><br/>

### private method

TypeScript에서 **`private`** 키워드는 클래스 멤버인 메서드나 속성을 선언할 때 사용됩니다. **`private`**로 선언된 멤버는 해당 클래스 내에서만 접근할 수 있으며, 클래스 외부에서는 접근할 수 없습니다.

```tsx
class ProjectInput {
    templateElement: HTMLTemplateElement;
    descriptionInputElement: HTMLDivElement;

    constructor() {
        this.titleInputElement = document.getElementById('project-input')! as HTMLTemplateElement;
        this.descriptionInputElement = document.getElementById('app')! as HTMLDivElement;

    }

    private clearInputs() {
        this.titleInputElement.value = '';
        this.descriptionInputElement.value = '';
    }

		...

}
```

<br/><br/>

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

**`interface`**는 객체의 구조를 정의하기 위해 사용되는 개념입니다. 인터페이스는 속성, 메서드, 인덱서(indexer) 등으로 구성될 수 있으며, 이를 통해 개발자가 코드의 일관성과 타입 안정성을 유지할 수 있습니다. 인터페이스는 클래스, 객체, 함수 등 다양한 구조에 적용될 수 있습니다.

인터페이스는 타입 체크의 역할을 수행하며, 특정 타입이 인터페이스의 요구사항을 충족시키는지를 검사할 수 있습니다. 이를 통해 컴파일러가 코드를 분석하고 타입 에러를 포착하거나 자동 완성 기능 등을 제공할 수 있습니다.

<br/><br/>

### ? (옵셔널(optional) 속성)
**`?`** 기호는 TypeScript에서 옵셔널(optional) 속성을 나타냅니다. 인터페이스 또는 타입에서 속성 뒤에 **`?`**를 붙이면 해당 속성은 선택적으로 사용할 수 있음을 의미합니다. **옵셔널 속성은 해당 속성의 값이 있을 수도 있고 없을 수도 있다는 것을 나타냅니다.** 즉, 해당 속성을 사용하는 코드에서 값이 제공되지 않으면 기본값이나 초기화되지 않은 값으로 처리될 수 있습니다.

<br/><br/>

### ! (non-null assertion operator)
```tsx
const listEl = document.getElementById("test")! as HTMLUListElement;
```

**`!`**는 non-null assertion operator(비-널 어설션 연산자)라고 불리며, 타입스크립트에서 변수가 null 또는 undefined가 될 수 없음을 명시적으로 나타냅니다. 

즉, **`getElementById()`**의 결과가 null일 가능성을 제거하고, **`HTMLUListElement`** 타입으로 단언한다는 의미입니다.


<br/><br/>

### enum

Enum은 특정 값들의 집합을 나타냅니다.

```tsx
//프로젝트의 상태를 "Active"와 "Finished"로 나타내기 위해 다음과 같이 Enum을 사용할 수 있습니다
enum ProjectStatus{
    Active,
    Finished
}
```

<br/><br/>

### type

새로운 타입을 정의하기 위해 사용됩니다. `type`을 사용하여 타입 별칭(Type Alias)을 생성하거나, 유니온 타입(Union Type), 인터섹션 타입(Intersection Type), 제네릭 타입(Generic Type) 등을 정의할 수 있습니다.

타입 별칭(Type Alias)은 기존 타입에 대해 새로운 이름을 지정하는 것으로, 코드의 가독성을 높이고 반복적인 타입 정의를 줄이는 데 도움을 줍니다.

```tsx
//**type Listener**는 **Project[]** 형식의 매개변수를 받아들이고 아무 것도 반환하지 않는 함수 타입입니다.
type Listener = (items: Project[]) => void;
```