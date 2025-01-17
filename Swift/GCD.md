### GCD (동시성 프로그래밍)

- 프로세스와 쓰레드의 차이가 뭔가요?
    - 프로세스는 운영체제에서 실행 중인 하나의 독립된 프로그램 단위입니다. 각 프로세스는 독립적인 메모리 공간을 할당받아 실행되는데, 프로세스 간에는 메모리나 리소스를 직접 공유할 수 없습니다.
    - 쓰레드는 프로세스 내에서 실행되는 작업의 흐름입니다. 하나의 프로세스는 여러 개의 쓰레드를 가질 수 있고, 이 쓰레드들은 메모리와 리소스를 공유합니다.
    - 즉, 프로세스는 실행 중인 하나의 프로그램이고, 쓰레드는 그 프로세스 내에서 실행되는 작업의 흐름입니다. 또한, 프로세스끼리는 자원을 직접 공유할 수 없는데, 쓰레드는 하나의 프로세스에 속한 여러개의 쓰레드일 경우 자원을 공유할 수 있습니다.
    - 쓰레드가 자원을 공유할 수 있는 이유는 힙 영역과 데이터 영역을 공유하기 때문이지만, 각 쓰레드는 자신만의 스택 영역을 가지며, 이를 통해 독립적인 작업을 수행합니다.
    
- Global DispatchQueue 의 Qos 에는 어떤 종류가 있는지, 각각 어떤 의미인지 설명하시오.
    - Qos는 Quality of Service의 약자로 작업의 중요도와 우선순위를 나타냅니다.
    - DispatchQueue에는 global이라는 타입메소드가 있는데, 파라미터로 오는 Qos에 따라 시스템이 실행할 작업의 우선 순위를 결정합니다. 이 메소드는 파라미터로 받은 Qos에 따라 작업을 실행할 Queue를 반환하고, 반환된 Queue에 제출된 작업들은 동시에 스케줄됩니다.
    - 종류 (맨 위에 있을수록 우선순위가 높음)
        - userInteractive : 사용자와 직접적으로 상호작용하거나 애니메이션, 앱의 UI를 업데이트하는 작업이 필요할 때 사용합니다.
        - userInitiated : 사용자가 수행하는 작업에 대해 즉각적으로 일을 처리하도록 할 때 사용합니다. 작업이 끝날 때까지 사용자는 상호작용을 할 수 없습니다. (ex. 파일을 열거나, 데이터를 로딩하거나)
        - default : 기본 Qos. 일반적으로 사용합니다.
        - utility : 사용자가 관심이 적고 오래 걸리는 작업에 사용됩니다. (ex. 데이터 다운로드, 네트워킹)
        - background : 앱이 백그라운드 상태에 있는 동안 수행하는데 사용됩니다. (ex. 데이터 미리 로딩, 백업, 동기화)
        - unspecified : Qos 정보가 없음을 알릴 때 사용합니다.
    
    https://developer.apple.com/documentation/dispatch/dispatchqueue/2300077-global
    
- NSOperationQueue 와 GCD Queue 의 차이점을 설명하시오.
    
    
    | NSOperationQueue | GCD Queue |
    | --- | --- |
    | Objective-C 기반 고수준 API | C기반 저수준 API |
    | 일시중지, 재시작, 취소 가능 | 불가능 |
    | 작업 간 우선순위 및 의존성 설정 가능 | 우선순위는 Qos로만 설정 가능 |
    | 작업 객체 재사용 가능 | 한번만 실행 가능 |
    | GCD보다 느리고 오버헤드 발생 | 오버헤드 적음 |
    | 복잡한 작업 흐름에 적합 | 간단하고 빠른 작업, 동시성 작업에 적합 |
