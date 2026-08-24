다음 상황을 생각해 봅시다:

```console
hacker@dojo:~$ ls
flag  flamingo  flowers
hacker@dojo:~$ cat f<TAB>
```

후보가 여러 개네요!
어떻게 될까요?

어떻게 되는지는 셸과 그 설정에 따라 다릅니다.
`bash`는 기본적으로 후보가 여러 개로 갈라지는 첫 지점까지(여기서는 `fl`) 자동으로 펼칩니다.
탭을 _두 번째_ 로 누르면 그 후보들을 출력해 줍니다.
다른 셸이나 설정에서는 후보들을 차례로 넘겨 가며 보여주기도 합니다.

이 챌린지의 `/challenge/files` 디렉터리에는 `pwncollege`로 시작하는 파일이 여럿 있습니다.
`/challenge/files/p` 정도에서 탭 자동완성을 시작해서 플래그까지 찾아가세요!

