# open-source
리눅스 top, ps, jobs, kill 명령어

---
# top

> top 이란?

+ 현재 실행중인 프로세스의 상태를 실시간으로 출력해주는 명령어
+ 프로세스 상태 및 CPU, Memory의 사용량 등도 알 수 있다.  

> top 사용법

```c
top [옵션]
```

> top 옵션

-d [갱신시간] : 실행결과 갱신시간(초단위)  
-n [값] : top 명령의 실행 횟수 지정  
-p [PID] : 지정한 PID값을 가진 프로세스 정보 출력  
-b : 배치모드로 실행. 실행된 top명령의 실행결과를 log로 남기기 위한 경우 사용  

> top 출력 필드

PID : 프로세스 ID  
USER : 프로세스를 시작한 사용자 ID  
PR : 작업의 우선순위  
NI : 우선순위 주는 값으로 음수이면 우선순위 높음, 양수이면 우선순위 낮음  
VIRT : 프로세스가 사용중인 가상 메모리의 크기 (Virtual Memory)  
RES : 프로세스가 실제 사용중인 상주 메모리, 물리 메모리 (Resident Memory)  
SHR : 프로세스가 다른 프로세스와 공유중에 있는 공유 메모리 (Shared Memory)  
S : 프로세스 상태 
  >> R : Running  
   S : Sleeping  
   I : ldle  
   D : Uninterruptable Sleep  
   T : 작업제어 신호에 의해 중지  
   t : trace 디버거에 의해 중지  
   Z : Zombie

%CPU : 프로세스의 CPU 사용량  
%MEM : 프로세스가 현재 사용중인 메모리 사용량   
TIME+ : 프로세스가 사용한 CPU시간 프로세스가 시작된 이후부터 총 사용한 CPU시간   
COMMAND : 명령어 이름 혹은 명령어 라인  

---
# ps

> ps 란?

+ ps는 (Process Status)의 약자로 현재 실행중인 프로세스와 상태를 출력하는 명령어
+ 리눅스는 다중 사용자(Multi User), 다중 작업(Multi-tasking) 시스템으로 여러개의 프로세스가 동시에 실행되어진다. 이때 현재 실행중인 프로세스의 정보를 확인하기 위해 ps 명령어를 사용한다. 

> ps 사용법

```c
ps [option]
```

>ps 옵션

-A : 모든 프로세스를 출력  
-a : 세션 리더 및 터미널에 속하지 않는 프로세스를 제외하고 출력
a : 현재 터미널의 사용자 고유 프로세스를 출력
-d : 세션 리더를 제외한 모든 프로세스를 출력  
-e : 커널 프로세스를 제외한 모든 프로세스를 출
-r : 실행중인 프로세스만 출력  
x : 데몬 프로세스처럼 
-x : 로그인 상태에 있는 동안 아직 완료되지 않은 프로세스를 출력 
-F : 완전한 형식의 내용으로 출력  
-f : 완전한 형식의 목록 출력  
-j : 작업에 관련된 ID만 출력  
l : BSD 형식으로 자세한 정보 출력  
u : 프로세스의소유자를 기준으로 출력   
-u [사용자] : 특정 사용자의 프로세스 정보를 출력. 사용자를 지정하지 않은 경우 현재 사용자를 기준으로 출력  
e : 명령에 따르는 환경들을 함께 출력(-e와는 다름)  
f : 프로세스간의 관계를 트리구조로 보여줌   
n : 사용자 정보를 숫자로 표시  
-w : 출력결과를 생략하지 않고 출력  

>ps 출력 항목

USER(BSD)/UID(System V) : 프로세스 소유자 이름  
PID : 프로세스 고유번호  
PPID : 부모 프로세스 PID   
%CPU : CPU사용 비율 추정(BSD)  
%MEM : 메모리 사용 비율 추정(BSD)  
VSZ : 페이지 단위의 가상 메모리사용량   
RSS : 실제 메모리 사용량  
TTY : 프로세스 사용중인 터미널  
S(System V)/STAT(BSD) : 프로세스의 상태코드  
TIME : 총 CPU사용시간  
COMMAND : 프로세스에 실행명령  
STIME : 프로세스 시작 시간 및 날짜  
C(System V)/CP(BSD) : 짧은 기간동안의 CPU사용률  
F : 플래그  
PRI : 실제 실행 우선순위  
NI : nice 우선순위  

> ps 사용 예

1. System V 계열 명령어로 -ef 옵션은 동작중인 모든 프로세스를 완전한 포맷으로 출력  
```c
ps -ef | grep [프로세스명]
```

2. BSD 계열 명령어로 aux 옵션은 동작중인 모든 프로세스를 완전한 포맷으로 출력   
```c
ps aux | grep [프로세스명]
```
---
# jobs

> jobs 란?

+ 셸에서 실행한 프로세스 목록 확인  
+ 백그라운드로 실행중인 프로세스를 확인하는 명령어
+ 현재 중지된 프로세스를 확인하는 명령어

> jobs 사용법

jobs 명령어는 옵션과 같은 인자값이 없이 주로 사용  
단, 실행중인 작업이 없다면 아무 내용도 출력되지 않는다.  

```c
jobs [option] [job]
```

실행결과
```c
jobs  
[1] Stopped        vi  
[2]- Stopped       vi  
[3]+ Stopped       vi
```

> jobs 옵션

-i : 프로세스ID와 함께 목록 출력   
-n : 마지막 알림 이후 변경된 작업 목록만 출력  
-p : job의 프로세스 ID만 출력   
-r : 실행중인 job만 출력  
-s : 중지된 job만 출력  

> jobs 출력시 상태값

Running : 실행중인 작업  
Done : 작업이 완료 0반환  
Done(code) : 작업이 종료되었으며 0이 아닌 코드 반환  
Stopped : 작업 중지  
Stopped(SIGSTP) : SIGSTP 시그널 작업 일시 중지    
Stopped(SICSTOP) : SICSTOP 시그널 작업 일시 중지   
Stopped(SICTTIN) : SICTTIN 시그널 작업 일시 중지   
Stopped(SIGTTOU) : SIGTTOU 시그널 작업 일시 중지  

---
#kill 


> kill 이란?

+ 프로세스애 종료 시그널을 보내는 명령어
+ 시스템에 예기치 않은 문제가 생긴 프로세스를 종료시킬 수 있다.
+ 만일 kill 명령으로 종료되지 않은 프로세스는 -9 옵션을 사용하여 강제 종료하면 된다.

```c
# kill -9 PID
```

> kill 사용법

```c
kill [option] [signal] [PID 또는 %job_number]
```

> kill 주요 옵션

-l : 시그널의 종류 출력  
-s signal : 시그널의 이름 지정  

> kill 사용 예

1. 테스트 프로세스 생성
```c
sleep 90000 &
```
2. 프로세스 확인
```c
ps -ef | grep sleep | grep -v grep
root   3333 232323  0  19:24 pts/1  00:00:00 sleep 90000
```
3. 프로세스 종료
```c
kill 3333
[1]+  종료됨        sleep 90000
```
5. 프로세스 강제 종료  
```c
kill -9 3333 # 3333=[pid]
```
