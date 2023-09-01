![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c0d2f7d1-b135-41dc-aef3-a22eb5780710/Untitled.png)

---

## Process & Thread

### 01. Process를 간단히 설명해주세요

- **실행파일(program)이 memory에 적재되어 CPU를 할당받아 실행되는 것을 process라고 합니다.**
- 운영체제를 관통하는 핵심적인 단어가 바로 Process
- 운영체제가 작동하는 다양한 원리들이 process를 위해 존재함
- process를 memory 와 CPU관점으로 설명하면 좋음

### 02. Process 실행 과정

- 코드가 컴파일되면(이걸 프로그램이라 함) HDD(하드디스크)에 저장이 된다
- HDD에 있는 프로그램은 컴퓨터가 바로 읽을 수 없고 RAM메모리에 올라와있는 프로그램만 읽을 수 있음
- 그래서 HDD의 프로그램을 RAM에 적재시킴 그래야 비로소 한줄한줄 컴퓨터가 코드를 읽을 수 있음
- 즉 컴파일된 코드가 HDD에서 RAM으로 메모리적재 및 CPU할당을 받으면 그제서야 읽을 수 있는거
- 이때 메모리는 보통 RAM메모리를 칭함

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0dd5fe7e-57bb-4978-9c52-080415335870/Untitled.png)

### 03. Process 내에서도 메모리 용도에 따라 구분이 되어있다!

- 크게 4가지 `code`, `data`, `heap`, `stack` 영역으로 구분된다
- `code`: 하드디스크에서 컴파일된 코드를 저장 하는 영역
- `data`: 전역변수 저장
- `heap`:  동적메모리 할당 이루어지는 곳
- `stack`: 지역변수나 매개변수 저장
- 보통 코드 영역이 낮은 주소값 스택 영역이 높은 주소값을 가지고 있다

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d9bd6275-7df3-4697-9cae-6f96028e0c4a/Untitled.png)

### 04. 프로세스(process)란 실행중인 프로그램(program in execution)을 뜻한다

- 실행파일 형태로 존재하던 program이 memory에 적재되어 CPU에 의해 실행(연산)되는 것을 process라고 말함
- program은 단순히 명령어 리스트를 포함하는 파일

### 05. Memory에 적재한다는 것은?

- memory는 CPU가 직접 접근할 수 있는 컴퓨터 내부의 기억장치
- Program이 CPU에서 실행되려면 해당 내용이 memory에 적재된 상태여야만 한다.
- Process에 할당되는 memory공간은 Code, Data, Stack, Heap 4개 영역으로 이루어지며 각 process마다 독립적으로 할당받는다
- 실제로 메모리에 여러개의 process가 올라오는데 이때 process마다 각 영역에 해당하는 데이터를 보유한 채로 옴

| Code 영역 | 실행한 프로그램의 코드가 저장되는 메모리 영역 |
| --- | --- |
| Data 영역 | 프로그램의 전역변수와 static 변수가 저장되는 메모리 영역 |
| Heap 영역 | 개발자가 직접 공간을 할당(malloc) / 해제(free) 하는 메모리 영역 → 동적메모리할당 |
| Stack 영역 | 함수 호출 시 생성되는 지역 변수와 매개변수가 저장되는 임시 메모리 영역 |

### 06. 프로그램의 코드를 토대로 CPU가 실제로 연산을 해야지 프로그램이 실행된다고 볼 수 있다!

- 어떤 코드를 읽어야할지는 CPU 내부에 있는 PC(program counter) register에 저장되어 있다.
- PC register에는 다음에 실행될 코드(명령어, instruction)의 주소값이 저장되어 있다.
- 읽어야할 명령어   의 주소값을 PC register가 순차적으로 가리키게 되고, 해당 명령어를 읽어와서 CPU가 연산을 하게되면 그제서야 process 가 실행되는 것임

### 07. Multi Process 에 대해서 설명해주세요

- 면접에서 병렬성보다 동시성이 훨씬 중요
- Multi process란 2개 이상의 process가 동시에 실행되는 것을 의미한다.
- 이 때 동시라는 말은 `Concurrency`(동시성)과 `parallelism`(병렬성) 두 가지를 의미한다
    - `Concurrency`: CPU core가 1개일 때, 여러 process를 짧은 시간동안 번갈아가며 연산을 하는 시분할 시스템(time sharing system)으로 실행
    - `parallelism`: CPU core 가 여러 개일 때, 각각의 core가 각각의 process를 연산함으로써 process가 동시에 실행
- 병렬성을 유지한채로 각각의 코어가 동시성 작동이 가능하다

| 동시성 | 병렬성 |
| --- | --- |
| Single core | Multi core |
| 동시에 실해오디는 것처럼 보인다 | 실제로 동시에 여러작업이 처리된다  |

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/86890590-f954-4370-87af-a8b0d15700fa/Untitled.png)

