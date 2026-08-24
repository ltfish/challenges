솔깃하겠지만, 커맨드 라인에 입력할 양을 줄이려고 `*`를 쓰다 보면 실수를 하게 됩니다.
글로브가 의도하지 않은 파일까지 펼쳐질 수 있고, `rm` 명령이 이미 실행된 뒤에야 그것을 알아챌 수도 있습니다!
이런 종류의 실수에서 자유로운 사람은 아무도 없습니다.

특정 대상을 지정하려 할 때 더 안전한 대안은 _탭 자동완성_ 입니다.
셸에서 탭을 누르면, 여러분이 무엇을 입력하려는지 추측해서 자동으로 완성해 줍니다.
자동완성은 아주 유용하며, 이 챌린지에서는 파일을 지정할 때 그것을 어떻게 쓰는지 살펴봅니다.

이 챌린지는 플래그를 `/challenge/pwncollege`로 복사해 두었고, 그 파일은 자유롭게 `cat`할 수 있습니다.
하지만 파일 이름을 직접 입력할 수는 없습니다. 반드시 탭으로 자동완성하도록 꽤나 짓궂은 장치를 해두었거든요.
한번 해보세요!

```console
hacker@dojo:~$ ls /challenge
Dockerfile  pwncollege
hacker@dojo:~$ cat /challenge/pwncollege
cat: /challenge/pwncollege: No such file or directory
hacker@dojo:~$ cat /challenge/pwn<TAB>
pwn.college{HECK YEAH}
hacker@dojo:~$
```

탭 키를 누르면 이름이 펼쳐지고, 그 파일을 읽을 수 있게 됩니다.
행운을 빕니다!
