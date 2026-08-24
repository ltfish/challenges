비슷한 두 파일 사이의 차이를 찾을 때, 눈으로 훑는 것은 그리 효율적인 방법이 아닐 수 있습니다!
이럴 때 `diff` 명령어가 큰 힘을 발휘합니다.

`diff`는 두 파일을 한 줄씩 비교해서 무엇이 다른지 정확히 보여줍니다.
예를 들면:

```console
hacker@dojo:~$ cat file1
hello
world
hacker@dojo:~$ cat file2
hello
universe
hacker@dojo:~$ diff file1 file2
2c2
< world
---
> universe
```

이 출력은 2번째 줄이 바뀌었고(`2c2`), 첫 번째 파일의 `world`(`<`)가 두 번째 파일에서 `universe`(`>`)로 바뀌었음을 알려줍니다.

새로운 줄이 추가된 경우에는 이런 것을 보게 됩니다:

```console
hacker@dojo:~$ cat old
pwn
hacker@dojo:~$ cat new
pwn
college
hacker@dojo:~$ diff old new
1a2
> college
```

이것은 첫 번째 파일의 1번째 줄 다음에 두 번째 파일에는 줄이 하나 더 있다는 뜻입니다(`1a2`는 "file1의 1번째 줄 뒤에 file2의 2번째 줄을 추가하라"는 의미입니다).

이제 여러분의 챌린지입니다!
`/challenge`에 두 개의 파일이 있습니다:
- `/challenge/decoys_only.txt`에는 가짜 플래그 100개가 들어 있습니다
- `/challenge/decoys_and_real.txt`에는 그 가짜 플래그 100개 전부와 진짜 플래그 하나가 들어 있습니다

`diff`로 두 파일의 차이를 찾아 플래그를 얻으세요!
