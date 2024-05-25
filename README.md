# open-source
리눅스 top, ps, jobs, kill 명령어

---
# 1.top

> top 이란?

+ 현재 실행중인 프로세스의 상태를 실시간으로 출력해주는 명령어  
+ top 명령어는 시스템의 프로세스/메모리 사용 상태를 5초의 간격으로 업데이트하여 출력  
+ 프로세스 상태 및 CPU, Memory의 사용량 등도 알 수 있다.  

> top 사용법

```c
top [옵션]
```

> top 옵션

-b : 배치모드로 실행. 실행된 top명령의 실행결과를 log로 남기기 위한 경우 사용  
-b : 배치모드로 정보를 출력. 실시간 상화 대화형모드로 정보를 화면에 일렬로 출력  
-d delay : 지정한 시간(delay 초)의 간격으로 정보를 업데이트하여 출력  
-i idle : 토글값이 off일 때, idle 프로세스나 좀비 프로세스 정보를 출력하지 않는다  
-n num : 지정한 시간(num)만큼 업데이트 정보를 출력  
-p pid : 지정한 프로세스 ID(pid)의 정보만을 출력  
-q : 시간의 간격 없이 계속하여 업데이트 정보를 출력  
-s : 몇 개의 대화식 명령을 비활성화 (시큐어 모드)    
-S : 누적된 정보를 출력 (cumulative 모드)  


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
>  > 
%CPU : 프로세스의 CPU 사용량  
%MEM : 프로세스가 현재 사용중인 메모리 사용량   
TIME+ : 프로세스가 사용한 CPU시간 프로세스가 시작된 이후부터 총 사용한 CPU시간   
COMMAND : 명령어 이름 혹은 명령어 라인  

> 실제 top명령 실행 예시