### 08. Multi Process에서 process들은 CPU와 메모리를 공유한다

- memory의 경우에는 여러 process들이 각각의 memory영역을 차지하여 동시에 적재된다
- 하나의 CPU는 매순간 하나의 process만 연산이 가능하다.
- CPU의 작업시간을 여러 proccess들이 나눔으로써 사용자 입장에서 여러 프로그램이 동시에 실행되는 것처럼 보임 이러한 시스템을 시분할 시스템(time sharing system)이라고 부름

### 09. Multi Process 에서의 메모리 관리

- 여러 Process 가 동시에 memory 에 적재된 경우 서로다른 process의 영역을 침범하지 않도록 각process가 자신의 memory에만 접근하도록 운영체제가 관리해준다

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f5ab0112-3fd0-4cf2-9cb0-7cc1cfe763bb/Untitled.png)

### 10. CPU의 연산과 PC register

- CPU는 PC(Program Counter) register가 가리키고 있는 명령어를 읽어들여 연산을 진행한다
- PC register에는 다음에 실행될 명령어의 주소값이 저장되어 있다.
- multi process 시스템에서는 process1 이 진행되고 있을 때는 process1의 code영역을 PC register 가 가리키다가, process2 가 진행되면 process2의 code영역을 가리킨다.
- CPU는 PC register가 가리키는 곳에 따라 process를 변경해 가면서 명령어를 읽고 연산한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9e8643b1-a1fe-4968-97f7-1c44300b36f5/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b4ea8701-c1b2-4e0b-a138-e6150d3c4e33/Untitled.png)

### 11. Context 란 무엇인가요?

- 시분할 시스템에서는 한 process가 매우 짧은 시간동안 CPU를 점유하여 일정부분의 명령 수행 후 다른 process로 넘김 그리고 그 프로세스가 끝나면 다시 CPU를 점유하여 명령 수행
- 따라서 이전에 어디까지 명령을 수행했는지(=register에 어떤 메모리 주소값이 저장되어 있었는지) 정보 필요
- process가 현재 어떤 상태로 수행되고 있는지에 대한 총체적인 정보가 바로 context이다.
- 이러한 context정보들은 PCB(Process Control Block)에 저장된다
- (정리) Context란 process가 현재 어떤 상태로 수행되고 있는지에 대한 정보입니다. 해당정보는 PCB(Process Control Block)에 저장합니다

### 12. PCB(Process Control Block)이란 무엇인가요?

- PCB는 운영체제가 process에 대해 필요한 정보를 모아놓은 자료구조입니다.
- PCB에는 프로세스의 중요한 정보가 포함되어 있기 때문에, 일반 사용자가 접근하지 못하도록 보호된 메모리 영역 안에 저장된다
- 일부 운영체제에서는 PCB는 커널 스택에 위치한다 (커널 스택은 보호를 받으면서도 접근에 용이)
- 운영체제도 하나의 프로세스다!
- 컴퓨터 키자마자 운영체제(kernel)이 메모리에 적재됨
- (이미지 참고) 커널에 PCB1, PCB2 정보를 저장함

| 종류 | PCB에 저장되는 주요 정보 정리 |
| --- | --- |
| Process State | new, running, waiting, halted 등의 state 존재 |
| Process Number | 해당 process의 number |
| Program counter(PC) | 해당 process가 다음에 실행할 명령어의 주소를 가리킴 |
| Registers | 컴퓨터 구조에 따라 다양한 수와 유형을 가진 register 값들 |
| Memory limits | base register, limit register, page table 또는 segment table 등 |
| … |  |

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/743c8d29-08bd-4f41-a408-ea473cef504b/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c3578a8e-b0f0-449a-8671-d6da7ef95afa/Untitled.png)

### 13. Context Switch란?

- Context Switch란 한 프로세스에서 다른 프로세슷로 CPU 제어권을 넘겨주는 것을 의미한다.
- 이때 이전의 프로세스 상태를 PCB에 저장하여 보관하고 새로운 PCB를 읽어서 보관된 상태를 복구하는 작업이 이루어진다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ff8f36f2-d323-460a-a36c-ad2502afa614/Untitled.png)

### 14. Process의 state에는 어떤 것들이 있나요?

- 프로세스는 **실행(running), 준비(ready), 봉쇄(wait, sleep, blocked)** 세 가지 상태로 구분된다

| 실행 | 프로세스가 CPU를 점유하고 명령을 수행중인 상태 |
| --- | --- |
| 준비 | CPU만 할당받으면 즉시 명령을 수행할 수 있도록 준비된 상태 |
| 봉쇄 | CPU를 할당받아도 명령을 실행할 수 없는 상태 - ex 입력작업 기다리는 경우 등 |

### 15. `Multi thread`에 대해서 설명해주세요

