# 프로세스 관리

## **프로세스**
**프로세스**는 디스크에 있는 프로그램이 메인 메모리에 올라와 있는 상태를 말한다. 프로세스는 CPU가 일을 처리할 때 사용하는 단위로 task와 동의어이다.

>프로그램은 일반적으로 하드디스크에 저장되어 아무 일도 하지 않는 상태이다. <br>
프로세스는 싱행하면서 stack pointer, data, text, register 등이 끊임없이 변하고 job, task 등으로 불리기도 한다.

<br>

## **프로세스의 상태**
현대에서 사용되는 멀티 태스킹 시스템에서 **프로세스**는 다른 프로세스들과 CPU를 공유하기 위해 여러가지 상태를 가진다.

- **new** : 프로그램이 메모리에 올라와 프로세스가 생성된 상태
- **ready** : 작업할 준비를 하고 CPU 할당을 기다리는 상태
- **running** : CPU 할당을 받아 명령어가 실행되고 있는 상태
- **waiting** : 어떠한 이벤트를 기다리는 상태(I/O, signal과 같은 것)
- **terminated** : 프로세스의 실행이 완료된 상태

<br>

![img](https://t1.daumcdn.net/cfile/tistory/9974B4465CC131A60E)

위 그림은 **프로세스 상태 전이도**의 모습이다.
new에서부터 프로세스가 어떤 작업에 의해 상태가 변화하는지를 보여준다. <br>
running에서 ready로 변할 때는 time sharing system에서 해당 프로세스가 CPU 시간을 모두 소진하였을 때 인터럽트에 의해 강제로 ready 상태로 변하고 CPU는 다른 프로세스를 실행시킨다.

<br>

## **PCB(Process Control Block)**
모든 프로세스들은 PCB를 가지고 있다. <br>
**PCB**는 프로세스에 관한 모든 정보를 가지고 있는 데이터 구조이다. <br>
**PCB**가 가지고 있는 프로세스의 정보들은 다음과 같다.

- **Process State** : 프로세스의 상태
- **Process ID, Parent Process ID** : 프로세스를 식별, 관리하기 위한 번호
- **CPU registers, PC(Program Counter)** : 프로세스 CPU 할당을 넘겨줄 때 당시의 CPU 레지스터의 내용과 다음 처리할 명령어의 주소
- **CPU Scheduling Information** : 프로세스의 우선순위와 스케쥴링 큐를 위한 포인터
- **Memory Management Information** : 사용중인 메모리의 주소와 할당받은 메모리의 주소
- **Accounting Information** : 타임 슬라이스를 위한 CPU 할당 시간
- **I/O Status Information** : 할당된 디바이스들과 연 파일 정보 등

<br>

![img](https://images.velog.io/images/chappi/post/3a88138f-5bc8-4756-8f39-955b89a560a2/1.jpg)

<br>

## **프로세스 큐(Queue)**
프로세스는 수행하면서 상태가 여러번 변하는데 이에 따라 서비스를 받아야 할 곳이 다르다. <br>
프로세스는 일반적으로 여러개가 한번에 수행되므로 그에 따른 순서가 있어야한다. <br>
이런 순서를 대기하는 장소를 **큐(Queue)**라고 부른다.

<br>

![img](https://velog.velcdn.com/images%2Fragi%2Fpost%2F070d1bab-5522-4772-88d0-3d577ab592b9%2Fimage.png)

<br>

- **Job Queue** : 하드디스크에 있는 프로그램이 실행되기 위해 메인 메모리의 할당 순서를 기다리는 곳
- **Ready Queue** : CPU 점유 순서를 기다리는 큐이다.
- **Device Queue** : I/O를 하기 위한 여러장치가 있는데, 각 장치를 기다리는 큐가 각각 존재한다.

<br>

이런 여러가지 큐가 존재하고 각 큐 내부에 저장된 실제 데이터는 각 프로세스의 PCB가 저장되어 있다. <br>
이런 순서를 기다리는 공간이 있다면, 그 순서를 정해주는 알고리즘이 있는데 이 알고리즘을 스케쥴링(Scheduling)이라고 한다.

- **Job Queue** : Job Scheduler (Long-term Scheduler)
- **Ready Queue** : CPU Scheduler (Short-term Sheduler)
- **Device Queue** : Device Scheduler