![image](https://github.com/uueonn/open-source/assets/170390635/7acb1a97-a835-46ba-9c69-514d743fb413)

---
# 2.ps

> ps 란?

+ ps명령어는 현재 실행중인 프로세스와 상태를 출력하는 명령어  
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
-e : 커널 프로세스를 제외한 모든 프로세스를 출력  
-r : 실행중인 프로세스만 출력  
x : 터미널이 없는 프로세스를 출력  
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

> 실제 ps명령 실행 예시

+ps로 현재 사용하는 프로세스의 상태를 살펴보자. 아래는 PID, TTY, TIME, CMD 헤더의 필드와 내용을 출력한다.  

![image](https://github.com/uueonn/open-source/assets/170390635/ae117a82-9b09-41e2-b7f3-d56679172505)

+ 아래와 같이 -u 옵션은 사용자의 프로세스를, -l 옵션은 자세한 정보를 출력한다.

![image](https://github.com/uueonn/open-source/assets/170390635/bbdc589f-9c1a-491c-8c05-2e2ba2d31962)

+ 시스템의 모든 프로세스를 확인할 경우 aux 옵션을 사용한다.

![image](https://github.com/uueonn/open-source/assets/170390635/f1581e57-6955-48ef-9cf3-e4172bb46631)

+ 다음은 자주 사용하는 ps 옵션의 조합이다. 표준 문장으로 시스템의 모든 프로세스를 출력한다

![image](https://github.com/uueonn/open-source/assets/170390635/3ba1949c-8343-4ebd-8d38-509b31790d22)

---
# 3.jobs

> jobs 란?

+ 셸에서 실행한 프로세스 목록 확인  
+ 백그라운드로 실행중인 프로세스 확인하는 명령어  
+ 현재 중지된 프로세스를 확인하는 명령어  
+ jobs는 작업이 중지된 상태, 백그라운드로 진행 중인 작업 상태, 변경되었지만 보고되지 않은 상태 등을 표시   

> jobs 사용법

jobs 명령어는 옵션과 같은 인자값이 없이 주로 사용  
단, 실행중인 작업이 없다면 아무 내용도 출력되지 않는다.  

```c
jobs [option] [job]
jobs -x command [args]
```
실행결과
```c
[1] Stopped        vi
[2]- Stopped       vi
[3]+ Stopped       vi
```

> jobs 명령어 옵션

-l : 프로세스 그룹 ID를 state 필드 앞에 출력  
-n : 프로세스 그룹 중에 대표 프로세스 ID를 출력   
-p : 각 프로세스 ID에 대해 한 행씩 출력  
-r : 실행중인 job만 출력    
-s : 중지된 job만 출력  
command : 지정한 명령어를 실행    

> jobs 출력시 상태값

Running : 작업이 일시 중단되지 않았고 종료하지 않고 계속 진행 중  
Done : 작업이 완료되어 0을 반환하고 종료  
Done (code) : 작업이 정상적으로 완료했으며, 0이 아닌 코드를 반환  
Stopped : 작업이 일시 중단  
Stopped (SIGTSTP) : SIGTSTP 신호가 작업을 일시 중단  
Stopped (SIGSTOP) : SIGSTOP 신호가 일시 중단  
Stopped (SIGTTIN) : SIGTTIN 신호가 작업을 일시 중단  
Stopped (SIGTTOU) : SIGTTOU 신호가 작업을 일시 중단  

> jobs 명령 실행 예시

+ 현재 환경의 작업 상태를 아래와 같이 확인할 수 있다.  

![image](https://github.com/uueonn/open-source/assets/170390635/fd087816-ff7e-4eba-8fca-ab3f5b3449f7)

+ -l 옵션은 state 필드 앞에 프로세스 ID를 출력한다.  

![image](https://github.com/uueonn/open-source/assets/170390635/fd93bfc1-accf-488b-b31e-7f0fb1812d4e)

+ 다음과 같이 하면 v로 시작하는 모든 프로세스 ID를 확인할 수 있다.

![image](https://github.com/uueonn/open-source/assets/170390635/79ca071b-4665-4fa8-9851-aa9b6ac7b532)

---
# 4.kill 

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

-l : 모든 시그널 목록을 표시  
-s : 전달할 시그널의 종류를 지정  
pid ··· : 종료시킬 프로세스 ID나 프로세스 이름을 지정  
-s signal : 시그널의 이름 지정  
-9 : 프로세스를 강제로 종료  
-1, : -HUP 프로세스를 재활성화  
-15 : SIGTERM 시그널을 보내어 정상 종료를 요청  

> 주요 시그널

SIGHUP : 세션 종료 시그널  
SIGINT : 인터럽트 시그널  
SIGKILL	: 강제 종료 시그널  
SIGTERM	: 정상 종료 요청 시그널  
SIGSTOP : 프로세스 일시 정지 시그널  

+ kill 명령어는 다양한 종류의 신호를 프로세스에 보낼 수 있다. 각 신호는 특정한 행동을 유발한다. 예를 들어, SIGKILL 신호는 프로세스를 강제로 종료시키는 반면, SIGTERM 신호는 프로세스에게 안전하게 종료할 수 있는 기회를 제공한다.  

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

> 실제 kill 명령 실행 예시

1. 아래와 같이 ps 명령어로 sshd 프로세스를 확인할 수 있다.

![image](https://github.com/uueonn/open-source/assets/170390635/82f7ac67-70a4-4e06-8eae-a238312ff3f3)

현재 sshd 프로세스는 root 사용자 권한으로 동작하고 있으며 PID는 2518와 12095이다.

2. ps 명령으로 확인한 PID를 이용하면 원하는 프로세스를 종료시킬 수 있다.

![image](https://github.com/uueonn/open-source/assets/170390635/a081cfba-6d41-4dbc-a24f-a92b6c508bc2)

3. 만일 kill 명령으로 종료되지 않으면 -9 옵션으로 강제 종료시킬 수 있다.

![image](https://github.com/uueonn/open-source/assets/170390635/bc29ae48-c501-490d-bbfd-d002a6bf7a79)

4. kill -HUP pid 명령을 이용하면 프로세스를 종료 후 다시 재실행한다.

![image](https://github.com/uueonn/open-source/assets/170390635/ba1ac951-b74d-4574-a6cc-72b49af165fa)


+ 먼저, ps -ef 명령어를 사용하여 종료하려는 프로세스의 ID를 확인한다. 그 후, kill -15 [프로세스ID] 명령어로 프로세스에 안전 종료 신호를 보낸다. 만약 프로세스가 이 신호에 반응하지 않는 경우, kill -9 [프로세스ID] 명령어를 사용하여 강제로 종료할 수 있다.
  
![image](https://github.com/uueonn/open-source/assets/170390635/2f20f683-8661-490e-bc51-b3cb3cfbdd94)

