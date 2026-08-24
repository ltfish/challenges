파일(또는 명령의 출력 줄)이 늘 원하는 순서로 되어 있지는 않습니다!
`sort` 명령어는 데이터를 정리하는 데 도움이 됩니다.
입력(또는 파일)에서 줄을 읽어 정렬된 순서로 출력합니다:

```console
hacker@dojo:~$ cat names.txt
  hack
  the
  planet
  with
  pwn
  college
hacker@dojo:~$ sort names.txt
  college
  hack
  planet
  pwn
  the
  with
hacker@dojo:~$
```

`sort`는 기본적으로 줄을 사전 순으로 정렬합니다.
인자로 이를 바꿀 수 있습니다:

- `-r`: 역순 (Z에서 A로)
- `-n`: 숫자 정렬 (숫자용)
- `-u`: 중복을 없앤 고유한 줄만
- `-R`: 무작위 순서!

이 챌린지에는 `/challenge/flags.txt` 파일에 가짜 플래그 100개가 들어 있고, 그 사이에 진짜 플래그가 섞여 있습니다.
사전 순으로 정렬하면 진짜 플래그가 맨 마지막에 옵니다(가짜 플래그를 만들 때 그렇게 되도록 해 두었습니다).
가서 가져오세요!