- `thread`는 한 process내에서 실행되는 동작(기능 function)의 단위이다.
- `thread`는 process 내에서 독립적인 기능을 수행합니다. 각각 도립적이라 stack memory가 필요함
- 각 `thread`는 속해있는 process의 Stack 메모리를 제외한 나머지 memory 영역을 공유할 수 있다.
- `Multi thread`란 하나의 process가 동시에 여러개의 일을 수행할 수 있도록 해주는 것이다.
- 즉 하나의 process에서 (실행이 된 하나의 program) 여러 작업을 병렬처리하기 위해 `multi thread` 를 사용한다
- `Multi thread` 에서는 한 process 내에 여러개의 `thread` 가 있고, 각 `thread` 들은 Stack 메모리를 제외한 나머지 영역(Code, Data, Heap) 영역을 공유한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3932419b-e0a0-4695-9410-fc7c39c956f7/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/01baef12-ea0f-4546-8a8c-aef52a121a49/Untitled.png)

### 16. Stack Memory & PC Register

- `thread` 가 함수를 호출하기 위해서는 인자전달, Return Address 저장 및 함수 내 지역변수 저장 등을 위한 독립적인 stack memory 공간을 필요로 한다.
- 결과적으로 `thread`는 process로부터 Stack memory영역은 독립적으로 할당받고, Code, Data, Heap 영역은 공유하는 형태를 갖게 된다
- `Multi thread`에서는 각각의 `thread`마다 PC register를 가지고 있어야 한다. 왜냐하면 한 process 내에서도 `thread` 끼리 context switch가 일어나는데, PC register에 code address가 저장되어있어야 이어서 실행할 수 있기 때문이다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a823aecb-0b4e-45fc-b154-483902148f46/Untitled.png)

### 17. `thread`는 왜 독립적인 stack memory 영역이 필요할까요?

- Stack 영역은 함수 호출시 전달되는 인자, 함수의 Return Address, 함수 내 지역변수 등을 저장하기 위한 memory 영역이다
- `thread`가 process 내에서 **“독립적인 기능을 실행”** 한다는 것은 **“독립적으로 함수를 호출”** 한다는 것을 의미한다.
- 따라서 각 thread가 독립적인 동작을 실행하기 위해서는 각 thread 의 stack메모리 영역이 독립적이어야 한다.

### 18. `Process` 와 `thread` 를 비교설명 해볼래?

- `process`는 운영체제로부터 자원을 할당받는 작업의 단위이고 `thread`는 `process`가 할당받은 자원을 이용하는 실행 단위이다.
- `process`는 실행파일(program)이 memory에 적재되어 CPU를 할당받아 실행되는 것이다.
- `thread`는 한 process 내에서 실행되는 동작의 단위이다.
- `process`는 memory 공간에 code, data, heap, stack 영역이 있는데, `thread`는 `processs` 내에서 stack 영역을 제외한 code, data, heap 영역을 공유한다.

### 19. `Multi process`와 `Multi thread`중 무엇을 선택해야하나요?

- 두 방법은 동시에 여러작업을 수행한다는 측면에서 유사한 면이 있다. 적용할 시스템에 따라 장단점 고려하여 적합한 방식을 선택해야한다
- 메모리 구분이 필요할 때는 `multi process` 가 유리하다. 반면에 Context switching 이 자주 일어나고 데이터 공유가 빈번한 경우, 자원을 효율적으로 사용해야할 경우에는 `multi thread`를 사용하는 것이 유리하다.
- `multi thread` 는  메모리 영역(데이터, 힙)을 공유하고 있어서 `multi process` 보다 context switch가 더 빠르게 처리된다.
- 결국 어떤 작업을 한 프로세스에서 처리할지, 여러 프로세스로 나눌지에 대한 고민

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2eefb6fe-92d8-45cf-9235-bf41ffb45ef4/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3dafb9af-28d0-4797-bf7e-9beb82919bc9/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f95b5fcd-5b6b-490d-90f4-ff8bc7cc8b96/Untitled.png)

### 20. `Multi Process` 대신 `Multi thread` 로 구현할 경우 고려사항

- `Multi process` 대신 `multi thread` 로 구현할 경우, 메모리 공간과 시스템 자원 소모가 줄어든다.
- 하지만 multi thread 를 사용할 때는 thread 간 자원을 공유해서 동기화 문제가 발생할 수 있기 때문에 이를 주의해야함
- 또한 `Process` 간의 통신(IPC) 보다 `thread` 간의 통신 비용이 적기 때문에 통신으로 인한 오버헤드가 적다

|  | 메모리 사용 / CPU 시간 | Context Switching | 안정성 |
| --- | --- | --- | --- |
| multi process | 많은 메모리 공간 / CPU 시간 차지  | 느림 | 높음 |
| multi thread | 적은 메모리 공간 / CPU 시간 차지 | 빠름 | 낮음 |

