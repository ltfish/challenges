첫 프로그램을 작성했다고요?
그런데 지금까지는 그것을 CPU가 실제로 실행할 수 있는 실행 파일로 빌드하는 일을 저희가 대신 해 주었습니다.
이 챌린지에서는 _여러분이_ 직접 빌드합니다!

실행 가능한 바이너리를 빌드하려면 다음을 해야 합니다:

1. 어셈블리를 파일에 작성합니다(보통 `.S`나 `.s` 확장자를 씁니다. 이 예시에서는 `program.s`를 쓰겠습니다).
2. 어셈블리 파일을 _오브젝트 파일_ 로 어셈블합니다(`as` 명령어).
3. 실행 가능한 오브젝트 파일 하나 이상을 최종 실행 바이너리로 링크합니다(`ld` 명령어)!

한 단계씩 살펴봅시다:

**어셈블리 작성하기.**  
어셈블리 파일에는 말 그대로 어셈블리 코드가 들어갑니다.
앞 레벨의 경우 이런 모습이겠죠:

```console
hacker@dojo:~$ cat program.s
mov rdi, 42
mov rax, 60
syscall
hacker@dojo:~$
```

그런데 _정보가 조금 더_ 필요합니다.
이 과정에서는 _인텔_ 어셈블리 문법을 쓴다고 했으니, 어셈블러에 그것을 알려줘야 합니다.
어셈블리 코드 맨 앞에 다음처럼 지시자를 붙이면 됩니다:

```console
hacker@dojo:~$ cat program.s
.intel_syntax noprefix
mov rdi, 42
mov rax, 60
syscall
hacker@dojo:~$
```

`.intel_syntax noprefix`는 인텔 어셈블리 문법을, 특히 명령어마다 별도의 접두사를 붙이지 않아도 되는 변형을 쓰겠다고 어셈블러에 알려줍니다.
이것은 (`mov`나 `syscall` 같은) 실제 x86 명령어가 아니므로 최종 실행 바이너리에 들어가지도, CPU에서 실행되지도 않습니다.
다른 지시자는 나중에 이야기하고, 지금은 어셈블러에 맡겨 둡시다!

**어셈블리 코드를 오브젝트 파일로 어셈블하기.**  
다음으로 코드를 어셈블합니다.
**as**sembler인 `as`로 다음과 같이 합니다:

```console
hacker@dojo:~$ ls
program.s
hacker@dojo:~$ cat program.s
.intel_syntax noprefix
mov rdi, 42
mov rax, 60
syscall
hacker@dojo:~$ as -o program.o program.s
hacker@dojo:~$ ls
program.o   program.s
hacker@dojo:~$
```

여기서 `as` 도구는 `program.s`를 읽어 이진 코드로 어셈블하고 `program.o`라는 _오브젝트 파일_ 을 만들어 냅니다.
이 오브젝트 파일에는 실제로 어셈블된 이진 코드가 들어 있지만 아직 실행할 준비가 되지는 않았습니다.
먼저 _링크_ 해야 합니다.

**오브젝트 파일을 실행 파일로 링크하기.**  
전형적인 개발 흐름에서는 소스 코드가 컴파일되고 어셈블리가 어셈블되어 오브젝트 파일이 되며, 보통 그 수가 많습니다(일반적으로 프로그램의 소스 코드 파일마다 각자의 오브젝트 파일로 컴파일됩니다).
그런 다음 이것들을 하나의 실행 파일로 _링크_ 합니다.
파일이 하나뿐이더라도 최종 실행 파일을 준비하려면 링크가 필요합니다.
"**l**ink e**d**itor"에서 온 `ld` 명령어로 다음과 같이 합니다:

```console
hacker@dojo:~$ ls
program.o   program.s
hacker@dojo:~$ ld -o program program.o
ld: warning: cannot find entry symbol _start; defaulting to 0000000000401000
hacker@dojo:~$ ls
program.o   program.s   program
hacker@dojo:~$
```

그러면 실행할 수 있는 `program` 파일이 만들어집니다!
이렇게요:

```console
hacker@dojo:~$ ./program
hacker@dojo:~$ echo $?
42
hacker@dojo:~$
```

셸에서 `$?`는 마지막으로 실행한 명령의 종료 코드를 담고 있습니다.

멋지네요!
이제 프로그램을 빌드할 수 있습니다.
이 챌린지에서는 이 과정을 직접 해보세요.
실행 파일을 빌드해서 `/challenge/check`에 넘기고 플래그를 얻으세요!

----
**_start는 뭔가요?**  
눈썰미 있는 학습자라면 `ld`가 `entry symbol _start`에 대한 경고를 찍는 것을 눈치챘을 것입니다.
`_start` 심볼은 본질적으로, ELF가 실행될 때 프로그램의 어디에서 실행을 시작해야 하는지 `ld`에 알려주는 표시입니다.
그 경고는 `_start`가 지정되지 않았으므로 코드의 맨 앞에서 실행이 시작될 것이라는 뜻입니다.
우리에게는 그것으로 충분합니다!

경고를 없애고 싶다면 코드에 `_start` 심볼을 다음처럼 지정할 수 있습니다:

```console
hacker@dojo:~$ cat program.s
.intel_syntax noprefix
.global _start
_start:
mov rdi, 42
mov rax, 60
syscall
hacker@dojo:~$ as -o program.o program.s
hacker@dojo:~$ ld -o program program.o
hacker@dojo:~$ ./program
hacker@dojo:~$ echo $?
42
hacker@dojo:~$
```

여기에는 두 줄이 더 있습니다.
두 번째 줄 `_start:`는 코드의 시작을 가리키는 start라는 _레이블_ 을 추가합니다.
첫 번째 줄 `.global _start`는 `_start` 레이블을 오브젝트 파일 수준에서만 보이게 두지 말고 링커 수준에서 _전역적으로 보이게_ 만들라고 `as`에 지시합니다.
`ld`가 링커이므로, `ld`가 `_start` 레이블을 보려면 이 지시자가 필요합니다.

이 도장의 모든 챌린지에서는 파일 맨 앞에서 실행을 시작해도 아무 문제가 없지만, 그 경고가 뜨는 것이 보기 싫다면 이제 없애는 법을 알게 되었습니다!
