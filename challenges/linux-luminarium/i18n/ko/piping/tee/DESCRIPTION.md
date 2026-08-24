데이터를 한 명령에서 다른 명령으로 파이프하면 당연히 화면에서는 그 데이터를 볼 수 없게 됩니다.
이것이 늘 바람직하지는 않습니다. 예를 들어 의도치 않은 결과를 디버깅하려고("왜 두 번째 명령이 동작하지 않았지???") 명령 사이를 흐르는 데이터를 보고 싶을 수 있습니다.

다행히 해법이 있습니다!
_배관_ 의 "T자 분기관"에서 이름을 딴 `tee` 명령어는, 파이프를 흐르는 데이터를 커맨드 라인에 지정한 파일들에 복제해 줍니다.
예를 들면:

```console
hacker@dojo:~$ echo hi | tee pwn college
hi
hacker@dojo:~$ cat pwn
hi
hacker@dojo:~$ cat college
hi
hacker@dojo:~$
```

보다시피 `tee`에 파일 두 개를 주었더니, 파이프로 들어온 데이터의 사본이 셋 생겼습니다. 하나는 stdout으로, 하나는 `pwn` 파일로, 하나는 `college` 파일로요.
이것을 써서 꼬여버린 상황을 어떻게 디버깅할지 짐작이 갈 것입니다:

```console
hacker@dojo:~$ command_1 | command_2
Command 2 failed!
hacker@dojo:~$ command_1 | tee cmd1_output | command_2
Command 2 failed!
hacker@dojo:~$ cat cmd1_output
Command 1 failed: must pass --succeed!
hacker@dojo:~$ command_1 --succeed | command_2
Commands succeeded!
```

이제 직접 해보세요!
이 챌린지의 `/challenge/pwn`을 `/challenge/college`로 파이프해야 하는데, `pwn`이 여러분에게 무엇을 원하는지 보려면 데이터를 가로채야 합니다!
`tee`로 첫 시도를 파일에 복제해 두고, 저장된 출력을 살펴본 뒤, 알아낸 것을 가지고 파이프라인을 다시 실행하세요.
