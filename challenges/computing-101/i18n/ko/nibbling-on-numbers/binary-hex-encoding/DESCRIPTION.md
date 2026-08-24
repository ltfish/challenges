위에서 읽은 것을 실제로 써볼 시간입니다.

핵심은 이것입니다. 16진수 한 자리는 정확히 4비트이므로, 8비트인 한 바이트는 16진수 두 자리입니다.
어떤 바이트를 2진수에서 16진수로 바꾸려면, 8비트를 4비트씩 두 묶음으로 나누고 각 묶음을 표에서 찾으면 됩니다:

```
11100011     the byte, in binary
1110 0011    the byte, in binary, split into two groups of 4 bits
 e    3      each group of 4 bits -> one hex digit
->  0xe3     the hex!
```

`/challenge/convert`를 실행해서 플래그를 얻으세요!
