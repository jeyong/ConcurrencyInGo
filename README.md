# Go 동시성 프로그래밍
## History
 * CSP (Communicating Sequential Processes)
   * C.A.R. Hoare CACM 1978
## Concept
 * Concurrency
   * 독립적으로 실행 가능한 프로세스들로 구성
   * 동시에 고려해야하는 것들
   * Structure
   * 문제 해결을 위한 솔루션을 구조화하는 방식(반드시 parallel하게 해야할 필요는 없다.)
   * ex) PC에 연결된 다양한 장치들 마우스, 키보드, 모니터 등.
   * 프로그램을 독립적으로 실행될 수 있는 조각으로 나눠서 구조화하는 것!
 * Parallelism
   * 동시에 실행되는 계산
   * 동시에 해야하는 것들
   * Execution
 * Communication
   * 독립적으로 실행되는 것들을 조직화하는데 필요한 방법 

## Rob Pike Concurrency Pattern
 * 문제 상황
   * 조건
     * Drone으로 물건 옮기기
     * 물건, Drone, Drone container, 목적지
   * 1대 드론
     * 물건이 많아서 1대 드론으로 시간이 오래 걸린다.
   * 2대 드론 (container가 없는 드론)
     * 1대 드론에만 container가 있어서 드론마다 container가 더 필요하다.
   * 2대 드론
     * 2대 모두 container 장착
     * 야적장과 목적지에서 병목 현상 발생
     * 드론들 사이에 동기화가 필요!
     * 드론들 사이에 통신은 message로!
   * 완전 독립 환경
     * 야적장과 목적지를 드론마다 별도로 마련(완전히 독립적으로 운영가능)
   * 다른 설계
     * 3대 드론이 각기 부분을 나눠서
     * 야적장에서 싣기, 옮기기, 목적지 배송
     * 각 드론은 독립적으로 실행 절차를 가지며 여기에서 코디네이션을 위한 통신이 필요하다.
   * 세분화
     * 빈 container를 옮기는 드론을 추가. 1대로 할때보다 4배 빠르게
   * 관찰
     * 기존 디자인에 동시성 절차를 추가함으로써 성능 개선
     * 더 열심히 일한다면?
 * 교훈
   * 프로세싱을 나눠는데는 다양한 방법이 있다.
   * 이것에 바로 동시성 디자인.
   * 일단 쪼개고 나면, 병렬성이 약해지며 이런 경우 적절한 작업을 하기 쉽다.

 * 컴퓨팅에 비유
   * 물건 => 웹 컨텐츠
   * 드론 => CPU
   * container => 마샬링, 렌더링, 네트워킹
   * 목적지 => 프록시, 브라우저, 데이터 종착지
### Goroutine
 * 함수로서 다른 goroutine과 동일한 주소 공간에서 독립적으로 실행되는 특징을 가진다.
 * Goroutine은 thread가 아니다
   * thrad랑 비슷하지만 훨씬 가볍다!
 * thread에 multiplex (1개 thread에 여러 goroutine이 실행)
 * goroutine이 block되는 경우 해당 thread도 block되지만 다른 goroutine은 block되지 않는다.

### Channels
 * type을 가지는 값
 * goroutine들끼리 동기화하고 정보를 교환하는 역할

### Select
 * switch문과 유사
 * 차이점은 값이 같으냐를 비교하는게 아니라 통신이 가능하냐에 따라 결정된다!
```go
//channel로부터 값을 받을 수 있느냐로 case가 결정
select {
    case v := <-ch1:
        fmt.Println("channel 1 sends", v)
    case v := <-ch2:
        fmt.Println("channel 2 sends", v)
    default:
        fmt.Println("neighter channel was ready")
}
```

## Goroutine & Channel
 * Goroutine
   * concurrent execution
 * Channel
   * synchronization and messaging
 * select
   * multi-way concurrent control 
 * 
## Package for Concurrency
 * Mutex
 * WaitGroup
 * Once
 * Cond
 * Pool

## Pattern

## Problem
 * Deadlock
 * Race condition