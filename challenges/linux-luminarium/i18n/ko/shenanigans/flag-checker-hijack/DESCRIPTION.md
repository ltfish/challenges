앞 레벨에서는 Zardus의 `~/.bashrc`를 악용해 그가 여러분 대신 명령을 실행하게 만들었습니다.

이번에 Zardus는 로그인한 뒤 읽을 수 있는 파일에 플래그를 그냥 두지 않습니다.
대신 `flag_checker`라는 명령을 실행해서 플래그를 직접 타이핑해 검증합니다.

여러분의 임무는 Zardus의 `.bashrc`에 대한 쓰기 권한을 계속 이용해 이 플래그를 가로채는 것입니다.
[PATH 파헤치기](/linux-luminarium/path) 모듈에서 명령을 가로챘던 것을 기억하나요?
그 능력으로 `flag_checker`를 가로챌 수 있을까요?

----
**힌트:**
Zardus가 여러분의 가로채기를 눈치채고 겁먹었나요?
그는 조심스러워서 `flag_checker`의 `Type the flag` 프롬프트를 확인합니다.
여러분의 가짜도 이 프롬프트를 출력하게 하세요(예: `echo "Type the flag"`).
그 프롬프트를 출력하는 것 말고, 가짜 `flag_checker`는 a) Zardus의 입력을 stdout으로 `cat`하거나(예: 인자 없는 `cat`), b) `read`로 변수에 읽어 `echo`로 내보내면 됩니다.
여러분 마음대로 하세요!

----
**힌트:**
[권한 들여다보기](/linux-luminarium/permissions) 모듈에서 배운 대로, 가짜 `flag_checker`를 실행 가능하게 만드는 것을 잊지 마세요!
