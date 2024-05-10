### queue

[python document : queue](https://docs.python.org/3.7/library/queue.html)
공식 문서의 정의에 따르면

```null
The queue module implements multi-producer, multi-consumer queues.
It is especially useful in threaded programming when information must be exchanged safely between multiple threads.
The Queue class in this module implements all the required locking semantics.
It depends on the availability of thread support in Python; see the threading module.
```

직역하자면

```null
queue module은 다중 생산자 / 소비자의 queue를 실행한다.
특히 정보가 여러 개의 스레드 간에 안전하게 교환되어야 하는 스레드 프로그래밍에서 사용된다.
이 모듈의 Queue 클래스는 필요한 모든 locking 과정들을 실행한다.
이것은 Python의 thread support가 가능함에 의존한다.
```

즉, `queue`는 멀티 스레드 환경에서 스레드 간의 안전한(thread-safe)한 소통을 위해 만들어진 **라이브러리**이다.

`queue`에서 활용 가능한 메소드들을 보면 이를 확인할 수 있다.

```null
from queue import Queue

queue = Queue()
dir(queue)
```

위 코드를 통해 살펴보면 단순한 `put`, `get`외에도 `put_nowait`, `get_nowait`, `task_done`, `join` 등의 멀티 스레드 환경에서 사용되는 메소드들이 존재하는 것을 확인할 수 있다.

### deque

[python document : deque](https://docs.python.org/3/library/collections.html#collections.deque)  
`queue`와 달리 `deque`는 파이썬의 **자료구조**의 일종이다.  
Why? `deque`은 `collections` 라이브러리에서 import 되는데 이 `collections` 라이브러리는 `container datatype`이다.

공식 문서에서도 `deque`은 `list`와 비슷하게 동작하지만, 그 연산의 복잡도에 있어 `deque`이 더 빠르게 동작하도록 설계되어 있다고 한다. (양 방향 입출력 모두 `O(1)`)