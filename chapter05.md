## 5.1 빠른 CPU를 위한 설계 기법

### 클럭

- 컴퓨터 부품들은 ‘클럭 신호’에 맞춰 일사불란하게 움직인다.
- CPU는 ‘명령어 사이클’ 이라는 정해진 흐름에 맞춰 명령어들을 실행한다.

클럭 신호가 빠르게 반복되면 CPU를 비롯한 컴퓨터 부품들은 빠른 박자에 맞춰 움직임

⇒ 더 빠르게 작동하기 때문에 일반적으로 성능이 좋음

**클럭 속도**는 헤르츠 단위로 측정

### 코어와 멀티코어

코어를 여러 개 포함하고 있는 CPU를 **멀티코어 CPU** 또는 **멀티코어 프로세서**라 부름

니는 CPU 내에 명령어를 처리하는 일꾼이 여러 명 있는 것과 같음.

### 스레드와 멀티스레드

**스레드**의 사전적 의미는 ‘실행 흐름의 단위’

- 스레드
    - 하드웨어적 스레드 : 하나의 코어가 동시에 처리하는 명령어 단위
    - 소프트웨어적 스레드 : 하나의 프로그램에서 독립적으로 실행되는 단위

가장 큰 핵심은 레지스터, 하나의 코어로 여러 명령어를 동시에 처리하돌고 만들려면 프로그램 카운터, 스택 포인터, 데이터 버퍼 레지스터, 데이터 주소 레지스터와 같이 하나의 명령어를 처리하기 위해 꼭 필요한 레지스터를 여러개 가지고 있으면 됨.

- 코어 : 명령어를 실행할 수 있는 ‘하드웨어 부품’
- 스레드 : ‘명령어를 실행하는 단위’
- 멀티코어 프로세서 : 명령어를 실행할 수 있는 하드웨어 부품이 CPU 안에 두 개 이상 있는 CPU
- 멀티스레드 프로세서 : 하나의 코어로 여러개의 명령어를 동시에 실행할 수 있는 CPU

## 5.2 명령어 병렬 처리 기법

### 명령어 파이프라인

명령어 처리 과정을 클럭 단위로 나누어 보면 일반적으로 다음과 같다

1. 명령어 인출 (Instruction Fetch)
2. 명령어 해석 (Instruction Decode)
3. 명령어 실행 (Execute Instruction)
4. 결과 저장 (Write Back)

파이프라이닝이 높은 성능을 가져오기는 하지만, 특정 상황에서는 성능 향상에 실패하는 경우도 있음

- 파이프라인 위험
    - 데이터 위험 : ‘데이터 의존성’에 의해 발생. 데이터 의존적인 두 명령어를 무작정 동시에 실행하려고 할 때
    - 제어 위험 : ‘프로그램 카운터의 갑작스러운 변화’에 의해 발생. 프로그램 실행 흐름이 바뀌어 명령어가 실행되면서 프로그램 카운터 값에 갑작스러운 변화가 생길 때. 이를 위해 사용하는 기술 중 하나가 **분기 예측**
    - 구조적 위험 : 명령어들을 겹쳐 실행하는 경우 서로 다른 명령억가 동시에 ALU, 레지스터 등고 ㅏ같은 CPU 부품을 사용하려고 할 때 (**자원 위험**)

### 슈퍼스칼라

CPU 내부에서 여러 개의 명령어 파이프라인을 포함한 구조를 **슈퍼스칼라**라고 함

### 비순차적 명령어 처리

파이프라이닝, 슈퍼스칼라 기법은 모두 여러 명령어의 순차적인 처리를 상정한 방법

명령어를 순차적으로만 실행하지 않고 순서를 바꿔 실행해도 무방한 명령어를 먼저 실행하여 명령어 파이프라인이 멈추는 것을 방지하는 기법 (의존성이 없는 명령어들)

## 5.3 CISC와 RISC

### 명령어 집합

CPU가 이해할 수 있는 명령어들의 모음을 **명령어 집합** 또는 **명령어 집합 구조**(**ISA**)라고 함

ISA가 같은 CPU끼리는 서로 명령어를 이해할 수 있지만, ISA가 다르면 서로의 명령어를 이해하지 못함 ⇒ 일종의 CPU의 언어

### CISC

**Complex Instruction Set Computer**, ‘복잡한 명령어 집합을 활용하는 컴퓨터’

명령어의 형태와 크기가 다양한 **가변 길이 명령어**를 활용

CISC가 활용하는 명령어는 명령어 수행 시간이 길고 가지각색이기 때문에 파이프라인이 효율적으로 명령어를 처리할 수 없음

### RISC

Reduced Instruction Set Computer, 1클럭 내외로 실행되는 명령어를 지향

RISC는 **고정 길이 명령어**를 활용

메모리 접근을 단순화, 최소화하는 대신 레지스터를 적극 활용. CISC보다 레지스터를 이용하는 연산이 많고, 범용 레지스터의 개수도 더 많음. 사용 가능한 명령어 개수가 CISC보다 적기 때문에 RISC는 CISC보다 많은 명령으로 프로그램을 작동