### 21. 총정리해서 `Multi thread` 와 `Multi process`를 비교설명해줘

- `multi thread`는 `multi process` 보다 적은 메모리 공간을 차지하고 Context Switching 이 빠르다
- `multi process`는 `multi thread` 보다 많은 메모리 공간과 CPU 시간을 차지한다
- `multi thread` 는 동기화 문제와 하나의 `thread`  장애로 전체 `thread` 가 종료될 위험이 있다
- `multi process`는 하나의 `process` 가 죽더라도 다른 `process`에 영향을 주지 않아 안정성이 높다!

### 22. `Multi thread`가 `multi process` 보다 좋은 점은 어떤거야?

- `multi process` 를 이용하던 작업을 `multi thread`로 구현할 경우, 메모리 공간과 시스템 자원 소모가 줄어든다
- 또한 `process`를 생성하고 자원을 할당하는 등의 system call을 생략할 수 있기 때문에 자원을 효율적으로 관리할 수 있다.
- 뿐만 아니라 Context Switching 시 캐시 메모리를 초기화할 필요가 없어서 속도가 빠르다
- 데이터를 주고 받을 때는 process 간의 통신(IPC)보다 multi thread 간의 통신 비용이 적기 때문에 통신으로 인한 오버헤드가 적다

### 23. `Multi thread` 가 `Multi process` 보다 안좋은 점은 무엇인지 알려줘

- `thread` 간의 자원 공유시 동기화 문제가 발생할 수 있어서 프로그램 설계시 주의가 필요하다
- 하나의 `thread`에 문제가 생기면 `process` 내 다른 `thread`에도 문제가 생길 수 있음

### 24. `Multi process` 환경에서 `process`간에 데이터를 어떻게 주고받아?

- 원칙적으로 `process`는 독립적인 주소 공간을 갖기 때문에, 다른 `process`의 주소 공간을 참조할 수 없다.
- 하지만 경우에 따라 운영체제는 `process` 간의 자원 접근을 위한 메커니즘인 프로세스 간 통신(IPC_Inter Process Communication)을 제공한다.
- 프로세스 간 통신(IPC) 방법으로는 파이프, 파일, 소켓, 공유메모리 등을 이용한다.

### 25. IPC(Inter - Process Communication)에 대해 설명해줘

- `process`는 각자 자신만의 독립적인 주소공간을 가지지만, 다른 `process`가 이 주소공간을 참조하는 것은 허용하지 않는다. 이를 해결하고자 운영체제는 IPC 기법을 통해 `prcocess`들 간 통신을 가능하게 해준다
- `process`간 통신(IPC)에는 기본적으로 **공유메모리(shared memory)**와 **메세지 전달(message passing)** 두가지 모델이 있다.

### 26. 공유 메모리(shared memory)에 대해서 설명해주세요

- 공유메모리 방식에서는 `process`들이 주소 공간의 일부를 공유한다
- 공유한 메모리 영역에 읽기/쓰기를 통해서 통신을 수행한다.
- `process`가 공유메모리 할당을 `kernel`에 요청하면 `kernel`은 해당 `process`에 메모리 공간을 할당한다
- 공유 메모리 영역이 구축된 이후에는 모든 접근이 일반적인 메모리 접근으로 취급되기 때문에 더이상 `kernel`의 도움없이도 각 `process`들이 해당 메모리 영역에 접근할 수 잇다.
- 따라서 `kernel`의 관여 없이 데이터 통신이 가능해져 IPC 속도가 빠르다는 장점이 있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/64128e44-4d46-4b30-abc9-fa8b5fdefcb2/Untitled.png)

### 27. 메세지 전달 (message passing) 에 대해서 설명해주세요

- 메세지 전달 방법은 통상 system call 을 사용하여 구현됩니다. `kernel`을 통해 send(message)와 receive (message)라는 두 가지 연산을 제공받는다. 예를 들면 process1 이 `kernel`로 message를 보내면 `kernel`이 process2에게 message를 보내주는 방식으로 동작하다.
- 메모리 공유보다는 속도가 느리지만, 충돌을 회피할 필요가 없기 때문에 적은양의 데이터를 교환하는 데 유용하다. 또한 구현하기 쉽다는 장점도 있다.
- 대표적인 예시로는 `pipe`, `socket`, `message queue`등이 있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5a3ec894-2060-4375-8532-a2727ab8efa3/Untitled.png)

### 28. IPC의 예시를 들어주세요

- IPC는 크게 공유메모리 모델과 메세지 전달 모델로 나눌 수 있다.
- 공유메모리 모델은 주소공간의 일부를 공유하여 공유한 메모리 영역에 read/write를 통해 통신하게 되는데 예시로는 공유메모리와 POSIX가 있다.
- 메세지 전송 모델의 경우에는 `kernel`을 통해 send/receive 연산을 통해 데이터를 전송한다. 예시로는 `pipe`, `socket`, `message queue` 등이 있다.

