계속 발전하는 파일 형식을 다루는 프로그램은, 어떤 버전의 형식을 파싱해야 하는지 알 수 있어야 합니다.
이 정보는 흔히 매직 넘버 바로 근처에 저장됩니다.
이 `/challenge/cimg`에 올바른 cIMG 버전을 어떻게 넘길지 알아내세요!

----
**바이너리 데이터 쓰기:**
이 레벨에서는 _키보드로 입력할 수 없는_ 문자가 들어간 파일을 만들어야 한다는 것을 알게 될 것입니다.
방법은 여러 가지지만, 그중 하나는 파일을 만들어 주는 Python 스크립트를 작성하는 것입니다.

먼저 쓰려는 파일을 엽니다.

```python
with open("my-file", "wb") as out_file:
```

위의 `"wb"`는 "my-file" 파일을 원시 바이트 쓰기 모드로 열라고 Python에 알려줍니다.
이렇게 하면 거기에 쓸 수 있습니다.
물론 평범한 파일 쓰기에는 익숙하시겠죠:

```python
with open("my-file", "wb") as out_file:
    out_file.write(b"HELLO WORLD")
```

보다시피 평범하게 입력할 수 있는 문자는 그냥 Python 바이트열에 넣어 파일로 보내면 됩니다.
그 밖의 문자는 어떨까요?
Python 바이트열에서 이미 보았을 수도 있는데, `\x` "이스케이프 시퀀스"로 문자를 원시 바이트 값으로 지정할 수 있습니다.
예를 들어 \x41은 16진수 값 0x41인 바이트를 만들며, 이는 ASCII의 A입니다.
먼저 이것으로 위의 내용을 다른 방식으로 써봅시다:

```python
with open("my-file", "wb") as out_file:
  out_file.write(b"HELLO \x57\x4f\x52\x4c\x44")
```

이것도 파일에 `HELLO WORLD`를 씁니다!
이스케이프 시퀀스는 Python이 여러분의 코드를 실행하며 바이트열을 만들 때 해석합니다.

다른 값으로 평소에는 입력할 수 없는 문자를 만들 수 있습니다.
예를 들어 여기서는 `HELLO WORLD` 뒤에 널 바이트(값 0)를 넣습니다:

```python
with open("my-file", "wb") as out_file:
  out_file.write(b"HELLO \x57\x4f\x52\x4c\x44\x00")
```

널 바이트는 많은 바이너리 형식과 프로토콜에서 쓰이며, 입력하기 어려운 값을 가진 다른 바이트들도 마찬가지입니다.
자주 쓰이는 몇몇에는 줄여 쓸 수 있는 다른 "이스케이프 시퀀스"가 있습니다.
몇 가지 예시입니다:

```python
assert b"\0" == b"\x00" # our null byte
assert b"\n" == b"\x0a" # a newline
```

또한 Python의 문법 자체와 충돌하는 문자도 "이스케이프"해야 합니다.
예를 들어 다음은 `HELLO "WORLD"!`를 출력합니다:

```python
with open("my-file", "wb") as out_file:
  out_file.write(b"HELLO \"WORLD\"!")
```

Python이 바이트열의 끝으로 해석하지 않도록 위의 큰따옴표는 이스케이프해야 합니다!

----
**정수 값 쓰기:**
물론 파일 형식의 어떤 바이트는 정수를 나타내며, 보통 리틀 엔디언 형식으로 저장됩니다.
이런 값을 쓰려면 보통의 정수(예: `5`)를 그 이진 표현으로 "패킹"해야 합니다(이는 변수의 크기에 따라 다릅니다. 예를 들어 32비트/4바이트 `1`은 `b"\x05\x00\x00\x00`이 됩니다).

정수와 원시 바이트 사이를 오가려면 Python의 `struct` 패키지를 살펴보세요.

```python
with open("my-file", "wb") as out_file:
  # this packs the integer 1337 (0x539 in hex) into four little-endian bytes
  out_file.write(struct.pack("<I", 1337))

  # the above is equivalent to
  out_file.write(b"\x39\x05\x00\x00")

  # this packs the integer 1337 (0x539 in hex) two little-endian bytes
  out_file.write(struct.pack("<H", 1337))

  # the above is equivalent to
  out_file.write(b"\x39\x05")
```

궁금하다면 [struct 문서](https://docs.python.org/3/library/struct.html#format-characters)에서 다른 형식 지정자도 살펴보세요.
