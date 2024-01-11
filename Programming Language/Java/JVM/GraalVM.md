# Abstract
- GraalVM은 자바와 다른 JVM 언어들로 작성된 애플리케이션의 실행을 가속화하는 동시에 JavaScript, Python 등과 같은 런타임을 제공하도록 설계된 고성능 JDK
- GraalVM은 자바 애플리케이션을 실행할 수 있는 두 가지 방법을 제공
  - [[JIT (Just-in-time)]] : 컴파일러를 이용해 런타임 중에 컴파일 및 최적화
	  ![[Pasted image 20240111093051.png]]
  - [[AoT (Ahead-of-time)]] : 컴파일러로 미리 컴파일된 네이티브 실행 파일을 실행
	![[Pasted image 20240111093101.png]]
# Reference
- [GraalVM이 제공하는 네이티브 이미지(Native Image)](https://mangkyu.tistory.com/302)