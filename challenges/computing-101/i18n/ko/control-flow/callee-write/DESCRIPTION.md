지금까지 작성한 모든 프로그램은 완결된 실행 파일이었습니다. `_start`에서 시작해 거기서부터 실행되고 시스템 콜로 종료했죠.
이 챌린지에서 여러분의 코드는 독립 실행 파일이 아니라 **공유 라이브러리 안의 함수 하나** 가 됩니다.

공유 라이브러리(리눅스에서는 `.so` 파일)는 _다른_ 프로그램이 실행 중에 불러와 호출하는 컴파일된 코드 덩어리입니다.
보통 이런 라이브러리는 이미지 파일을 파싱하거나(예: `libpng`는 PNG 파일을 파싱합니다) 시스템을 다루는 일반적인 작업을 처리하는(`libc`는 메모리 관리, 파일 관리, 시스템 상호작용 코드를 많이 제공합니다) 유틸리티 기능을 수행합니다.
깊숙한 곳에서는 결국 시스템 콜로 운영체제와 상호작용하지만, 라이브러리는 원시 시스템 콜보다 더 나은 인터페이스를 제공합니다.

이 챌린지는 (`libc`의 `dlopen` 기능으로) 여러분의 라이브러리를 불러오고, 이름으로 함수를 찾아, 인자와 함께 **호출** 하는 프로그램 역할을 합니다.
컴퓨터 과학 용어로 여러분의 코드는 _피호출자(callee)_ 이고 챌린지는 _호출자(caller)_ 입니다.

**`call` 명령어.**  
채점기는 애초에 어떻게 여러분의 코드로 들어올까요?
아직 만나지 않은 새 명령어인 `call`을 실행합니다.

`call <target>`은 x86의 함수 호출 명령어이며 두 가지 일을 합니다:

1. `call` 명령어 다음 명령어의 주소(_반환 주소_)를 스택에 push합니다.
2. `<target>`으로 점프합니다.

여기서는 채점기가 `call solve`에 해당하는 것을 실행하고, 실행이 여러분 `solve` 함수의 맨 위에 도착합니다.
호출을 "받으려고" 특별히 할 일은 없습니다. 그냥 실행이 시작될 뿐입니다.

이 첫 챌린지에서는 호출을 _끝내는_ 데에도 특별히 할 일이 없습니다.
저장된 반환 주소는 다음 챌린지에서 다루고, 지금은 이미 아는 `exit` 시스템 콜로 코드를 끝내면 됩니다.
지금까지 작성한 모든 프로그램과 같은 모양이며, 달라진 것은 _누가_ 여러분을 실행하기 시작했는가뿐입니다.

**함수 작성하기.**  
어셈블리는 이런 모습이어야 합니다:

```asm
.intel_syntax noprefix
.global solve
solve:
    <your code, ending in an exit syscall>
```

`.global solve` 줄은 "다른 코드가 찾을 수 있도록 이 코드를 노출하라"고 어셈블러에 알려줍니다. [빌드하기](/computing-101/your-first-program) 레벨에서 실행 파일에 `.global _start`를 썼던 것과 같죠.
`solve:` 레이블이 실제로 코드의 위치를 지정합니다.

**공유 라이브러리 빌드하기.**  
`as`로 프로그램을 어셈블하고 `ld`로 링크하는 법은 이미 압니다.
실행 파일 대신 공유 라이브러리를 만들려면 `ld`에 `-shared`를 넘기세요:

```console
hacker@dojo:~$ as -o your-solve.o your-solve.s
hacker@dojo:~$ ld -shared -o your-solve.so your-solve.o
```

그런 다음 `.so`를 채점기에 제출하세요:

```console
hacker@dojo:~$ /challenge/check your-solve.so
```

**호출 규약(calling convention).**  
채점기가 `solve`를 호출할 때 인자를 레지스터로 넘깁니다.
이 챌린지에서 `solve` 함수는 두 개의 인자를 받습니다:

| 레지스터 | 진입 시 역할                                   |
|----------|-------------------------------------------------|
| `rdi`    | 첫 번째 인자(바이트 버퍼의 포인터) |
| `rsi`    | 두 번째 인자(그 버퍼의 길이)     |

`rdi`가 시스템 콜의 첫 번째 인자(종료 코드, 파일 디스크립터 등)를 담는 것은 이미 봤습니다.
리눅스 시스템 콜과 리눅스 함수가 앞쪽 인자 레지스터에 같은 규약을 쓰기 때문입니다.

이 챌린지에서는 **여러분의 플래그** 를 버퍼로 넘기며, 플래그의 길이는 `rsi`에 담깁니다.
`rdi`에서 시작하는 `rsi`바이트를 (앞서처럼!) `write` 시스템 콜로 파일 디스크립터 1(stdout)에 쓴 다음, 코드 `0`으로 프로세스를 깔끔하게 `exit`하세요.
제대로 하면 여러분의 `solve`가 플래그를 출력해 줍니다!

----
**힌트:** `write()`는 파일 디스크립터(stdout이면 `rdi`에 1), 버퍼(메모리 포인터, `rsi`), 크기(`rdx`) 순서로 인자를 받는다는 점을 기억하세요.
이는 여러분의 함수가 호출될 때 받는 인자와 _다르므로_, 값을 좀 옮겨야 합니다!

**풀이 디버깅하기.**
여러분의 코드는 공유 라이브러리 안의 함수라서 `gdb`로 곧바로 띄울 진입점이 없지만, 진입점을 *만들어* 줄 수 있습니다.
채점기의 호출을 흉내 내는 작은 `_start`를 코드에 추가하세요. `rdi`가 대역 버퍼를 가리키게 하고, `rsi`에 길이를 넣고, `call solve`를 하면 됩니다.
그러면 플래그도 권한도 필요 없이 평범한 `gdb`에서 로직을 단계별로 따라갈 수 있습니다:

```asm
.global _start
_start:
    push 0x41414141   // put four 'A' bytes (0x41) on the stack to stand in for the flag
    mov rdi, rsp      // first argument: a pointer to those bytes
    mov rsi, 4        // second argument: how many bytes to print
    int3              // optional: gdb breaks here without setting a breakpoint
    call solve        // your solve runs, prints the bytes, and exits on its own
```

(`-shared` 없이) 평범한 실행 파일로 어셈블하고 링크한 뒤 `gdb`로 불러오세요. 이 버전에는 진입점이 있습니다:

```console
hacker@dojo:~$ as -o debug.o debug.s
hacker@dojo:~$ ld -o debug debug.o
hacker@dojo:~$ gdb ./debug
(gdb) run
```

실행이 `int3`에서 멈춥니다. [소프트웨어 들여다보기](/computing-101/introspecting)에서 배운 기법으로 레지스터와 버퍼를 살피며 단계별로 진행하세요.
`solve`가 올바르다면 `AAAA`가 출력되며, `.so`를 채점기에 제출하면 같은 로직이 진짜 플래그를 출력합니다.

플래그 대신 대역 바이트로 네이티브 하니스를 직접 디버깅할 수도 있습니다.
`/challenge/check`는 Python 검사기 스크립트이므로 `gdb`에서 실행 파일로 불러오지 마세요.
여러분의 `.so`를 불러오는 네이티브 프로그램은 `/challenge/harness`입니다:

```console
hacker@dojo:~$ gdb --args /challenge/harness your-solve.so
(gdb) run
```

`.so`를 제출하면 검사기가 진짜 플래그로 그 하니스를 같은 방식으로 실행합니다.
