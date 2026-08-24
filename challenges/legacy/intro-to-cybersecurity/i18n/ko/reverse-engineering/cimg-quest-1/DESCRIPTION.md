리버스 엔지니어링의 또 다른 목적은 _상호운용성_ 입니다.
세월은 가혹해서, 시간이 흐르는 동안 소프트웨어에는 여러 일이 일어납니다.
예를 들어 소스 코드는 보통 해당 회사의 내부 기밀이라 [사라질 수 있지만](https://www.rockpapershotgun.com/square-enix-digital-preservation-plans-slowed-by-lost-code), 바이너리 파일은 (상업적으로) 널리 배포되므로 오래 남는 경향이 있습니다.
소스 코드가 사라지면, 바이너리 파일을 리버스 엔지니어링해서 [재구성](https://decompilation.wiki/applications/program-reconstruction/)하거나 [고쳐 쓰는](https://scanlime.org/2009/04/a-binary-patch-for-robot-odyssey/) 방식으로 상호운용성을 확보해야 합니다.

이 챌린지에서는 `The Epic Quest for the Flag` 게임의 소스 코드(`/challenge/quest.py`)를 되찾았지만, 그 게임의 맞춤형 cIMG 기반 그래픽 엔진이 없습니다!
비슷한 것(`/challenge/cimg`의 평범한 cIMG 파서)을 제공했지만, 그대로는 동작하지 않습니다.
호환되도록 바이너리를 패치해야 합니다!
플래그를 밝혀낼 수 있을까요?

----
**참고:**
`/challenge/quest.py`는 `cimg`를 그래픽 엔진으로 쓰지만, 여러분에게 없는 맞춤형 버전의 `cimg`에 맞춰 만들어졌습니다.
`/challenge/quest.py NOFLAG | /challenge/cimg`로 실행하면 "호환 모드"로 돌아갑니다. 플래그는 없지만 표준 `cimg`와는 호환됩니다.
플래그를 원한다면 `cimg`를 `quest`와 맞물리도록 고친 뒤 `/challenge/quest.py | /home/hacker/your-patched-cimg`로 실행해야 합니다.

----
**힌트:**
원하는 리버스 엔지니어링 도구로 패치하거나, 패치할 바이트의 파일 내 주소를 알아내 `hexedit`으로 패치할 수 있습니다.
