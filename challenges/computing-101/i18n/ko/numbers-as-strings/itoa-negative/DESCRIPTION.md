여러분의 `itoa`는 음이 아닌 수를 처리합니다.
하지만 합은 음수일 수 있고(어쨌든 여러분의 `atoi`는 음수를 읽으니까요), 음수는 앞에 `-`를 붙여 적습니다.

요령은 부호를 먼저 떼어내고, 이미 해둔 일이 나머지를 처리하게 두는 것입니다:

- 입력 값이 음수면 `'-'`를 쓰고, 버퍼 포인터를 그 뒤로 한 칸 옮기고(예: `add rsi, 1`), 입력 값을 `neg`해서 크기를 얻습니다.
- `cmp rdi, 0`으로 비교하고 `jl is_negative`를 쓸 수 있습니다(`jl`은 앞서 비교한 왼쪽 값이 오른쪽보다 부호 있는 값으로 **l**ess일 때 **j**ump합니다).
- 그 (이제 음이 아닌) 크기에 기존의 숫자 반복문을 돌립니다.
- 전체 길이는 쓴 숫자의 개수에 부호 `1`을 더한 값입니다.

음이 아닌 수에는 부호가 없으므로 앞서와 똑같이 출력됩니다.

`itoa(value, buf)`를 확장해 음수도 처리하게 하세요.
호출 규약은 같습니다. 값 인자는 `rdi`, 버퍼 인자는 `rsi`, 전체 길이는 `rax`로 반환합니다.
`.global itoa`를 잊지 마세요.

앞서처럼 빌드하고 제출하세요:

```console
hacker@dojo:~$ as -o your-solve.o your-solve.s
hacker@dojo:~$ ld -shared -o your-solve.so your-solve.o
hacker@dojo:~$ /challenge/check your-solve.so
```

부호를 처리하고 길이를 반환하세요.
