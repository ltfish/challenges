이제 파일은 만들 수 있습니다.
디렉터리는 어떨까요?
`mkdir` 명령어로 **m**a**k**e **dir**ectory, 즉 디렉터리를 만듭니다.
그리고 그 안에 파일을 넣을 수 있죠!

보세요:

```console
hacker@dojo:~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ mkdir my_directory
hacker@dojo:/tmp$ ls
my_directory
hacker@dojo:/tmp$ cd my_directory
hacker@dojo:/tmp/my_directory$ touch my_file
hacker@dojo:/tmp/my_directory$ ls
my_file
hacker@dojo:/tmp/my_directory$ ls /tmp/my_directory/my_file
/tmp/my_directory/my_file
hacker@dojo:/tmp/my_directory$
```

자, 이제 `/tmp/pwn` 디렉터리를 만들고 그 안에 `college` 파일을 만들어 보세요!
그런 다음 `/challenge/run`을 실행하면 풀이를 확인하고 플래그를 줍니다!
