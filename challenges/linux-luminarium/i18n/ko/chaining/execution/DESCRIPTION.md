첫 셸 스크립트를 작성했지만, `bash script.sh`로 호출하는 것은 번거롭습니다.
저 `bash`가 왜 필요할까요?

`bash script.sh`를 실행하면 당연히 `script.sh`라는 인자와 함께 `bash` 명령을 실행하는 것입니다.
이것은 bash에게 표준 입력 대신 `script.sh`에서 명령을 읽으라고 알려주고, 그렇게 여러분의 셸 스크립트가 실행됩니다.

사실 `bash`를 직접 실행할 필요를 없앨 수 있습니다.
셸 스크립트 파일이 _실행 가능_ 하다면([파일 권한](/linux-luminarium/permissions)을 떠올려 보세요), 상대 경로나 절대 경로로 그냥 실행할 수 있습니다!
예를 들어 홈 디렉터리에 `script.sh`를 만들고 _실행 가능하게 만들면_, `/home/hacker/script.sh`나 `~/script.sh`, 또는 (작업 디렉터리가 `/home/hacker`라면) `./script.sh`로 실행할 수 있습니다.

여기서 해보세요!
`/challenge/solve`를 실행하는 셸 스크립트를 만들고, 실행 가능하게 만든 다음, `bash`를 명시적으로 부르지 않고 실행하세요!
