`tmux`로 같은 것을 해봅시다!

`tmux`(터미널 멀티플렉서)는 screen의 더 젊고 현대적인 사촌입니다.
같은 일을 하지만 키 바인딩이 조금 다릅니다.
가장 큰 차이는요?
tmux는 명령 접두 키로 `Ctrl-A` 대신 `Ctrl-B`를 씁니다.

그래서 tmux에서 분리하려면 `Ctrl-B`를 누른 다음 `d`를 누릅니다.

```console
hacker@dojo:~$ tmux
[doing some work...]
[Press Ctrl-B, then d]
[detached (from session 0)]
hacker@dojo:~$ 
```

명령어도 다릅니다:
- `tmux ls` - 세션 목록 보기
- `tmux attach` 또는 `tmux a` - 세션에 다시 붙기

이 챌린지에서는:
1. tmux를 실행합니다
2. 거기서 분리합니다.
3. `/challenge/run`을 실행합니다(분리된 세션으로 플래그를 보냅니다!)
4. 다시 붙어서 상품을 확인합니다
