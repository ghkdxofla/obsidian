# Abstract
- [[Django]]에서 Asynchronous한 코드 작성에 대한 부분
- 기본적으로 WSGI 대신, [ASGI](https://docs.djangoproject.com/en/5.0/howto/deployment/asgi/)를 사용해야 한다
# Content
## 기본 사용법
```python
import asyncio
import time

async def say_after(delay, what):
    await asyncio.sleep(delay)
    print(what)

async def main():
	# create_task()를 사용하지 않으면, task를 await keyword로 실행해도
	# 비동기가 아닌 동기적으로 실행됨.
	# create_task() 사용을 하지 않으면, async가 선언된 함수를 호출 시
	# 코드가 실행되지 않고 코루틴(Coroutine) 객체만 return.
    task1 = asyncio.create_task(say_after(1, 'hello'))
    task2 = asyncio.create_task(say_after(2, 'world'))

    print(f"started at {time.strftime('%X')}")

    # 두 task가 끝나길 기다린 후 실행. 비동기 실행으로 task2의 2초 소요.
    await task1
    await task2

    print(f"finished at {time.strftime('%X')}")

asyncio.run(main())  # 코루틴 실행

# 결과
started at 17:14:32
hello
world
finished at 17:14:34
```