### 29. 공유메모리와 메세지 전달 모델의 장단점을 알려주세요

- 공유 메모리 모델은 초기에 공유 메모리 할당을 제외하면 `kernel`의 관여없이 통신할 수 있기 때문에 속도가 빠른 장점이 있습니다.
- 하지만 여러 `process`가 동시에 메모리에 접근하는 문제가 발생할 수 있어서 별도의 동기화 과정이 필요하다는 단점이 있습니다.
- 메세지 전달 모델은 `kernel`을 통해서 데이터를 주고받기 때문에 통신 속도가 느리다는 단점이 있습니다.
- `kernel`에서 제어를 해주기 때문에 안전하며 `kernel`이 동기화를 제공해준다는 장점이 있습니다.

### 30. Multi process/thread 환경에서 동기화 문제를 어떻게 해결하나요?

- 동기화 문제 해결을 위해서는 `Mutex`, `Semaphore` 기법 등을 사용한다.
- `Mutex`란?
    - 1개의 스레드만이 공유 자원에 접근할 수 있도록 하여 경쟁상황(race condition)을 방지하는 기법이다.
    - 공유 자원을 점유하는 thread가 lock을 걸면, 다른 thread는 unlock 상태가 될 때까지 해당 자원에 접근할 수 없다.
- `Semaphore`란?
    - S개의 thread만이 공유 자원에 접근할 수 있도록 제어하는 동기화 방식이다
    - `Semaphore`기법에서는 정수형 변수 S(세마포) 값을 가용한 자원의 수로 초기화하고, 자원에 접근할 때는 `S--` 연산을 수행하여 세마포 값을 감소시키고 자원을 방출할 때는 `S++` 연산을 수행하여 세마포 값을 증가시킨다.

### 31. 동기화 문제란?

- `multi process/thread` 환경에서는 서로 다른 `thread`가 메모리 영역을 공유하기 때문에 여러 `thread`가 **동일한 자원에 동시에 접근하여** 엉뚱한 값을 읽거나 수정하는 문제이다.
- 동기화 문제를 해결하기 위해 임계영역을 설정하고 `mutex`와 `semaphore` 기법을 사용한다.
- 둘 이상의 `thread`가 동일한 자원에 접근하여 조작하고, 그 실행결과가 접근이 발생한 순서에 따라 달라지는 경쟁상황에 의해서 동기화 문제가 발생할 수 있습니다.
- 경쟁상황으로부터 보호하기 위해, 우리는 한 순간에 하나의 `process`/`thread`만 해당 자원에 접근하고 조작할 수 있도록 보장해야한다. 다시말해 `process` / `thread`들이 동기화되도록 할 필요가 있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/04488329-baab-4a4c-998c-1e5556f91456/Untitled.png)

### 32. 임계영역이란? (Critical section)

- 둘 이상의 `process`/`thread` 가 동시에 동일한 자원에 접근하도록 하는 프로그램 코드 부분을 의미한다.
- 중요한 특징중 하나는, 한 `process`/`thread`가 자신의 임계구역에서 수행하는 동안에는 다른 `process`/`thread`들은 그들의 임계구역에 들어갈 수 없어야 한다.
- 즉 임계영역내 코드는 원자적으로(atomically) 실행되어야한다.
- 원자적으로 실행되기 위해서는 각각의 `process`/`thread`는 자신의 임계구역으로 진입하려면 진입 허가를 요청해야한다. 이부분을 enrty section이라고 함
- 임계영역이 끝나고 나면 exit section으로 퇴출한다.
- 임계영역의 원자성을 보장하여 `process`/`thread`들이 동기화되도록 할 수 있다.
- 동기화 방법은 대표적으로 `Mutex`와 `Semaphore`가 있다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4e8d874b-f766-4d78-997c-908161dbabe3/Untitled.png)

### 33. `Mutex`란?

- 동기화 방법중 하나로 **mutual exclusion**의 축약어이다.
- 공유자원에 접근할 수 있는 `process` / `thread` 의 수를 1개로 제한한다.
- 임계영역을 보호하고, 경쟁상황을 방지하기 위해 **`mutex` lock**을 사용한다.
- 즉 `process` / `thread` 는 임계영역에 들어가기 전에 **lock**을 획득해야하고, 임계구역을 빠져나올 때 **lock**을 반환해야한다.
- `acquire()` 함수가 **lock**을 획득하고 `release()` 함수가 **lock**을 반환한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c051fa41-01bd-430a-bfcd-73cbf235ec20/Untitled.png)

```swift
**acquire() //entry section

// critical section

release() // exit section**
```

### 34. `Semaphore`란?

