## HashMap과 ConcurrentHashMap의 차이점

### Thread Safe
- 주요 차이점은 ConcurrentHashMap는 내부적 동기화 때문에 스레드가 Safe합니다. 
- HashMap는 내부적으로 동기화되지 않고 스레드로부터 안전하지 않습니다. HashMap 메서드를 사용하여 외부에서 동기화 할 수 있습니다.


###  Internal Structure(내부구조)
- ncurrentHashMap의 모든 작업이 동기화되는 것은 아닙니다. 추가 및 삭제와 같은 수정 작업만 동기화됩니다. 
- 읽기 작업은 동기화되지 않습니다. 이렇게 하면 ConcurrentHashMap이 외부에서 동기화된 HashMap보다 동시 다중 스레드 응용 프로그램에 대한 첫 번째 선택 맵이 됩니다.

### Null Keys And Null Values
- HashMap은 최대 하나의 null 키와 임의의 수의 null 값을 허용합니다.
- ConcurrentHashMap은 null 키와 null 값도 허용하지 않습니다.

### Performance(성능)

- ConcurrentHashMap에 대한 수정 작업만 동기화됩니다. 따라서 ConcurrentHashMap에 대한 추가 또는 제거 작업은 HashMap보다 느립니다. 
- ConcurrentHashMap 및 HashMap 모두에 대한 읽기 작업은 두 맵의 읽기 작업이 동일한 성능을 제공합니다


출처: https://applepick.tistory.com/124 [애픽’s 기록공간:티스토리]
