자, 레지스터를 하나 더 배워봅시다: `rsi`입니다!
`rdi`와 마찬가지로 `rsi`도 데이터를 잠시 놓아둘 수 있는 곳입니다.
예를 들면:

```assembly
mov rsi, 42
```

물론 레지스터끼리 데이터를 옮길 수도 있습니다!
보세요:

```assembly
mov rsi, 42
mov rdi, rsi
```

첫 줄이 `42`를 `rsi`로 옮기듯, 둘째 줄은 `rsi`에 있는 값을 `rdi`로 옮깁니다.
여기서 한 가지 짚을 것이 있습니다. _옮긴다(move)_ 고 했지만 사실은 _설정한다(set)_ 는 뜻입니다.
위 코드가 실행되고 나면 `rsi` _와_ `rdi` 둘 다 `42`가 됩니다.
왜 `set` 같은 합리적인 이름 대신 `mov`가 선택되었는지는 수수께끼지만(아주 박식한 사람들조차 질문을 받으면 [제멋대로 추측](https://retrocomputing.stackexchange.com/questions/12968/why-is-the-processor-instruction-called-move-not-copy)에 기댑니다), 어쨌든 그렇게 되었고 우리는 여기 있습니다.

아무튼 챌린지로 넘어갑시다!
이 챌린지에서는 `rsi` 레지스터에 비밀 값을 저장해 두었고, 여러분의 프로그램은 그 값을 반환 코드로 삼아 종료해야 합니다.
`exit`는 `rdi`에 저장된 값을 반환 코드로 쓰므로, `rsi`에 있는 비밀 값을 `rdi`로 옮겨야 합니다.
`/challenge/check`를 실행하고 코드를 넘겨 플래그를 얻으세요! `/challenge/check`는 여러분의 코드를 실행하기 전에 `rsi`에 비밀 값을 넣어 줍니다.
행운을 빕니다!
