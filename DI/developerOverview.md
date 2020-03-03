DI 는 프로그래밍에서 범용적으로 많이 사용되며, 안드로이드 개발에 적합.

DI 의 이론을 따르면 좋은 앱 구조를 취할 수 있음.

DI 의 장점

1. 코드의 재사용성
2. 리팩토링 용이
3. 테스트 용이

DI란?

클래스는 종종 다른 클래스를 참조한다. 예를들면 Car 클래스는 Engine 클래스가 필요할 수 있다. 이러한 필수 클래스를 종속성이라고 하며 예제에서 Car 클래스는 Engine 클래스의 인스턴스를 실행하는데 의존합니다.

클래스가 필요한 객체를 얻기 위한 방법이 세가지 있습니다.

1. 클래스는 필요한 종속성을 구성합니다. 예를들어 위와 같이, Car 는 Engine 의 인스턴스를 생성하고 초기화합니다.
2. 다른 곳에 가져 가십시오. Context 의 getter, getSystemService() 와 같은 안드로이드 API 들은 이 방식이다.
3. 매개변수로 제공하세요. 앱은 클래스가 구성될 때 이러한 종속성을 제공하거나 각 종속성이 필요한 함수에 전달할 수 있습니다. Car 생성자는 Engine 을 매개변수로 받습니다. 

이 세가지 방식을 통해 클래스의 의존성을 가질 수 있으며 클래스의 인스턴스를 가지는게 아니라 그들 자신이  클래스를 변수로 받을 수 있습니다.

@Module - 클래스에만

@Provide - @Module 클래스 안에 선언된 메소드에만

Module 클래스는 의존성 주입에 필요한 객체들을 Provide 메소드를 통해 관리합니다.

Provide 메소드의 파라미터 또한 컴포넌트 구현체로부터 전달 받을 수 있습니다.

Module 클래스는 클래스 이름뒤에 Module 을 붙이고

Provide 메소드 명 앞에슨 provid 를 붙임

@Compnent

@Component 는 interface 또는 abstact 클래스에 붙일 수 있습니다. 컴파일 타임에 어노테이션 프로세서에 의해 생성된 ㅋ르래스는 접두어 Dagger 와 @Component 가 붙은 클래스 이름이 합쳐진 형식의 이름을 ㄱ자습니다

@Component interface MyComponent{...} 란 인터페이스가 있다면 DaggerMyComponent 라는 클래스가 생성됩니다.

당신의 앱을 위한 적정기술 선택

 위에서 증명했듯이, 당신의 앱의 의존성을 관리하기 위핸 몇몇 기술이 있습니다.

1. 수동 DI : 확장성이 낮기 때문에 상대적으로 작은 앱에 적절합니다. 앱이 커질 수록 객체를 사용하기 위해 보일러플레이트 코드가 늘어날 것 입니다.
2. Service Locater : 상대적으로 적은 보일러플레이트 코드에서 시작하겠지만 확장성이 낮습니다. 더불어 이 기술은 싱글톤에 의존하기 때문에 테스트하기가 점점 어려워질 것 입니다.
3. Dagger : 확장가능하며  복잡한 앱에 잘 맞습니다.

당신의 라이브러리를 위한 적정기술 선택

 만약 당신이 외부 SDK나 라이브러리를 개발하고 있다면 사이즈에 따라 수동 DI 와 Dagger 중에 선택해야 합니다. 만약에 DI 를 위해 써트파티 라이브러리를 사용해야 한다면, 라이브러리 사이즈가 증가할 것 입니다.

결과

DI 를 이용하면 다음과 같은 이점을 얻을 수 있습니다.

1. 클래스의 재사용성과 의존성의 해제 : 이것은 의존성의 실행을 쉽게 변경할 수 있습니다. 코드의 재사용은 조적의 역전때문에 클래들은 더이상 그들의 의존성이 어떻게 생성되는지 조절할 필요가 없습니다 그러나 다른 트성들과 함께 일해야 합니다

2. 리팩토링의 용이 : 의존성들은 API 에서 증명할 수 있으므로 객체를 생성할때 체크할 수 있거나 컴파일 단계에서 어떤것이 실행되는지 숨길필요가 없습니다.

3. 테스트의 용이 : 클래스 테스트 시, 이 클래스의 의존성을 관리할 필요가 없기 때문에 테스트할 수 있는 다른 모든 케이스들을 다르게 실행해 볼 수 있습니다.

DI 의 장점을 모두 이해하기 위해서, 당신은 수동으로 DI 를 [https://developer.android.com/training/dependency-injection/manual](https://developer.android.com/training/dependency-injection/manual) 에 따라 적용해봐야 합니다.



class Car {
    
        private Engine engine = new Engine();
    
        public void start() {
            engine.start();
        }
    }
    
    
    class MyApp {
        public static void main(String[] args) {
            Car car = new Car();
            car.start();
        }
    }

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b7ae9e90-c237-4f8f-a551-6844efbb3675/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b7ae9e90-c237-4f8f-a551-6844efbb3675/Untitled.png)

 이 예제는 DI 예제가 아닙니다 왜냐하면 Car 클래스가 자신의 Engine 을 생성합니다. 이 것은 다음과 같은 이유로 문제가 있습니다

