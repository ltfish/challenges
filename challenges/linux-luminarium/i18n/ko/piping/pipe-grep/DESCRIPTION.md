앞 레벨처럼 결과를 파일에 저장할 필요 없이 "중간 단계를 건너뛸" 수 있습니다.
`|`(파이프) 연산자를 쓰면 됩니다.
파이프 왼쪽 명령의 표준 출력이 오른쪽 명령의 표준 입력에 연결됩니다(_파이프로 흘려보낸다_ 고 합니다).
예를 들면:

```
hacker@dojo:~$ echo no-no | grep yes
hacker@dojo:~$ echo yes-yes | grep yes
yes-yes
hacker@dojo:~$ echo yes-yes | grep no
hacker@dojo:~$ echo no-no | grep no
no-no
```

이제 직접 해보세요! `/challenge/run`은 플래그를 포함해 십만 줄의 텍스트를 내보냅니다.
`grep`으로 플래그를 찾으세요!
