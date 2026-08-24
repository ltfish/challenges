자, Zardus가 정신을 차렸습니다. 애초에 왜 `.bashrc`를 쓰기 가능하게 두었을까요?
하지만 더 흔한 상황은, 같은 시스템의 사용자들이 협업을 편하게 하려고 자기 홈 디렉터리를 _누구나 쓸 수 있게_ 만드는 것입니다.
여기에 무슨 문제가 있을까요?

문제는 리눅스 파일/디렉터리 권한의 미묘한 점, 즉 디렉터리에 쓰기 권한이 있는 사람은 누구나 그 안의 파일을 _옮기고_ _지울_ 수 있다는 것입니다.
예를 들어 Zardus에게 협업용으로 누구나 쓸 수 있는 디렉터리가 있다고 해봅시다:

```console
zardus@dojo:~$ mkdir /tmp/collab
zardus@dojo:~$ chmod a+w /tmp/collab
zardus@dojo:~$ echo "do pwn.college" > /tmp/collab/todo-list
```

그런데 해커가 나타나서, _todo-list 파일의 소유자가 아닌데도_ 다음과 같이 합니다!

```console
hacker@dojo:~$ ls -l /tmp/collab/todo-list
-rw-r--r-- 1 zardus zardus 15 Jun  6 13:12 /tmp/collab/todo-list
hacker@dojo:~$ rm /tmp/collab/todo-list
rm: remove write-protected regular file '/tmp/collab/todo-list'? y
hacker@dojo:~$ echo "send hacker money" > /tmp/collab/todo-list
hacker@dojo:~$ ls -l /tmp/collab/todo-list
-rw-r--r-- 1 hacker hacker 18 Jun  6 13:12 /tmp/collab/todo-list
hacker@dojo:~$
```

직관에 어긋나 보일 수 있습니다. `hacker`는 `todo-list`에 쓰기 권한이 없는데도 결과적으로 그 내용을 바꿀 수 있으니까요.
하지만 이렇게 생각해 보세요. 파일과 디렉터리의 연결 관계는 결국 그 디렉터리 안에 있으며, 그 디렉터리에 쓰기 권한이 있는 사용자는 그것을 마음대로 주무를 수 있습니다.
당연히 중요한 디렉터리가 누구나 쓸 수 있게 되어 있으면 보안상 문제가 됩니다.

이 챌린지에서 Zardus는 편의를 위해 자기 홈 디렉터리를 열어 두었습니다:

```console
zardus@dojo:~$ chmod a+w /home/zardus
```

알다시피 그 디렉터리에는 _`.bashrc` 같은_ 민감한 파일이 많습니다!
`/home/zardus/.bashrc`가 아니라 `/home/zardus`에 대한 쓰기 권한만으로 앞의 공격을 재현할 수 있을까요?
