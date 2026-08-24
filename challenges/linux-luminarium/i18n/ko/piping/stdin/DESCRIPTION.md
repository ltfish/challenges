프로그램의 _출력_ 을 리다이렉트할 수 있듯이, 프로그램 _으로_ 들어가는 입력도 리다이렉트할 수 있습니다!
`<`로 다음과 같이 합니다:

```
hacker@dojo:~$ echo yo > message
hacker@dojo:~$ cat message
yo
hacker@dojo:~$ rev < message
oy
```

입력 리다이렉션을 쓰면 여러 프로그램으로 흥미로운 일을 할 수 있습니다!
이 레벨에서는 `/challenge/run`을 연습하는데, `PWN` 파일을 그 프로그램으로 리다이렉트하되 `PWN` 파일이 `COLLEGE`라는 값을 담고 있어야 합니다!
그 값을 `PWN` 파일에 쓰려면 `echo`의 출력 리다이렉션을 다뤘던 앞 챌린지를 떠올리세요!