- 동기화 방법중 하나로 `mutex`와 가장 큰 차이점은 공유 자원에 접근할 수 있는 `process`/`thread` 의 개수가 2개 이상이 될 수 있다는 것이다
- `Semaphore` 변수 S(세마포)에 동시에 접근 가능한 `process` / `thread`의 갯수를 저장한다.
- S가 0보다 크면 임계영역으로 들어갈 수 있고, 임계영역에 들어가면 S값을 1감소시킨다.
- S값이 0이 되면 다른 `process` / `thread`는 임계영역으로 접근할 수 없다.
- 임계영역에서 작업이 끝나고 임계영역에서 exit 하면서 S값을 1 증가시킨다.
- `semaphore`값이 0,1만 가질 수 있는 경우 `binary semaphore`라고 하는데, 이는 `mutex`랑 거의 유사하게 작동한다.

![S가 2 → Critical Section에 동시에 최대 2개 스레드가 들어올 수 있다.](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fc351bb3-2618-451e-abfb-14a58750ca47/Untitled.png)

S가 2 → Critical Section에 동시에 최대 2개 스레드가 들어올 수 있다.

```swift
**wait(S) // entry section 

// critical section

signal(S) // exit section** 
```

### 35. `mutex`와 `semaphore`기법을 비교해서 설명해주세요

- `mutex`는 오직 1개의 `process`/`thread`만이 공유자원에 접근할 수 있고, `semaphore`는 세마포 변수의 값만큼의 `process`/`thread`들이 동시에 자원에 접근할 수 있다.
- `mutex`는 `binary semaphore`라고 할 수 있다.

### 36. 교착상태(Deadlock)에 대해서 간단히 설명해주세요

- 둘 이상의 `thread`가 각각 다른 `thread`가 점유하고 있는 자원을 서로 기다릴 때, 무한 대기에 빠지는 상황을 말한다.

![서로 Lock이 된 리소스 순서를 기다리다보니 무한대기열에 빠져버림](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/431e5186-712c-4be8-a199-62a68b02ebd0/Untitled.png)

서로 Lock이 된 리소스 순서를 기다리다보니 무한대기열에 빠져버림

### 37. Deadlock이 발생하는 조건을 말해주세요

- Deadlocck은 다음 4자기 조건이 동시에 성립할 때 발생한다
1. **상호배제 (mutual exclusion)**
    1. 동시에 한 thread만 자원을 점유할 수 있는 상황이어야 한다
    2. 다른 thread가 자원을 사용하려면 자원이 방출될 때까지 기다려야 한다.
2. ********************점유대기 (hold - and - wait)********************
    1. thread가 자원을 보유한 상태에서 다른 thread가 보유한 자원을 추가로 기다리는 상황이어야 한다.
3. **비선점 (no preemption)**
    1. 다른 thread가 사용중인 자원을 강제로 선점할 수 없는 상황이어야한다.
    2. 자원을 점유하고 있는 thread에 의해서만 자원이 방출된다
4. **순환대기 (circular wait)**
    1. 대기 중인 thread들이 순환 형태로 자원을 대기하고 있는 상황
    

### 38. Deadlock을 해결하는 방법에 대해 설명해주세요

- deadlock 문제를 해결하는 방법에는 **(1) 무시, (2) 예방, (3) 회피, (4) 탐지-회복** 4가지 방법이 있다.

| 기법 | 설명 | 비고 |
| --- | --- | --- |
| 무시 | deadlock 발생 확률이 낮은 시스템에서
아무런조치도 취하지 않고 deadlock을
무시하는 방법 | - 무시 기법은 시스템 성능 저하가 없다는 큰 장점이 있습니다
- 현대 시스템에서는 deadlock이 잘 발생하지 않고, 해결 비용이 크기 때문에 무시방법이 많이 사용된다. |
| 예방 | 교착 상태의 4가지 발생 조건 중 하나가
성립하지 않게 하는 방법 | - 순환 대기 조건이 성립하지 않도록 하는 것이 현실적으로
가능한 예방 기법이다
- 자원 사용의 효율성이 떨어지고 비용이 크다 |
| 회피 | thread 가 앞으로 자원을 어떻게 요청할지에 대한 정보를 통해 순환 대기 상태가 발생하지 않도록 자원을 할당하는 방법 | - 자원 할당 그래프 알고리즘, 은행원 알고리즘 등을 사용하여 자원을 할당하여 deadlock을 회피한다 |
| 탐지-회복 | 시스템 검사를 통해 deadlock 발생을 탐지하고, 이를 회복시키는 방법 | - 자원 사용의 효율성이 떨어지고 비용이 크다. |

---

## Memory

### 01.  논리적 주소(logical address)와 물리적 주소(physical address)와 주소바인딩(address binding)에 대해 간단히 설명해주세요

