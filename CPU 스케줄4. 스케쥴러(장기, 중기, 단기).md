# 스케쥴러(장기, 중기, 단기)

이 문서는 2022년 11월 11일에 @unchaptered에 의해서 작성되었습니다.

## 1. 스케쥴러란 무엇인가?

스케쥴러는 **어떤 프로세스에게 자원을 할당할지**를 결정하는 운영체제의 커널의 모듈을 지칭합니다.
이러한 스케쥴러는 영향력의 범위에 따라서 다음과 같은 3가지 큰 범주로 구분될 수 있습니다.

1. 장기 스케쥴러
2. 중기 스케쥴러
3. 단기 스케쥴러

### 1.1. Queue란?

스케쥴러에 대한 내용을 이해하기 위해서는 **기본적인 Queue**에 대한 내용을 알고 있어야 합니다.

자료구조의 일종인 Queue를 설명하는 가장 쉬운 예시는 **선입선출**, 영어로는 FIFO(First in First out)입니다.

<img style="width:500px;" src="https://user-images.githubusercontent.com/86306802/201363779-d2cadc62-3e1b-438b-9685-0c1d76870664.png" />

이러한 자료구조는 다음과 같이 손쉽게 구현할 수 있습니다.

```javascript
class Queue {
   
  queue = [];
   
  addProps = (value) => {
    // push는 배열의 마지막 인덱스에 붙입니다.
    this.queue.push(value);
  }
  
  removeProps = (value) => {
    // shift는 배열의 0번 인덱스를 지웁니다.
    this.queue.shift(value);
  }
}
```

이러한 Queue의 사용 목적은 **작업 관리**에 주로 쓰이고 있습니다.
아래 링크들로 더 자세한 예시를 볼 수 있습니다.

- Queue 구조의 예시 코드 : https://github.com/dailythm/dailythm-sumin/blob/main/algorithm/14%EA%B0%95_221110.md (contributed by [@sumin-dev](https://github.com/sumin-dev))
- Queue 구조로 만들어진 라이브러리 : https://www.npmjs.com/package/semaphore

### 1.2. 장기 스케쥴러

이 친구는 CPU 성능에 **장기적인 영향**을 미치기 때문에, **장기 스케쥴러**라고 불립니다.

- 행동 관점에서 보면 JOB Queue 에서 Ready Queue로 **프로세스**를 가져오는 역할을 담당합니다.
- 책임 관점에서 보면 Ready Queue에 있는 전체 프로세스를 관리하는 책임이 있습니다.

![image](https://user-images.githubusercontent.com/86306802/201362782-73cd10b1-f1b9-4005-a498-01db4503be9f.png)


https://www.scaler.com/topics/what-is-a-long-term-scheduler/
