운영체제프로젝트 readme파일
=====================
# 실행환경
vscode내부에서 그냥 컴파일 시 오류가 발생해 terminal을 사용해 

1. gcc -o procon procon.c -pthread (컴파일)

2. ./procon (실행)

가. gcc -o rdwr rdwr.c -pthread (컴파일)

나. ./rdwr (실행)

이런 방식으로 터미널로 파일을 만들어서 직접 실행시켰다.

# 구현내용, 방법

producer/consumer : 

pthread_create 를 사용해서 producer 와 consumer각각 thread 2개씩 만들고

처음엔 semaphore 없이 실행시켜서 race condition이 발생하게 만들고

다음엔 semaphore 을 추가해서 실행하였다

mutex semaphore을 추가하여서 critical section을 들어갈때는 Lock을 걸고 나올때는 lock을 풀게 만들었고

full, empty semaphore을 추가하여서 empty일때 producer가 생산하게하고, full일때 생산하지 않고 consumer한테 신호를 보내 사용하게 한다.

reader/writer

pthread_create를 사용해서 reader 와 writer을 각각 3개씩 만들고

처음엔 semaphore없이 실행시켜서 race condition이 발생되게 하고

다음엔 semaphore을 추가하여 실행하였다.

mutex semaphore을 추가하여서 reader들로부터 critical section을 보호하게 만들고

wrt semaphore을 추가하여서 writer가 실행중인지를 reader에게 알려주도록 하였다.

read_count를 추가하여서 읽고 있는 reader의 수를 계산하도록 하였다.

만약 reader의 수가 없으면 다시 writer가 접근하도록 wrt semaphore을 변경시키도록 해 주었다.


