이제 파일을 나열하고, 읽고, 만드는 법을 알게 되었습니다.
그런데 파일을 어떻게 *찾을까요*?
`find` 명령어를 씁니다!

`find` 명령어는 검색 조건과 검색 위치를 나타내는 인자를 선택적으로 받습니다.
검색 조건을 지정하지 않으면 `find`는 모든 파일에 매칭됩니다.
검색 위치를 지정하지 않으면 `find`는 현재 작업 디렉터리(`.`)를 씁니다.
예를 들면:

```console
hacker@dojo:~$ mkdir my_directory
hacker@dojo:~$ mkdir my_directory/my_subdirectory
hacker@dojo:~$ touch my_directory/my_file
hacker@dojo:~$ touch my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find
.
./my_directory
./my_directory/my_subdirectory
./my_directory/my_subdirectory/my_subfile
./my_directory/my_file
hacker@dojo:~$
```

검색 위치를 지정하면 이렇습니다:

```console
hacker@dojo:~$ find my_directory/my_subdirectory
my_directory/my_subdirectory
my_directory/my_subdirectory/my_subfile
hacker@dojo:~$
```

물론 조건도 지정할 수 있습니다!
예를 들어 이름으로 걸러보면:

```console
hacker@dojo:~$ find -name my_subfile
./my_directory/my_subdirectory/my_subfile
hacker@dojo:~$ find -name my_subdirectory
./my_directory/my_subdirectory
hacker@dojo:~$
```

원한다면 파일 시스템 전체를 뒤질 수도 있습니다!

```console
hacker@dojo:~$ find / -name hacker
/home/hacker
hacker@dojo:~$
```

이제 여러분 차례입니다.
파일 시스템의 어느 무작위 디렉터리에 플래그를 숨겨 두었습니다.
이름은 여전히 `flag`입니다.
가서 찾아보세요!

몇 가지 참고사항이 있습니다. 먼저, 파일 시스템에는 `flag`라는 이름의 다른 파일들도 있습니다.
처음 열어본 것에 진짜 플래그가 없더라도 당황하지 마세요.
둘째, 파일 시스템에는 일반 사용자가 접근할 수 없는 곳이 많습니다.
그런 곳에서 `find`는 오류를 뱉겠지만 무시해도 됩니다. 거기에는 플래그를 숨겨두지 않았으니까요!
마지막으로, `find`는 시간이 좀 걸릴 수 있으니 인내심을 가지세요!
