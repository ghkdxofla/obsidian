# Abstract
![[Pasted image 20240219143900.png]]
# Content
- async로 Coroutine을 정의하고, await로 실행권을 Event Loop에 넘겨주는 방식으로 concurrency를 달성
- 스레드당 실행 중인 Eventloop은 하나
- 내부 queue에 등록된 코루틴들을 기억하면서 한 번에 하나씩 번갈아가며 실행
- await 키워드가 실행될 때 실행권을 Event Loop에 넘긴다
- 해당 Coroutine이 Suspend 되면서 다른 Coroutine을 마저 실행
- Event Loop은 비선점형이기 때문에 실행 중인 코루틴이 await을 사용하거나 return 해서 실행권을 Event Loop에 돌려주지 않는다면 실행권을 뺏어서 다른 코루틴을 실행할 방법이 없다
![[Pasted image 20240219144102.png]]
![[Pasted image 20240219144118.png]]
## Coroutine & Future
### Awaitable
- `await` 키워드를 붙일 수 있는 최소 조건이 Awaitable
### Coroutine
- 코루틴은 Eventloop에 등록되지 않으면 실행되지 않기 때문에, `await`을 붙이거나 Future나 Task로 감싸야 함
```
             ┌──Coroutine
             │
Awaitable◄───┤
             │
             └──Future◄────────Task
```
## 동시에 실행되는 원리
```
 Caller            Function                 Caller            Coroutine
┌─────────────┐    ┌─────────────┐         ┌─────────────┐     ┌─────────────┐
│             │    │             │         │             │     │             │
│      │      │    │             │         │      │      │     │             │
│      │      │    │             │         │      │      │     │             │
│      ▼      │    │             │         │      ▼      │     │             │
│      │      │    │             │         │      │      │     │             │
│ call └──────┼────┼───────┐     │         │ call └──────┼─────┼──────┐      │
│             │    │       │     │         │             │     │      │      │
│             │    │       │     │         │             │     │      ▼      │
│             │    │       │     │         │             │     │      │      │
│             │    │       │     │         │      ┌──────┼─────┼──────┘      │
│             │    │       │     │         │      │      │     │      suspend│
│             │    │       │     │         │      ▼      │     │             │
│             │    │       │     │         │      │      │     │             │
│             │    │       │     │         │      └──────┼─────┼──────┐      │
│             │    │       │     │         │ resume      │     │      │      │
│             │    │       │     │         │             │     │      ▼      │
│             │    │       │     │         │             │     │      │      │
│             │    │       │     │         │      ┌──────┼─────┼──────┘      │
│             │    │       │     │         │      │      │     │      suspend│
│             │    │       │     │         │      ▼      │     │             │
│             │    │       │     │         │      │      │     │             │
│             │    │       │     │         │      └──────┼─────┼──────┐      │
│             │    │       │     │         │ resume      │     │      │      │
│             │    │       │     │         │             │     │      ▼      │
│             │    │       │     │         │             │     │      │      │
│      ┌──────┼────┼───────┘     │         │      ┌──────┼─────┼──────┘      │
│      │      │    │      return │         │      │      │     │      return │
│      │      │    │             │         │      │      │     │             │
│      ▼      │    │             │         │      ▼      │     │             │
│             │    │             │         │             │     │             │
└─────────────┘    └─────────────┘         └─────────────┘     └─────────────┘
```
## Platform 별 지원 차이
- MacOS나 Unix에서는 대부분 모든 기능 지원
- Windows에 일부 제약
- [참고](https://docs.python.org/3/library/asyncio-platforms.html)
# Reference
- [Python Event Loop](https://www.pythontutorial.net/python-concurrency/python-event-loop/)
- [Python concurrency with asyncio](https://livebook.manning.com/book/python-concurrency-with-asyncio/chapter-2/52)
- [Asynchronous I/O with Python part III – native coroutines and the event loop](https://leftasexercise.com/2020/08/08/asynchronous-i-o-with-python-part-iii-native-coroutines-and-the-event-loop/)
- [asyncio 뽀개기 1 - Coroutine과 Eventloop](https://tech.buzzvil.com/blog/asyncio-no-1-coroutine-and-eventloop/)
## Asyncio 공식 문서
- [High-level API Index](https://docs.python.org/3/library/asyncio-api-index.html)
- [Low-level API Index](https://docs.python.org/3/library/asyncio-llapi-index.html)