- Car, Engine 은 서로 강력하게 묶여 있습니다. Car 인스턴스는  한 가지 유형의 Engine을 사용하므로 하위 클래스나 대체 구현을 쉽게 사용할 수 없습니다. Car 자체가 Engine 을 구성하는 경우 Gas 및 Electric 유형의 엔진에 동일한 Car 를 재사용하는 대신 두가지 유형의 Car 를 작성해야 합니다.

- Engine 타입을 사용했고 서브 클래스가 없거나 쉽게 쉽게 사용되어질 변경가능한 실행이 없습니다. 만약에 Car 가 자신의 Engine 을 생성한다면, 당신은 똑같은 car 를 단지 재사용하 는 것이 아니라 반드시 두종류의 Car 를 생성해야합니다.
- Engine 에 대한 의존성은 테스트를 더욱 어렵게 만듭니다. Car 는 실제 Engine 인스턴스를 사용하므로 "Test double" 을 사용하여 다른 테스트 사례에 대한 엔진을 수정할 수 없습니다.
- Engine 에 대한 강한 종속성은 테스트하기 어렵게 만듭니다. Car 가 실제 Engine 의 인스턴스를 사용하고 이러면

    class Car {
    
        private final Engine engine;
    
        public Car(Engine engine) {
            this.engine = engine;
        }
    
        public void start() {
            engine.start();
        }
    }
    
    
    class MyApp {
        public static void main(String[] args) {
            Engine engine = new Engine();
            Car car = new Car(engine);
            car.start();
        }
    }

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e2603694-f1ed-4ed5-9efd-b11c3701b5aa/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e2603694-f1ed-4ed5-9efd-b11c3701b5aa/Untitled.png)

메인 함수가 Car 를 사용합니다. 왜냐하면 Car 는 Engine 에 의존하고 앱이 Engine 인스턴스를 생성하고나서 이것을 Car 의 인스턴스를 생성하기위해 사용합니다. DI 관점에서 바라본 이것의 장점은

- Car 재사용성 : 당신은 다른 엔진의 실행을 car 에 이용할 수 있습니다. 예를들어 당신이 Engine 의 새로운 하위클래스를 정의한다면 당신이 원하는 ElectricEngine 을 Car 에 사용할 수 있습니다. 당신이 DI 를 이용한다면, 오직 필요한 것은 다른 변경없이 변경된 하위 클래스인 ElectricEngine 의 인스턴스를 Car 에 넣어주면 됩니다.
- 테스트 용이성 : 당신은 다른 시나리오들을 더블 테스트를 이용해 테스트 할 수 있습니다. 예를들어 엔진의 테스트 더블을 만들었다면 Engine을 FakeEngine 으로 다르게 테스트할 수 있습니다.

안드로이드에서 DI 를 이용하는 주요한 방식은 두가지가 있습니다.

1. 생성자 주입 : 위에 말한 것이 생성자 주입입니다. 클래스의 의존성을 생성자에 넣습니다.
2. 필드 주입 : 액티비티나 프래그먼트 같은 특정 안드로이드 프레임워크 클래스는 시스템에 의해서 초기화 되기 때문에 생성자 주입이 불가능합니다. 그래서 필드 인젝선을 이용해서 클래스가 생성된 이후에 의존성을 초기화해줍니다. 

    class Car {
    
        private Engine engine;
    
        public void setEngine(Engine engine) {
            this.engine = engine;
        }
    
        public void start() {
            engine.start();
        }
    }
    
    class MyApp {
        public static void main(String[] args) {
            Car car = new Car();
            car.setEngine(new Engine());
            car.start();
        }
    }

자동 DI

이전 예제에소는 다른 클래스의 의존성을 라이브러리 없이 직접 생성하고, 제공하고 관리했다. 이것을 수동 DI 라고 한다. Car 예제에서는 종속성이 하나만 있었지만 종속성과 클래스가 늘어날수록 종속성을 수동으로 주입하는 것이 지루할 수 있스빈다. 수동 DI 는 다음과 같은 문제가 있따

- 큰 앱은, 모든 종속성을 가져와 올바르게 연결하려면 많은은 보일러플레이트 코드가 필요하다. 다중 계층 구조의 경우, 최상단 계층에서 객체를 생성하기 위해 모든 하위 레이어에 의존성을 제공해야한다. 실제 예제로 들어보면, 실제 카를 만들기 위해 엔진, 트랜스미션, 샤시 등 다른 것들이 필요하다. 그리고 엔진은 실린더와 스파크 플러그가 필요하다.
- 만약에 생성자에서 의존성을 주입할 수 없다면 예를들어 지여뇐 초기화를 한다면 의존성 그래프를 봐야한다

라이브러리는 생성시 자동으로 의존성을 제공해서 이러한 문제를 해결한다. 두가지 범주가 있는데

- 런타임에 생성
- 컴파일 타임에 생성

Daggera 는 구글에서 관린하며 Java, Kotlin 그리고 안드로이드에 쓰이는 유명한 DI 라이브러리이다. Dagger는 의존성 그래프를 만들고 관리해서 앱에 쉽게 DI 를 쓸 수 있게 한다. Dagger 는 완벽하게 static 이고 컴파일 타임에 .
