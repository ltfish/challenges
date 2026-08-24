앞 레벨의 챌린지는 gdb 안팎 모두에서 여러분의 대화형 셸 환경을 물려받았습니다.
현실에서는 여러분의 로컬 환경과 분석 대상 사이의 환경 차이가 훨씬 큰 경우가 많습니다.
셸에서 디버깅하는 바이너리와 서비스, 크론 작업, 원격 스크립트로 도는 같은 바이너리는 완전히 다른 환경(다른 `HOME`, 다른 `PATH`, 아예 다른 변수 _집합_)을 보게 됩니다.

이 레벨은 그 개념을 조금 더 살펴봅니다.
여기서 `gdb` 래퍼는 셸에서 물려받는 대신 자기 환경을 직접 설정하고, 챌린지를 직접 실행할 때는 여러분에게도 똑같이 하도록, 즉 변수가 딱 하나뿐인 환경을 요구합니다.
예를 들면:

```console
hacker@dojo:~$ /challenge/program
You're running me with 8 environment variables, but I need exactly 1! Clear the environment and set one variable, then rerun me!
hacker@dojo:~$ /challenge/program
```

환경은 어떻게 비울까요?
[리눅스 루미나리움](/linux-luminarium/variables)에서 export된 환경 변수를 전부 출력할 때 써본 `env` 명령으로 할 수 있습니다.
`env` 명령은 프로그램의 환경을 세밀하게 통제하는 _래퍼_ 로도 쓸 수 있습니다.
예를 들어 `env -i`로 자식 프로그램의 환경을 완전히 비울 수 있습니다:

```console
hacker@dojo:~$ env -i /challenge/program
You're running me with 0 environment variables, but I need exactly 1! Clear the environment and set one variable, then rerun me!
hacker@dojo:~$ /challenge/program
```

환경을 비운 뒤 변수를 설정할 수도 있습니다:

```console
hacker@dojo:~$ env -i PWN=COLLEGE HACK=PLANET /challenge/program
You're running me with 2 environment variables, but I need exactly 1! Clear the environment and set one variable, then rerun me!
hacker@dojo:~$ /challenge/program
```

덕분에 환경을 아주 세밀하게 통제할 수 있습니다.
이 챌린지에서는 그 세밀한 통제로 조금 더 현실적인 상황에서 주소를 맞춰보게 되지만, 다른 상황에서도 쓸 수 있는 능력이라는 점을 기억해 두세요!
