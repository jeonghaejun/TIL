# git 버전관리

버전 관리 시스템은 파일 변화를 시간에 따라 기록했다가 나중에 특정 시점의 버전을 다시 꺼내올 수 있는 시스템이다. 이 책에서는 버전 관리하는 예제로 소프트웨어 소스 코드만 보여주지만, 실제로 거의 모든 컴퓨터 파일의 버전을 관리할 수 있다. VCS를 사용하면 각 파일을 이전 상태로 되돌릴 수 있고, 프로젝트를 통째로 이전 상태로 되돌릴 수 있고, 시간에 따라 수정 내용을 비교해 볼 수 있고, 누가 문제를 일으켰는지도 추적할 수 있고, 누가 언제 만들어낸 이슈인지도 알 수 있다. VCS를 사용하면 파일을 잃어버리거나 잘못 고쳤을 때도 쉽게 복구할 수 있다. 이런 모든 장점을 큰 노력 없이 이용할 수 있다.



## git로 버전관리하기

* 기본적인 버전관리 파일 흐름
 ![img](https://res.cloudinary.com/practicaldev/image/fetch/s--Si7ksd-d--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://cdn-images-1.medium.com/max/800/1%2AdiRLm1S5hkVoh5qeArND0Q.png)

```
working directory 👉 staging area 👉 repository
```

* working directory

  수정한 파일들

* staging area

  수정한 파일들 중 버전을 만들려고 하는 파일들

* repository

  만들어진 버전

  

## git 기본명령어

### 처음시작 계정 설정

``git config --global user.name "이름" ``

``git config --global user.email "이메일"``

| 명령어                           | 설명                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| `git init`                       | 프로젝트(소스코드가 있는 디렉토리)를 git repo로 만드는 명령어. 소스코드가 저장되어 있는 디렉토리에서 해당 명령어를 실행하여야 한다. |
| `git status`                     |                                                              |
| `git log`                        |                                                              |
| `git add <file/dirname>`         | modified -> staged 로 파일의 상태를 옮긴다.                  |
| `git commit -m "<message>"`      | staging area에서 repository로 이동하는 명령                  |
| `git restore <file/dirname>`     | Working tree 파일을 되돌린다.                                |
| `git restore --staged <file>...` | staging 상태에서 Unstaged 상태로 변경할 수 있다.             |
