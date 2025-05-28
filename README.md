🧠 Project 1 - MIPS Single-Cycle CPU Design
Verilog HDL을 사용하여 MIPS 명령어 10종을 지원하는 단일 사이클 구조의 CPU를 직접 설계하였습니다. 본 프로젝트는 명령어 수준의 ISA를 실제 하드웨어 회로로 구현하며, 명령어 디코딩, 연산, 메모리 접근, 제어 흐름까지 전체 시스템의 동작을 경험하고 이해하는 데 목적이 있습니다.

📌 프로젝트 개요
과목명: Computer Structure (컴퓨터구조)

목표: MIPS 단일 사이클 구조 CPU 설계

언어: Verilog HDL

검증 방식: 테스트 벤치 시뮬레이션 (ModelSim 사용)

구현 아키텍처: Harvard 구조, 단일 클럭 사이클 기반 처리

🔧 지원 명령어
Instruction	Type	설명
add	R	덧셈
sub	R	뺄셈
and	R	비트 AND
or	R	비트 OR
slt	R	비교 후 결과 레지스터에 설정
addi	I	상수값 덧셈
lw	I	메모리 읽기
sw	I	메모리 쓰기
beq	I	조건 분기
j	J	무조건 분기

🧩 모듈 구조 및 설명
1. Control.v
PLA(Programmable Logic Array) 방식으로 구성된 제어 유닛

Instruction opcode 및 funct 필드를 해석하여 제어 신호 생성

각 명령어에 맞는 RegWrite, ALUSrc, MemRead, MemWrite, Branch 등 신호 출력

2. Datapath.v
ALU, 레지스터 파일, 프로그램 카운터(PC), MUX, Sign-extend 등 포함

제어 신호에 따라 경로 결정

연산 수행 결과 또는 메모리 접근 후 데이터를 목적 레지스터에 저장

3. Memory.v
Instruction Memory (명령어 저장)

Data Memory (데이터 저장/읽기)

lw, sw 연산 시 주소 기반 접근 구현

4. CPU.v
위의 세 모듈을 통합하는 최상위 모듈

각 유닛 간 신호 연결 및 동기화 수행

전체 명령어 흐름 제어 및 테스트용 Entry Point 역할

5. tb_CPU.v
Testbench 설계로 다양한 MIPS 명령어를 입력하여 기능 검증

실행 결과를 시뮬레이션 파형을 통해 분석

📈 주요 학습 성과
ISA 기반 명령어가 하드웨어 회로로 어떻게 실행되는지 전 과정 학습

각 명령어별로 어떤 제어 신호가 필요한지 분석 및 회로 설계로 구현

단일 사이클 구조의 한계점(느린 클럭 주기, 확장성 문제 등) 직접 체감

이후 멀티 사이클 및 파이프라인 구조 설계에 기반이 되는 핵심 개념 내재화

🧪 시뮬레이션 결과 예시
verilog
복사
편집
// tb_CPU.v 내 테스트 예시
// ADD 연산 테스트
$display("Expected: 0x00000007, Actual: %h", uut.Registers[3]);
각 명령어 수행 결과는 파형(파형 파일 .vcd 또는 .wlf)으로 시각화하여 디버깅 수행

beq, j 등의 제어 흐름 명령어가 PC에 어떻게 영향을 주는지 확인함

📎 향후 확장 고려사항
Pipeline 설계로의 확장

캐시 메모리 및 Forwarding Logic 구현

Interrupt 및 Exception 처리 추가

