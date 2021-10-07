### 수 체계
32 bit  기반의 숫자와 64 bit 기반의 숫자를 연산하려면 두 수를 맞춰줘야 한다 
- 더 작은 메모리 체계의 수를 더 큰 메모리 체계의 수로 맞춘다 (32 bit -> 64 bit)

- 방법 1) Sign Extension
	- Sign bit에 있는 값을 모자란 bit를 채우는데 사용
	- (음수,  양수 모두) 숫자 제대로 보존

- 방법 2) Zero-Extension
	- Sign bit 값이 아닌 0을 모자란 bit를 채우는데 사용
	- 음수 보장 x
	- 숫자가 아닌 패턴 등을 그대로 더 큰 체계로 확장시켜야 할 때 유용

대소 관계 등과 같이 +/- 구분이 중요한 경우에는 sign-extension
0과 1의 위치에 따른 패턴이 중요한 경우는 zero-extension



### Digital building blocks
#### Digital building blocks
	Gates, multiplexers, decoders, registers, arithmetic circuits, counters, memory arrays, logic arrays

#### Building blocks demonstrate hierarchy, modularity, and regularity
    Hierarchy of simpler components
    Well-defined interfaces and functions
    Regular structure easily extends to different sizes

#### Logic gates
    NOT, AND, OR, NAND, NOR, etc

### Single-input
    NOT gate, buffer

#### buf 게이트 (buffer) 
  - 논리값 그대로.
	- 왜 쓰나? 전기적으로 볼때 output에서 나오는 전류의 양을 많게 만든다.
	- 전류의 양을 많게 만드는 목적은? output에서 나오는 값을 여러 군데(여러 gate)에서 쓰려고 할 때 이것들이 정상적으로 작동하기 위한 최소한의 전류가 필요
	- 게이트들이 현실세계에서 구현될 때는 전류가 통과해서 나가는 여러 transitor의 조합으로 구현. 이런 경우 Current 양, voltage 범위, capacitance 양을 고려해서 증가시켜주며 값들을 넘겨주게 되는데 실제 boolean logic 측면에서는 변동이 없으므로 buffer라고 부른다

#### not 게이트 
  - 논리 값 반대로
  - not 게이트도 위와 같이 전류 목적으로 쓸 때가 있다

### Two-input
    AND, OR, XOR, NAND, NOR, XNOR
    
    
### ALU : 어떤 building block을 사용하여 연산을 할 지 결정
    다양한 building blocks : Adder, Subtractor, Comparator (Equality), Comparator (Less Than), Shifter, Counters
