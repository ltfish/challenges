다음으로 gdb로 프로세스 메모리를 들여다보는 법을 배웁니다!

`x/<n><u><f> <address>` 형태의 명령으로 메모리 내용을 e**x**amine할 수 있습니다. 이 형식에서 `<u>`는
표시할 단위 크기, `<f>`는 표시할 형식, `<n>`은 표시할 요소의 개수입니다. 유효한
단위 크기는 `b`(1바이트), `h`(2바이트), `w`(4바이트), `g`(8바이트)입니다. 유효한 형식은 `d`(10진수), `x`
(16진수), `s`(문자열), `i`(명령어)입니다. 주소는 레지스터 이름, 심볼 이름, 절대 주소로 지정할 수 있습니다.
또한 주소를 지정할 때 수식을 쓸 수도 있습니다.

예를 들어 `x/8i $rip`는 현재 명령 포인터에서 다음 8개 명령어를 출력합니다. `x/16i main`은
main의 처음 16개 명령어를 출력합니다. `disassemble main`(줄여서 `disas main`)으로 main의 모든
명령어를 출력할 수도 있습니다. 한편 `x/16gx $rsp`는 스택의 처음 16개 값을 출력합니다. `x/gx $rbp-0x32`는
스택의 그 자리에 저장된 지역 변수를 출력합니다.

명령어는 아마 올바른 어셈블리 문법으로 보고 싶을 것입니다. 그렇게 하려면 `set disassembly-flavor intel`
명령을 쓰세요.

이 레벨을 풀려면 스택에 있는 무작위 값(`/dev/urandom`에서 읽어온 값)을 알아내야 합니다.
read 시스템 콜의 인자가 무엇인지 생각해 보세요.

----
**관련 문서:**
- gdb의 [run](https://sourceware.org/gdb/current/onlinedocs/gdb#Starting) 명령
- gdb의 [continue](https://sourceware.org/gdb/current/onlinedocs/gdb#Continuing-and-Stepping) 명령
- gdb의 [info](https://sourceware.org/gdb/current/onlinedocs/gdb#Registers) 명령
- gdb의 [print](https://sourceware.org/gdb/current/onlinedocs/gdb#Data) 명령
- gdb의 [examine](https://sourceware.org/gdb/current/onlinedocs/gdb#Memory) 명령
