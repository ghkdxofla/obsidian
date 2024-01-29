# Abstract
- [[TBD]]
# Content
## 각 EC2 별 성능 비교 Benchmark
![[Pasted image 20240124162158.png]]
- Use _5th-Gen_ as much as possible
    1. _5th-Gen_ has better performance in CPU and Memory. **~25% faster** in CPU and **10 times faster** in memory.
    2. _5th-Gen_ is **15% cheaper** than _4th-Gen_ - $0.231 per hour for c4.xlarge and $0.196 per hour for c5.xlarge in Singapore.
- Use _C-Series_ for CPU-bound applications, _C-Series_ CPU performance is **~20% better** than _M/R-Series_.
- _AMD_ instances is **20% faster** in CPU but **25% slower** in Memory.
- [링크](https://dev.to/yaorenjie/benchmarks-of-aws-ec2-5-4-3-series-1kpl)
# Reference
- [왜 우리는 AWS Graviton2 사용해야 하는가?](https://medium.com/spoontech/%EC%99%9C-%EC%9A%B0%EB%A6%AC%EB%8A%94-aws-gravition2-%EC%82%AC%EC%9A%A9%ED%95%B4%EC%95%BC-%ED%95%98%EB%8A%94%EA%B0%80-6cb8b5858552)
	- Graviton Instance를 사용할 때 비교 분석에 도움이 되는 사이트