- process가 memory에 적재되기 위한 독자적인 주소 공간인 **논리적 주소(logical address)**가 생성됩니다. 논리적 주소는 각 process마다 독립적으로 할당되며, 0번지부터 시작됩니다.
- **물리적 주소(physical address)**는 process가 실제로 메모리에 적재되는 위치를 말한다.
- CPU가 기계어 명령을 수행하기 위해 process의 **논리적 주소가 실제 물리적 메모리의 어느 위치에 맵핑되는지 확인하는 과정을** 주소 바인딩(address binding)이라 한다.
- 흔히 생각하는 코데힙스 메모리가 논리적 주소, 이게 실제로 RAM에 올라가는 주소는 다름 이걸 물리적 주소라함, 이 두 주소 사이를 맵핑(연결)해주는게 주소바인딩

### 02. Paging 이란 무엇인가요?

- paging이란 process가 할당받은 메모리 공간을 일정한 page 단위로 나누어, 물리 메모리에서 연속되지 않는 서로 다른 위치에 저장하는 메모리 관리기법이다.
- paging 기법에서는 물리적 메모리를 page와 같은 크기의 frame으로 미리 나누어둔다
- 이렇게 page단위로 메모리 적재가 이루어져 저장해둘 공간을 미리 분할해두면 빠르게 메모리 할당이 가능해진다(다른 프로세스끼리 섞여보여도 페이지 별로 구분해놓아서 찾기 쉬움)
- paging 기법에서는 주소 바인딩(address binding)을 위해 모든 프로세스가 각각의 주소 변환을 위한 page table을 갖는다.
- page 기법에서는 하나의 프로세스 내에서도 페이지 단위로 다른 물리적 메모리에 저장되기 때문에 주소 바인딩을 위해서는 별도의 page table이 필요하다(해시밸류랑 비슷한 개념)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/18725e1b-5bf4-423c-b52b-a9d9f977ae57/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7b8885aa-dc6e-41ad-853e-0d9a0a32dd9d/Untitled.png)

### 03. Paging 기법 사용시 발생할 수 있는 메모리 단편화 (Memory Fragmentation) 문제에 대해 설명해주세요

- 물리적 메모리 공간이 작은 조각으로 나눠져서 메모리가 충분히 존재함에도 할당이 불가능한 상태를 보고 메모리 단편화가 발생했다고 말한다.
- Paging 기법에서는 process의 논리적 주소 공간과 물리적 메모리가 같은 크기의 page단위로 나누어지기 때문에 외부단편화 문제가 발생하지 않는다.
- **하지만 process 주소 공간의 크기가 page 크기의 배수라는 보장이 없기 때문에 프로세스의 주소 공간 중 가장 마지막에 위치한 page에서는 내부 단편화 문제가 발생할 가능성이 있다.**

![내부 단편화](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0645c55f-797a-440a-bf79-84fd70ea9d89/Untitled.png)

내부 단편화

![외부 단편화](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f86265d2-26db-4207-bb38-0675dcb9fcba/Untitled.png)

외부 단편화

### 04. segmentation 에 대해서 설명해주세요

- **segmentation**이란 process가 할당받은 메모리 공간을 논리적 의미 단위(segment)로 나누어, 연속되지 않는 물리 메모리 공간에 할당될 수 있도록 하는 메모리 관리기법이다.
- segmentation table에서 보면 paging과 달리 크기가 일정하지 않음(base시작점, limit끝점 비교)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5c906021-34e3-4b46-83a0-220bad074f36/Untitled.png)

### 05. segmentation의 메모리 단편화(Memory fragmentation) 문제에 대해 설명해주세요

- segmentation 기법에서 segment의 크기만큼 메모리를 할당하므로 내부 단편화 문제가 발생하지 않는다.
- 하지만 서로 다른 크기의 segment들이 메모리에 적재되고 제거되는 일이 반복되면 외부 단편화 문제가 발생할 수 있다.

![segment2 가 빠지면 저 공간에 딱맞게 들어올 메모리가 안들어올시 외부 단편화 문제 발생](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ff8fdb9b-0c2f-4e37-9a43-91d6fc7f87fb/Untitled.png)

segment2 가 빠지면 저 공간에 딱맞게 들어올 메모리가 안들어올시 외부 단편화 문제 발생

### 06. paging과 segmentation의 차이는 무엇인가요?

- **paging**은 일정한 크기의 단위로 나누어 할당하는데 **segmentation**은 코데힙스와 같은 기능(의미)단위로 물리 메모리에 할당하는 기법이다.
- **Paging**에서는 내부단편화가 문제, **segmentation**에서는 외부단편화가 문제가 된다.

### 07. paged segmentation 기법에 대해 설명해주세요

