# TIL

* 개발관련 기록사항 정리
* [Markdown](https://guides.github.com/features/mastering-markdown/)
 으로 정리




JVM (Java Virtual Machine)

자바 가상 머신의 약자를 땄음.

1. 가상머신 : 프로그램을 실행하기 위해 물리적 머신과 유사한 머신을 소프트웨어로 구현한 것
2. 역할
    - 자바 애플리케이션을 클래스 로더를 통해 읽어들여, 자바 API 와 함께 실행하는 것
    - JAVA 와 OS 사이의 중재자 역할을 해, JAVA 가 OS 에 구애받지 않고 재사용을 가능하게 함
    - 메모리 관리인 Garbage collection 을 수행함
    - 스택기반의 가상머신 (ARM 아키텍쳐 같은 하드웨어는 레지스터 기반으로 동작)
3. 왜 알아야 할까?

    한정된 메모리를 효율적으로 사용하여 최고의 성능을 내기 위해서

    메모리 효율성을 위해 메모리 구조를 알아야함

    메모리 관리에 따라 성능이 좌우됨

    메모리 관리가 되지 않으면, 속도저하, 프로그램 종료 현상이 일어날 수 있음

4. 자바프로그램 실행과정
    1. 프로그램이 실행되면 JVM은 OS로 부터 이 프로그램이 필요로 하는 메모리를 할당 받음

        JVM 은 이 메모리 용도에 따라 여러 영역으로 나누어 메모리를 관리함

    2. 자바 컴파일러(javac)가 자바코드(.java)를 읽어들여 자바 바이트코드(.class)로 변환
    3. Class loader 를 통해 class 파일을 JVM 으로 로딩
    4. 해석된 바이트 코드는 Runtime Data Areas 에 배치되어 실질적이 수행이 이루어짐

        이러한 실행과정 속에서 JVM 은 필요에 따라 Thread Synchronization과 GC 같은 역할을 수행

[https://jamcode.tistory.com/66](https://jamcode.tistory.com/66)
