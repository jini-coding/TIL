### Initializer (생성자)

- convenience의 뜻이 뭔가요? convenience init에 대해 설명해주세요.
    - convenience는 편의성, 편리함을 의미한다.
    - convenience init은 보조 이니셜라이저로, 클래스 내의 init을 도와주는 역할을 한다.
    - convenience init은 init을 호출하여 인스턴스를 초기화하고 반드시 **같은 클래스 내의 다른 이니셜라이저를 호출해야 한다.**
    - 코드 재사용성을 높이고 초기화 과정을 단순화하는데 유용하다.
    
    ```swift
    class Person {
        var name: String
        var age: Int
        
        // Designated Initializer
        init(name: String, age: Int) {
            self.name = name
            self.age = age
        }
        
        // Convenience Initializer
        convenience init(name: String) {
            self.init(name: name, age: 15)
        }
    }
    ```
    
- Designated Initializer(지정 이니셜라이져)는 무엇인가요?
    - Designated Initializer는 주 이니셜라이저로, 클래스나 구조체의 모든 프로퍼티를 초기화하는 역할을 한다.
    - 클래스에서 최소 하나의 Designated Initializer가 필요하며 초기화할 때 모든 프로퍼티를 초기화해야하고 **상위 클래스의 Designated Initializer를 호출해야 한다**.
    
    ```swift
    class Person {
        var age: Int
        
        // Designated Initializer
        init(age: Int) {
            self.age = age
        }
    }
    ```
    
- init(이니셜라이징)의 종류에 대해 얘기해주세요.
    - Designated Initializer
        - 클래스나 구조체의 모든 저장 속성을 초기화하며 상위 클래스의 Designated Initializer를 호출해야 한다.
    - Convenience Initializer
        - 주 생성자인 Designated Initializer를 호출하여 초기화를 위임한다.
        - 초기화 과정을 간소화하거나 기본값을 설정할 때 유용하다.
    - Required Initializer
        - 상속할 때 서브 클래스에서 반드시 재정의해야하는 이니셜라이저이다.
        - 앞에 required init 키워드를 사용하여 선언한다.
    - Failable Initializer
        - 초기화에 실패할 가능성이 있을 경우 사용된다.
        - init?으로 선언하며 실패하면 nil을 반환한다.
        - Failable Initializer로 만들어진 인스턴스는 반드시 옵셔널 타입으로 정의되어야 한다.
        
- 멤버와이즈(memberwise) 이니셜라이저가 뭔가요?
    - 멤버와이즈 이니셜라이저는 구조체에서만 기본적으로 제공되는 초기화 메서드이다.
    - 구조체는 Designated Initializer를 구현하지 않았을 때, 모든 프로퍼티를 파라미터로 가진 생성자를 자동으로 생성하여 이니셜라이저를 제공해준다.
    - 즉, 명시적으로 Designated Initializer를 적지 않고도 편하게 이니셜라이저를 사용할 수 있다.
    
    ```swift
    struct Person {
        var name: String
        var age: Int
    }
    
    let passerby = Person(name: "riel", age: 25)
    ```
