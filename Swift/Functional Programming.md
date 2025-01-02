### Functional Programming (함수형 프로그래밍)

- 함수형 프로그래밍이 무엇인지 설명해보세요.
    - 함수형 프로그래밍은 순수 함수와 불변성을 강조하는 프로그래밍 패러다임으로, 프로그램이 상태 변화 없이 데이터 처리를 수학적인 함수의 계산으로 하는 것을 말한다.
    - 순수 함수는 동일한 입력에 대해 항상 동일한 출력을 반환하며 부작용이 없는 것이다. 오류가 적고 안정성이 높다.
    
    ```swift
    func plus(a: Int, b: Int) -> Int {
    	return a + b
    }
    ```
    
    - 불변성은 데이터의 변경 불가능성을 의미하고, 데이터가 한번 생성되면 그 값을 변경할 수 없게 만드는 것을 의미한다.
    - 함수형 프로그래밍에서 함수를 일급 객체로 다루는데, 일급 객체는 아래의 조건을 만족한다.
        - 객체를 변수나 상수에 저장 및 할당이 가능하다.
        - 객체를 반환 값으로 사용할 수 있다.
        - 객체를 함수의 매개변수로 사용이 가능하다.
        
- 고차 함수가 무엇인지 설명해보세요.
    
    고차 함수는 다른 함수를 파라미터로 받거나, 함수를 반환하는 함수를 말한다. map, filter, reduce, compactMap, flatMap 등이 있다.
    
- Swift Standard Library의 map, filter, reduce, compactMap, flatMap에 대하여 설명해보세요.
    - map
        - 배열이나 컬렉션의 각 요소에 주어진 함수를 적용하여 새로운 배열을 생성한다. 단, 원본 데이터는 변경되지 않는다.
    - filter
        - 배열이나 컬렉션의 요소 중 조건을 만족하는 요소만 반환한다. 단, 원본 데이터는 변경되지 않는다.
        
        ```swift
        let sports = ["클라이밍", "백패킹", "낚시", "러닝", "수영", "눈썰매"]
        let twoLetterSports: [String] = sports.filter { $0.count == 2 }
        
        print(twoLetterSports)
        // ["낚시", "러닝", "수영"]
        ```
        
    - reduce
        - 배열의 각 요소를 결합하여 단일 값으로 축소한다. 사용할 때 초기값을 설정해줘야 한다.
        
        ```swift
        let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
        let sum = numbers.reduce(0) { $0 + $1 }
        
        print(sum)
        // 55
        ```
        
    - compactMap
        - 배열의 각 요소를 변환한 후에 nil이 아닌 요소만 포함한 새 배열을 반환한다. 옵셔널 값이 포함된 배열에 사용할 때 유용하다.
        
        ```swift
        let stringArray = ["1", "2", "3", "four", "5"]
        let intArray = stringArray.compactMap { Int($0) }
        
        print(intArray) 
        // [1, 2, 3, 5]
        ```
        
    - flatMap
        - 중첩된 배열을 하나의 배열로 flat하게 만든다.
        
        ```swift
        let numbers = [[1], [2, 3], [4, 5, 6], [7, 8, 9, 10]]
        let flatMapped = numbers.flatMap { $0 }
        
        print(flatMapped)
        // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
        ```
        
- map이 뭔가요? 쉽게 설명해보세요.
    - map은 배열의 각 요소에 특정 연산을 적용한 후, 그 결과를 이용하여 새 배열을 만들어주는 도구이다. 즉, 변환해주는 도구라 할 수 있다.
    
    ```swift
    let fruits = ["apple", "banana", "cherry"]
    let uppercasedFruits = fruits.map { $0.uppercased() }
    
    print(uppercasedFruits) 
    // ["APPLE", "BANANA", "CHERRY"]
    ```
