복잡한 효과를 내려고 명령을 점점 더 많이 조합하다 보면, 합쳐진 명령줄의 길이가 금세 다루기 성가셔집니다.
그럴 때는 그 명령들을 _셸 스크립트_ 라는 파일에 담고, 그 파일을 실행해서 돌릴 수 있습니다!
예를 들어 세미콜론 기법을 떠올려 봅시다:

```console
hacker@dojo:~$ echo COLLEGE > pwn; cat pwn
COLLEGE
hacker@dojo:~$
```

`pwn.sh`라는 셸 스크립트를 만들 수 있습니다(관례상 셸 스크립트에는 `sh` 확장자를 붙이는 경우가 많습니다):

```sh
echo COLLEGE > pwn
cat pwn
```

그런 다음 새 셸(`bash`) 인스턴스의 인자로 넘겨서 실행할 수 있습니다!
셸을 이렇게 실행하면 사용자에게서 명령을 받는 대신 파일에서 명령을 읽습니다.

```console
hacker@dojo:~$ ls
hacker@dojo:~$ bash pwn.sh
COLLEGE
hacker@dojo:~$ ls
pwn
hacker@dojo:~$
```

셸 스크립트가 두 명령을 모두 실행해서 `pwn` 파일을 만들고 출력한 것을 볼 수 있습니다.

이제 여러분 차례입니다!
앞 레벨과 마찬가지로 `/challenge/pwn`을 실행한 뒤 `/challenge/college`를 실행하되, 이번에는 `x.sh`라는 셸 스크립트 안에 담고 `bash`로 실행하세요!

---
**참고:** 리눅스의 훌륭한 커맨드 라인 파일 편집기들은 아직 다루지 않았습니다.
지금은 Desktop 모드의 `Text Editor` 애플리케이션(`Applications->Accessories->Text Editor`)이나 VSCode 워크스페이스의 기본 편집기를 마음껏 쓰세요!
