## **Class**

- class의 성능을 향상 시킬수 있는 방법들을 나열해보시오.
    1. static dispatch를 통해 성능을 향상시킬 수 있다.
        1. final 키워드를 붙여 상속 및 오버라이딩을 금지하여 static dispatch를 통해 동작한다.
        2. Static Dispatch
            - 호출할 메서드를 컴파일 타임에 결정하는 방식
            - 런타임 때 호출할 매서드를 이미 결정해두었기 때문에 성능이 빠름
    2. 파일 내에서만 접근해도 될 경우에는 private 키워드를 붙인다.
        1. 외부 접근을 제한하면 컴파일러가 최적화를 더 잘 수행할 수 있다.
- instance 메서드와 class(타입)메서드의 차이점을 설명해보세요.
    - instance 메서드
        - func으로 시작하는 메서드
        - 클래스의 인스턴스를 생성하고 생성된 인스턴스를 통해서 호출된다.
        
        ```swift
        class Example {
            func instanceMethod() {
                print("인스턴스 메서드")
            }
        }
        
        let example = Example() // 인스턴스 생성
        example.instanceMethod() // 인스턴스 메서드 호출
        ```
        
    - class(타입) 메서드
        - func 앞에 static 또는 class가 붙으면 타입 메서드
        - 인스턴스를 만들지 않고 클래스 등의 타입으로부터 바로 호출할 수 있다.
        
        ```swift
        class Example {
            static func staticTypeMethod() {
                print("static 타입 메서드")
            }
            
            class func classTypeMethod() {
                print("class 타입 메서드")
            }
        }
        
        Example.classTypeMethod() // 클래스 타입 메서드 호출
        ```
        
- 타입메서드 중에서, class 메서드와 static 메서드의 차이점을 설명해보세요.
    - class 메서드
        - class 키워드로 선언한다.
        - 메서드 오버라이딩 가능
        - 상속이 불가능한 struct/enum에서 사용 불가
    - static 메서드
        - static 키워드로 선언한다.
        - 메서드 오버라이딩 불가능
- Pointer라고 들어봤는지?
    - 포인터는 메모리 주소를 가리키는 변수를 말한다.
    - class의 참조타입 특성과 힙 메모리 할당 동작은 포인터 기반으로 구현되어있다.
        - 클래스 인스턴스는 참조타입으로, 변수나 상수에 저장되는 건 객체의 메모리 주소(포인터)이다.
        - 클래스 인스턴스는 힙 메모리에 할당되는데, 힙은 동적으로 메모리가 관리되는 영역으로, 포인터를 통해 접근한다.
    - swift는 안전성을 중시하는 언어로 기본적으로 안전한 메모리 구조를 갖고 있다. 직접 포인터를 사용해서 메모리에 접근하는 것은 권장되지 않지만 아래와 같은 경우 사용해볼 수 있다.
        - C나 Objective-C와 상호 운용할 때 사용한다.
        - 직접 메모리를 관리할 필요가 있는 경우 등 성능 최적화가 필요한 저수준 작업을 할 때 사용한다.
    - Swift의 UnsafePointer, UnsafeMutablePointer, UnsafeRawPointer, UnsafeBufferPointer 등을 통해 사용할 수 있다.
        - UnsafePointer<T> : 읽기 전용 포인터로, 포인터가 가리키는 데이터는 변경 불가능하다.
        - UnsafeMutablePointer<T>: 읽기와 쓰기가 가능한 포인터로, 데이터를 직접 수정 가능하다.
        - UnsafeRawPointer : 타입 정보가 없는 포인터로, 메모리를 바이트 단위로 접근할 때 사용된다. 데이터를 특정 타입으로 변환하려면 타입 캐스팅이 필요하다.
        - UnsafeMutableRawPointer: 위와 비슷하지만 데이터를 수정할 수 있다.
        - UnsafeBufferPointer<T> : 배열처럼 연속된 메모리 블록을 다룰 수 있도록 하는 포인터이다.
    
    ```swift
    //UnsafePointer
    var value = 10
    let pointer: UnsafePointer<Int> = UnsafePointer(&value)
    print(pointer.pointee)  // 출력: 10
    
    //UnsafeMutablePointer
    var value = 10
    let mutablePointer = UnsafeMutablePointer(&value)
    mutablePointer.pointee = 20
    print(value)  // 출력: 20
    
    //UnsafeRawPointer
    var value: UInt32 = 42
    let rawPointer = UnsafeRawPointer(&value)
    let rawValue = rawPointer.load(as: UInt32.self)
    print(rawValue)  // 출력: 42
    
    //UnsafeMutableRawPointer
    var value: UInt32 = 42
    let mutableRawPointer = UnsafeMutableRawPointer(&value)
    mutableRawPointer.storeBytes(of: 99, as: UInt32.self)
    print(value)  // 출력: 99
    
    //UnsafeBufferPointer
    var array = [1, 2, 3, 4]
    array.withUnsafeBufferPointer { buffer in
        for value in buffer {
            print(value)
        }
    }
    ```
    
- lazy 속성이 뭔지? lazy를 마구잡이로 사용할 때 주의할 점이 뭐가 있을까요?
    - lazy(지연 저장) 속성이란
        - var와만 사용할 수 있다. (let과 사용 불가)
            - let은 초기화가 끝나기 전에 무조건 값을 갖고 있어서 사용 불가
        - lazy 키워드를 사용하면 프로퍼티를 실제로 사용할 때 초기화하도록 할 수 있어 메모리를 효율적으로 사용할 수 있다. (불필요한 할당과 실행 방지)
        - 초기화 비용이 큰 프로퍼티나 자주 사용하지 않는 프로퍼티가 있으면 사용하기에 유용하다.
    - 주의할 점
        1. lazy 프로퍼티는 멀티스레드 환경에서 한번만 실행되는걸 보장할 수 없고 중복 호출될 수 있으므로, 스레드 안전성이 떨어진다. 안전성을 보장하려면 추가 동기화가 필요하다.
        2. 실제 프로퍼티를 사용할 때 연산이 수행되기 때문에 마구잡이로 사용하면 속도저하가 일어날 수 있다.
