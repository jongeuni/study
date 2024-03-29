## Git-flow

깃 플로우는 우리가 브랜치를 쉽계 운영할 수 있도록 하는 사례를 의미한다.

<br>

브랜치 종류로는 

**master	develop	feature	hotfixes	release**

가 있다.

<br>

일단 **master** 브랜치는 언제나 실행 가능한 상태를 유지해야 한다. **master** 브랜치의 가장 최신 버전은 언제나 실행 가능한 상태여야 한다. 실행 가능한 상태를 만드는 과정은 **develop** 브랜치에 진행한다.

출시를 준비하는 브랜치는 **release** 브랜치이다. **release** 브랜치의 이름은 뒤에 버전명을 붙여서 생성한다. (relase0.2) 만약 **release** 브랜치에서 수정할 게 있다면 **release** 브랜치에서 수정한다. 수정하면서 충돌 방지를 위하여 계속 **develop** 브랜치와 병합해준다. 이런 과정을 거치면서 **release** 준비가 다 끝난다. 최종적으로 잘 작동하는 것을 확인했다면 그것을 **master** 브랜치로 병합한다.

일반적인 병합을 사용하는 게 아니라 머지 커밋을 남기는 병합을 사용한다. `git merge --no-ff release/02` 머지를 할 때 fast-forward를 하지 말라는 뜻이다. 커밋 메세지를 의도적으로 만든다.

이렇게 머지(병합)을 다 한 후에는 `git branch -d release/0.2` 이런식으로 **release**0.2 브랜치를 삭제해도 된다. 출시 할 때는 출시할 버전을 기록해놓아야 하기 때문에 **master** 브랜치에 tag를 등록한다. `git tag 0.2` (0.2 버전이 출시되었다.) 이렇게 태그를 등록하면 언제라도 0.2 버전 상태로 되돌릴 수 있다.

<br>

신규로 추가할 기능이 두 개 있다. 하나는 금방 개발되고 (short) 하나는 개발 기간이 오래 (long) 걸린다. 오래 지속되는 개발때문에 릴리즈가 미루어지면 안 된다. **develop**에서 **feature** 브랜치를 만든다. (feature/short, feature/long) 기능이 개발된다면 **develop**에서 머지한다. 역시 `--no-ff`를 사용한다. 그리고 기존에 있었던 **feature** 브랜치를 삭제한다. (feature/short) 그 후release/1.0을 만들어 릴리즈 작업을 시작한다. 역시 릴리즈 과정에서 생기는 자잘한 문제들은 **release** 브랜치에서 고친다. 모든 작업을 마쳤다면 **master**과 **develop**에서 머지한다. (`--no-ff`, master에서는 `git tag 1.0`) 그 후 release1.0 브랜치를 삭제한다.

<br>

이렇게 출시를 했는데 갑자기 긴급히 수정해야할 문제가 발견되면 그 때는 바로 다음 버전을 출시해야 한다. 그 때는 **release**가 아니라 **hotfixes**를 사용한다. hotfixes1.1 브랜치를 만들고 (1.1 버전을 위한 hotfixes) **master**과 **develop**에 머지한다. (--no -ff) **master**에서 머지 후 git tag 1.1로 태그를 단 후 **hotfixes** 브랜치를 삭제한다.

<br>

이런식으로 이루어지는 것이 깃 플로우이다.

깃플로우를 하는 과정이 번거럽고 실수가 일어나는 것을 방지하기 위해 소프트웨어의 도움을 받는데, 그 때 사용할 수 있는 도구가 깃 플로우라는 도구이다.
