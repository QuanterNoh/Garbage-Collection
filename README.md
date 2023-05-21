## GC(Garbage-Collection)
프로세스 실행하거나 객체를 생성시 힙, 스택 영역에 메모리를 할당하고, 해당 프로세스가 종료되었거나 생성된 객체가 더이상 사용되지 않을 때 할당된 메모리를 해제하는 동작을 자동적으로 수행하는 메모리 관리 기능입니다.

## GC 가 필요한 이유
1. 메모리 누수(memory leark) 방지
    - 사용된 메모리가 해제되지 않을 경우 메모리 부족, 메모리 사용률 증가, 메모리 조각화 등과 같이 시스템 성능 저하 및 안정성 문제 등을 일으킬 수 있는데, GC가 자동적으로 메모리 자원 해체를 수행함으로써 메모리 누수를 방지합니다.

2. 프로그래머의 부담 완화
    - C언어의 경우 프로그래머가 직접 malloc 함수로 메모리를 할당하고 free 함수를 통해 메모리를 해제해야 하지만, GC가 메모리의 할당 및 해체를 자동으로 처리함으로써 프로그래머의 메모리에 대한 직접적인 관리를 감소시켜준다.

## Python 에서 GC 가 동작되는 방식
Python에서 GC는 참조 횟수 확인 방식과 세대별 가비지 컬렉션의 2 가지 방식으로 동작합니다.

1. 참조 횟수 확인(Reference counting)
    - 특정 객체를 변수에 할당하거나 함수의 인수로 전달할때, list 혹은 class 에 속성으로 추가하는 등 data structure에 추가할 때 참조 횟수가 증가하게 되는데, 이후 특정 객체의 참조 횟수가 0이 되었을 때 GC가 자동적으로 객체의 메모리 할당을 해제합니다.

2. 세대별 가비지 컬렉션(Generational Garbage Collection)
    - Python의 GC는 세대(generation)와 임계값(threshold)에 따라 GC 주기와 객체를 관리합니다. 
    - 0 ~ 2 세대로 구분되며 최근에 생성된 객체일 수록 0세대로 오래된 객체일 수록 2세대로 이동합니다. 
    - 각 세대에는 객체 할당 임계값이 있고, 특정 세대의 객체 할당 횟수가 임계값을 초과할 경우 GC가 동작합니다. 
    - 어린 객체가 오래된 객체보다 해제될 가능성이 높다는 가설(generational hypothesis)에 근거하여 세대가 낮을 수록 보다 자주 GC 를 수행합니다.
