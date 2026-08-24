어떤 명령어는 man 페이지와 도움말 옵션을 갖춘 프로그램이 아니라, 셸 자체에 내장되어 있습니다.
이런 것들을 *빌트인(builtin)* 이라고 부릅니다.
빌트인은 명령어처럼 실행하지만, 다른 프로그램을 띄우는 대신 셸이 내부적으로 처리합니다.
셸 빌트인 목록은 *빌트인* 인 `help`를 실행해서 볼 수 있습니다:

```console
hacker@dojo:~$ help
```

특정 빌트인에 대한 도움말은 그 이름을 `help` 빌트인에 넘겨서 볼 수 있습니다.
앞에서 이미 써 본 빌트인인 `cd`를 살펴봅시다!

```console
hacker@dojo:~$ help cd
cd: cd [-L|[-P [-e]] [-@]] [dir]
    Change the shell working directory.
    
    Change the current directory to DIR.  The default DIR is the value of the
    HOME shell variable.
...
```

유용한 정보네요!
이 챌린지에서는 `help`로 빌트인의 도움말을 찾아보는 연습을 합니다.
이 챌린지의 `challenge`는 프로그램이 아니라 셸 빌트인입니다.
앞서와 마찬가지로, 도움말을 찾아서 거기에 넘겨야 할 비밀 값을 알아내야 합니다!