- **paged segmentation**이란 **segmentation**을 기본으로 하되 이를 다시 동일 크기의 **page**로 나누어 물리 메모리에 할당하는 메모리 관리 기법이다.
- 다시말해 프로그램을 의미단위의 **segment**로 나누고 개별 **segment**의 크기를 **page**의 배수가 되도록 하는 방법이다.
- 이를 통해 **segmentation** 기법에서 발생하는 외부 단편화 문제 해결 및 **segment** 단위로 process간의 공유나 process 내 접근권한 보호가 이루어지도록 해서 **paging** 기법의 단점을 해결한다.
- 다만 내부 단편화 문제는 생길 수 있음

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c101a029-7835-4bbb-850c-7fb178fd519f/Untitled.png)

### 08. 가상메모리에 대해서 설명해주세요

- 가상메모리는 실제의 물리 메모리 개념과 개발자 입장의 논리 메모리 개념을 분리한 것이다.
- 이를 통해 개발자는 메모리 크기 관련 문제에 대한 고려할 필요 없이 쉽게 프로그램을 작성할 수 있다.
- 운영체제는 가상 메모리 기법을 통해 프로그램의 논리적 주소 영역에서 필요한 부분만 물리적 메모리에 적재하고, 직접적으로 필요하지 않은 메모리 공간은 디스크(Swap 영역)에 저장하게 된다.
- 가상메모리 기법을 통해 사용자 프로그램이 물리적 메모리보다 커져도 실행이 가능하다는 장점이 있다.
- 실제 우리가 사용하고 잇는 운영체제에서는 가상메모리를 사용하고 있기 때문에 가상메모리를 이해하는 것은 개발자에게 중요하다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2e7cd700-7faa-45c2-b7fb-421dc6b12685/Untitled.png)

### 09. 요구 페이징(demand paging)에 대해 설명해주세요

- 당장 사용될 주소 공간을 page단위로 메모리에 적재하는 방법을 **요구 페이징(demand paging)**이라고 한다.
- 요구 페이징 기법에서는 특정 page에 대해 CPU의 요청이 들어온 후에 해당 page를 메모리에 적재한다.
- 당장 실행에 필요한 page만을 메모리에 적재하기 때문에 메모리 사용량이 감소하고 프로세스 전체를 메모리에 적재하는 입출력 오버헤드도 감소한다
- 요구 페이징 기법에서는 유효/무효 비트(valid/invalid bit)를 두어 각 page가 메모리에 존재하는지 표시한다.

### 10. Page fault

- CPU가 무효비트(invalid bit)로 표시된 page에 엑세스하는 상황을 page fault라고 부른다.
- CPU가 무효 page에 접근하면 주소변환을 담당하는 하드웨어인 MMU가 page fault trap을 발생시키게 되고 다음과 같은 순서로 page fault를 처리하게 된다.
    - (1) CPU가 페이지 N을 참조한다
    - (2) page table에서 페이지 N이 무효 상태임을 확인한다
    - (3) MMU에서 page fault trap을 발생시킨다.
    - (4) 디스크에서 페이지 N을 빈 프레임에 적재하고 page table을 업데이트 한다. (invalid → valid)

![CPU가 B를 읽으려고 가보니깐 물리적 메모리에 없음 이때 page fault 발생](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/92e44042-52f4-4e39-b9a7-c9b15bcb693d/Untitled.png)

CPU가 B를 읽으려고 가보니깐 물리적 메모리에 없음 이때 page fault 발생

![page table에 물리적 메모리에 없다고 적혀있음 ](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9ac2f8cb-8b55-45a2-9f8c-8d2174ebeaa0/Untitled.png)

page table에 물리적 메모리에 없다고 적혀있음 

### 11. Page 교체 알고리즘 (replacement algorithm)

- page fault가 발생하면, 요청된 page를 디스크에서 메모리로 가져온다.
- 이때 물리적 메모리에 공간이 부족할 수 있다. 그럴 경우에는 메모리에 올라와있는 page를 디스크로 옮겨서 메모리 공간을 확보해야한다. 이를 페이지 교체(page replacement)라고 하며, 어떤 page를 교체할 것이냐를 결정하는 알고리즘이 page교체 알고리즘(replacement algorithm)이라고 한다.
- 교체 알고리즘은 최대한 page fault가 적게 일어나도록 도와주어야 한다.
- 따라서 앞으로 참조될 가능성이 적은 page를 선택해서 교체해주어야 성능을 향상시킬 수 있다.

| 알고리즘 | 설명 |
| --- | --- |
| FIFO (First In First Out) | 메모리에 올라온지 가장 오래된 page를 교체한다. |
| 최적 페이지 교체 | 앞으로 가장 오랫동안 사용되지 않을 page를 찾아 교체한다. 실제구현은 어렵다 |
| LRU(Least Recently Used) | 가장 오랫동안 사용되지 않은 page를 교체한다 |
| LFU(Least Frequently Used) | 참조 횟수가 가장 적은 page를 교체한다. 비용대비 성능이 별로라 잘 사용 x |
