# Package
sync package에서 동시성 관련된 유용한 기능을 제공.
메모리 접근 동기화가 동시성의 주된 사용 시나리오.

## Mutex
 * mutual exclusion
 * 공유 자원인 critical section에 배타적으로 접근하는 방법
 * channel이 아닌 메모리 공유 방식 제공
 * ex)
```go
import sync
sync.Mutex

Mutex.Lock()
Mutex.Unlock()
```

## WaitGroup
 * ex)
```go
import sync

sync.WaitGroup

WaitGroup.Done()
WaitGroup.Add()
WaitGroup.Wait()
```

## Once
 * ex)
```go
imoprt sync
sync.Once
Once.Do
```
## Cond
## Pool
 * ex)
```go
import sync
sync.Pool

```