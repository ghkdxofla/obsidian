# Abstract
- 특정 시점에 자신의 실행과 관련된 상태를 어딘가에 저장한 뒤 실행을 중단하고, 나중에 그 상태를 복원하여 실행을 재개할 수 있는 Subroutine
- Subroutine은 일반적으로 우리가 정의해서 사용하는 함수
# Content
## Coroutine vs Subroutine
### Subroutine
- 반복적인 기능을 모은 동작
- main 함수 내에서 실행되는 개별 함수의 흐름
- 서브루틴이 종료될 때까지 제어권이 유지되며, 서브루틴 종료 시 데이터 및 상태가 제거되며 호출 지점에 제어권을 반납
	![[Pasted image 20240129101725.png]]
### Coroutine
- Concurrency
- 실행의 지연과 재개를 허용함으로써, 비선점적 멀티태스킹을 위한 서브 루틴을 일반화
	- Non-preemptive : 하나의 프로세스가 CPU를 할당받으면 종료되기 전까지 다른 프로세스가 CPU를 강제로 차지할 수 없음 `Coroutine`
	- preemptive : 하나의 프로세스가 다른 프로세스 대신에 프로세서(CPU)를 강제로 차지 `Thread`
- 비선점형이기 떄문에 Context Switching이 발생하지 않음
- 실행과 관련된 데이터와 상태를 모두 유지
- 제어권 상시 반환 가능
- 코루틴이 종료될 때까지 데이터 및 상태가 유지되며, 필요 시 제어권을 언제든지 반납할 수 있음
	![[Pasted image 20240129101825.png]]
- 스레드 내에 동작하는 하나의 단위
	- 단일 스레드에서 실행
	- 스레드 관리를 위한 메모리 사용이 없어 효율적
	- 멀티 스레드 환경보다 코드 작성이 쉽고, 안전함
	![[Pasted image 20240129102956.png]]
## 언어 별 특징
### [[Python]]
- Django 에서의 사용법은 [[Async]] 참조
- Python에서는 Generator로 구현된 것이 특징
```python
def generator_outer():
       yield 1
       yield from another_generator()
       yield 4
   
   def another_generator():
       yield 2
       yield 3
   
   >>> result = list(generator_outer())
   >>> print(result)
   [1, 2, 3, 4]
```
- `async` keyword는 일종의 syntactic sugar
	![[Pasted image 20240129102543.png]]
- Coroutine 실행을 위해선 Coroutine Object 외에 `Task`, `Future`, `Event loop`