방금 살펴본 왼쪽 시프트를 이제 코드로 옮겨봅시다.

`rdi`로 64비트 값을 받아 왼쪽으로 4칸 시프트하고(16을 곱하고) 그 결과를 `rax`로 반환하는 `solve` 함수를 작성하세요.

공유 라이브러리로 빌드해서 채점기에 넘기세요:

```console
hacker@dojo:~$ as -o solve.o solve.s
hacker@dojo:~$ ld -shared -o solve.so solve.o
hacker@dojo:~$ /challenge/check solve.so
```
