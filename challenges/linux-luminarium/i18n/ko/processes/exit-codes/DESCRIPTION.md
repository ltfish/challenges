모든 셸 명령은, 모든 프로그램과 모든 빌트인을 포함해서, 실행이 끝나 종료될 때 _종료 코드(exit code)_ 를 남깁니다.
셸이나 셸 사용자(바로 여러분!)는 이것으로 그 프로세스가 제 역할을 해냈는지 확인할 수 있습니다(물론 그 판단은 애초에 그 프로세스가 무엇을 하기로 되어 있었는지에 달려 있습니다).

가장 최근에 끝난 명령의 종료 코드는 특별한 `?` 변수로 확인할 수 있습니다(값을 읽으려면 앞에 `$`를 붙이는 것을 잊지 마세요!):

```console
hacker@dojo:~$ touch test-file
hacker@dojo:~$ echo $?
0
hacker@dojo:~$ touch /test-file
touch: cannot touch '/test-file': Permission denied
hacker@dojo:~$ echo $?
1
hacker@dojo:~$
```

보다시피 성공한 명령은 보통 `0`을 반환하고, 실패한 명령은 0이 아닌 값을 반환합니다. 대개는 `1`이지만, 특정 실패 유형을 나타내는 오류 코드일 때도 있습니다.

이 챌린지에서는 `/challenge/get-code`가 반환한 종료 코드를 알아낸 다음, 그 코드를 인자로 주어 `/challenge/submit-code`를 실행해야 합니다.
행운을 빕니다!
