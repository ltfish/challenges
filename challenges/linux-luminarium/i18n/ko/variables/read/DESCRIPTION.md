사용자(여러분)에게서 입력을 읽는 것부터 시작합시다.
이름 그대로인 `read` 빌트인으로 하며, 입력을 변수로 *읽어* 들입니다!

프롬프트를 지정할 수 있는 `-p` 인자를 쓴 예시입니다(그렇지 않으면 지금 이 글을 읽는 여러분이 아래 예시에서 입력과 출력을 구분하기 어려울 테니까요):

```console
hacker@dojo:~$ read -p "INPUT: " MY_VARIABLE
INPUT: Hello!
hacker@dojo:~$ echo "You entered: $MY_VARIABLE"
You entered: Hello!
```

`read`는 표준 입력에서 데이터를 읽는다는 점을 기억하세요!
위의 첫 `Hello!`는 _출력_ 이 아니라 _입력_ 이었습니다.
이 점을 좀 더 분명히 해봅시다.
아래에서는 각 줄 앞에 그 줄이 사용자의 `INPUT`인지 사용자에게 가는 `OUTPUT`인지 표시했습니다:

```console
 INPUT: hacker@dojo:~$ echo $MY_VARIABLE
OUTPUT:
 INPUT: hacker@dojo:~$ read MY_VARIABLE
 INPUT: Hello!
 INPUT: hacker@dojo:~$ echo "You entered: $MY_VARIABLE"
OUTPUT: You entered: Hello!
```

이 챌린지에서 여러분이 할 일은 `read`로 `PWN` 변수를 `COLLEGE` 값으로 설정하는 것입니다.
행운을 빕니다!
