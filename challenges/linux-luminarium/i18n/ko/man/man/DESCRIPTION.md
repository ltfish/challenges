이 레벨에서는 `man` 명령어를 소개합니다.
`man`은 `manual`의 줄임말이며, 인자로 넘긴 명령어의 매뉴얼이 있다면 그것을 보여줍니다.
예를 들어 `yes` 명령어에 대해 알아보고 싶다고 해봅시다(_네_, 진짜 있는 명령어입니다):

```console
hacker@dojo:~$ man yes
```

이렇게 하면 `yes`의 매뉴얼 페이지가 나오는데, 대략 이런 모습입니다:

```text
YES(1)                           User Commands                          YES(1)

NAME
       yes - output a string repeatedly until killed

SYNOPSIS
       yes [STRING]...
       yes OPTION

DESCRIPTION
       Repeatedly output a line with all specified STRING(s), or 'y'.

       --help display this help and exit

       --version
              output version information and exit

AUTHOR
       Written by David MacKenzie.

REPORTING BUGS
       GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
       Report any translation bugs to <https://translationproject.org/team/>

COPYRIGHT
       Copyright  ©  2020  Free Software Foundation, Inc.  License GPLv3+: GNU
       GPL version 3 or later <https://gnu.org/licenses/gpl.html>.
       This is free software: you are free  to  change  and  redistribute  it.
       There is NO WARRANTY, to the extent permitted by law.

SEE ALSO
       Full documentation <https://www.gnu.org/software/coreutils/yes>
       or available locally via: info '(coreutils) yes invocation'

GNU coreutils 8.32               February 2022                          YES(1)
```

중요한 절들은 다음과 같습니다:

```text
NAME(1)                           CATEGORY                          NAME(1)

NAME
	This gives the name (and short description) of the command or
	concept discussed by the page.

SYNOPSIS
	This gives a short usage synopsis. These synopses have a standard
	format. Typically, each line is a different valid invocation of the
	command, and the lines can be read as:

	COMMAND [OPTIONAL_ARGUMENT] SINGLE_MANDATORY_ARGUMENT
	COMMAND [OPTIONAL_ARGUMENT] MULTIPLE_ARGUMENTS...

DESCRIPTION
	Details of the command or concept, with detailed descriptions
	of the various options.

SEE ALSO
	Other man pages or online resources that might be useful.

COLLECTION                        DATE                          NAME(1)
```

매뉴얼 페이지는 화살표 키와 PgUp/PgDn으로 스크롤할 수 있습니다.
다 읽었으면 `q`를 눌러 빠져나올 수 있습니다.

매뉴얼 페이지는 중앙 데이터베이스에 저장됩니다.
궁금하다면, 이 데이터베이스는 `/usr/share/man` 디렉터리에 있습니다. 하지만 직접 만질 일은 없고, `man` 명령어로 질의하기만 하면 됩니다.
`man` 명령어의 인자는 파일 경로가 아니라 항목의 이름 그 자체입니다(예를 들어 `yes` man 페이지를 보려면 `man yes`를 실행하며, `yes` 프로그램의 실제 경로인 `man /usr/bin/yes`를 쓰면 `man`이 깨진 내용을 보여줍니다).

이 레벨의 챌린지에는 비밀 옵션이 있는데, 그 옵션을 쓰면 챌린지가 플래그를 출력합니다.
`challenge`의 man 페이지를 통해 그 옵션을 알아내야 합니다!
