# Abstract
- [[Python]]에서 사용하는 Scheduling Library
# Content
## 실행 Worker의 수 설정
- [문서](https://apscheduler.readthedocs.io/en/3.x/modules/executors/pool.html) 참고
- 각, Thread Pool, Process Pool을 구분하여 사용할 수 있음
- 실제 적용 시, `add_job()` 에 Argument 전달
	- [링크](https://stackoverflow.com/questions/34214511/why-does-the-processpoolexecutor-ignore-the-max-workers-argument)
### 현재 실행 중인 APScheduler의 Thread 수 확인 방법
```bash
ps -ef | grep py # python 프로세스의 PID 추출 ps hH p {PID} | wc -l # 해당 프로세스의 thread 개수 도출
```
# Reference
- [APScheduler 스케쥴링 라이브러리](https://jbf-story.tistory.com/32)