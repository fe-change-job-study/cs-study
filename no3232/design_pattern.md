# Design Pattern

## 목차

- [`디자인 패턴`](#디자인-패턴)

  - 디자인 패턴이란 무엇인가요?

- [`바닐라 디자인 패턴`](#바닐라-디자인-패턴)
  - Command Pattern
  - Factory Pattern
  - Flyweight Pattern
  - Mediator/Middleware Pattern
  - Mixin Pattern
  - Module Pattern
  - Observer Pattern
  - Prototype Pattern
  - Provider Pattern
  - Proxy Pattern
  - Singleton Pattern
- [`리액트 디자인 패턴`](#리액트-디자인-패턴)
  - Compound Pattern
  - HOC Pattern
  - Hooks Pattern
  - Container/Presentational Pattern
  - Render Props Pattern

<br/>

## 디자인 패턴

### 디자인 패턴이란 무엇인가요?

디자인 패턴은 소프트웨어를 개발하는 과정의 반복되는 일반적인 문제들에 대해 기준이 되는 해결책을 제공하는 중요한 개념이다.
디자인 패턴은 소프트웨어의 특정 구현을 직접 제공하지는 않지만, 반복되는 문제 상황들을 최적화된 방법으로 해결하도록 돕는 컨셉들이다.

<br/>

## 바닐라 디자인 패턴

### Command Pattern

커맨드 패턴을 사용하면 특정 작업을 실행하는 개체와 메서드를 호출하는 개체를 분리할 수 있다.

온라인 음식 배달 플랫폼을 개발한다고 가정해보자. 사용자는 주문하거나, 주문한 음식이 어디쯤 왔는지 확인하거나, 주문을 취소할 수 있다.

```js
class OrderManager {
  constructor() {
    this.orders = [];
  }

  placeOrder(order, id) {
    this.orders.push(order);
    return `You have successfully ordered ${order} (${id})`;
  }

  trackOrder(id) {
    return `Your order ${id} will arrive in 20 minutes.`;
  }

  cancelOrder(id) {
    this.orders = this.orders.filter((order) => order.id !== id);
    return `The order ${id} has been cancelled`;
  }
}
```

`OrderManager` 클래스에서 `placeOrder`, `trackOrder`, `cancelOrder` 를 구현하였고, 이 메서드들을 직접 사용하는 것도 가능하다.

```js
const manager = new OrderManager();

manager.placeOrder("Pad Thai", "1234");
manager.trackOrder("1234");
manager.cancelOrder("1234");
```

하지만 이렇게 `manager`의 메서드를 사용하는 도중, 나중에 특정 메서드의 이름을 변경하거나 메서드의 기능을 변경해야하는 경우가 생길 수 있다.

`placeOrder`대신에 이름을 `addOrder`로 변경하면 전체 코드베이스에서 해당 메서드를 호출하지 않도록 코드를 수정해야한다. 앱의 규모가 크면 까다로운 작업이 될 것이다.

이렇게 하는 대신, `manager` 객체로 부터 메서드를 분리하고 각각의 명령을 처리하는 함수를 만들 것이다.

먼저 `OrderManager` 클레스에서 `execute`라는 하나의 메서드만 가지도록 한다. 이 메서드는 인자로 주어진 어떤 명령이든 실행할 수 있다.

각 명령은 첫번째 인자로 `OrderManager`의 `orders`배열을 넘겨 접근할 수 있도록 한다.

```js
class OrderManager {
  constructor() {
    this.orders = [];
  }

  execute(command, ...args) {
    return command.execute(this.orders, ...args);
  }
}
```

아래에서 3개의 `Command` 를 만든다.

```js
class Command {
  constructor(execute) {
    this.execute = execute;
  }
}

function PlaceOrderCommand(order, id) {
  return new Command((orders) => {
    orders.push(id);
    return `You have successfully ordered ${order} (${id})`;
  });
}

function CancelOrderCommand(id) {
  return new Command((orders) => {
    orders = orders.filter((order) => order.id !== id);
    return `The order ${id} has been cancelled`;
  });
}

function TrackOrderCommand(id) {
  return new Command(() => `Your order ${id} will arrive in 20 minutes.`);
}
```

최종적으로 동작하게 만드느 코드는 다음과 같다.

```js
class OrderManager {
  constructor() {
    this.orders = [];
  }

  execute(command, ...args) {
    return command.execute(this.orders, ...args);
  }
}

class Command {
  constructor(execute) {
    this.execute = execute;
  }
}

function PlaceOrderCommand(order, id) {
  return new Command((orders) => {
    orders.push(id);
    console.log(`You have successfully ordered ${order} (${id})`);
  });
}

function CancelOrderCommand(id) {
  return new Command((orders) => {
    orders = orders.filter((order) => order.id !== id);
    console.log(`You have canceled your order ${id}`);
  });
}

function TrackOrderCommand(id) {
  return new Command(() =>
    console.log(`Your order ${id} will arrive in 20 minutes.`)
  );
}

const manager = new OrderManager();

manager.execute(PlaceOrderCommand("Pad Thai", "1234"));
manager.execute(TrackOrderCommand("1234"));
manager.execute(CancelOrderCommand("1234"));
```

#### 개인적인 평

패턴 자체는 클래스에 종속되지않은 순수함수를 사용하는, 그리고 함수를 일급객체형식으로 사용하고 있는 함수형 프로그래밍을 충실히 따르는 패턴이라고 생각한다.

다만 함수형 프로그래밍과 맞지 않는 부분은 orders를 this로 지속적으로 참조하고 있다는 점.
굳이 기존의 배열(orders)를 사용하는게 아니라 새로운 배열을 새로 생성해서 return 하는 것이 더 함수형 프로그래밍에 가깝다는 생각.

아래는 AI가 작성한 함수형 프로그래밍 형식의 개선판 코드다.

```js
class OrderManager {
  constructor() {
    this.orders = [];
  }

  // 함수를 인자로 받는 일급 객체 형식
  execute(command, ...args) {
    const result = command.execute(this.orders, ...args);
    // 기존의 값을 수정하는 대신 새로 리턴한 값으로 대체
    this.orders = result.newState;
    return result;
  }
}

// orders 배열을 수정하는 대신 새로운 배열을 리턴
// state 와 event 를 리턴하는 형식
// 부수 효과는 Event 객체에 담아 외부로 분리
function PlaceOrderCommand(order, id) {
  return new Command((orders) => ({
    newState: [...orders, id],
    event: {
      type: "ORDER_PLACED",
      payload: { order, id },
    },
  }));
}

// 사용
const manager = new OrderManager();
const result = manager.execute(PlaceOrderCommand("Pad Thai", "1234"));
console.log(result.event); // 부수 효과를 외부로 분리
```

<br/>
