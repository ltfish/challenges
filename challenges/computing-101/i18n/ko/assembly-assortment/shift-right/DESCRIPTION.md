이번에는 `shr`를 위치 맞추기에 씁니다.
입력의 두 번째 바이트를 낮은 쪽 끝으로 내린 다음, [비트 마스킹하기](/computing-101/assembly-assortment/bit-and)에서 쓴 마스크를 다시 써서 그 바이트 바깥을 전부 버리세요.

`rdi`로 값을 받아 그 *두 번째* 바이트(비트 8부터 15까지, 0~255 사이의 수)를 `rax`로 반환하는 `solve` 함수를 작성하세요.

공유 라이브러리로 빌드해서 채점기에 넘기세요:

```console
hacker@dojo:~$ as -o solve.o solve.s
hacker@dojo:~$ ld -shared -o solve.so solve.o
hacker@dojo:~$ /challenge/check solve.so
```
