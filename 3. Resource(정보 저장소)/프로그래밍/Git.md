![[첨부 파일 소스/Image File 1/Pasted image 20241016151011.png]]
![[Pasted image 20241016155801.png]]

**vscode terminal**
Crtl + j 또는 Crtl + 백틱 으로 터미널 창 열고 닫기 가능

**기본 명령어**
`git init` : 깃 생성
`git status` : 깃에 있는 파일 확인
`git log` : 커밋 로그 확인
	`git log --all --oneline` 으로 변경사항마다 한 줄로 간단하게 확인 가능
`git add` : 파일 깃에 추가 (스테이징)
`git commit` : 커밋
- `-a(add)`, `-m(message)` 를 뒤에 붙여서 한번에 작업 가능
`git checkout \<commit-hash>` : 해당 해쉬의 커밋으로 되돌아감
`git difftool` : 파일의 변경사항을 시각적으로 확인 가능
	`git difftool (커밋ID)` : 해당 커밋의 변경 사항을 확인 가능
	(커밋2개 입력 시 커밋 2개간의 차이점 확인 가능)

**git brench**
- nuke의 노드 트리처럼 원본을 토대로 새로 작업할 수 있는 작업공간.
- `git brench` (브랜치 이름) : brench 생성
- `git checkout` (브랜치 이름) : brench 전환
- `git merge`
	- git checkout <목표 브랜치>
	- git merge <소스 브랜치>
	- 위 문장을 통해서 목표 브랜치로 소스 브랜치의 데이터를 가져올 수 있다. 

**커밋 업데이트 하기**
**git push -u origin main** : 로컬과 원격 저장소연결
- `git push -u origin main`  Git에서 원격 저장소로 변경 사항을 푸시하는 명령
- `git push`: 로컬 저장소의 변경 사항을 원격 저장소로 푸시
- `-u`: "upstream"을 의미하며, 로컬 브랜치와 원격 브랜치 간의 연결을 자동으로 설정.
- `origin`: 원격 저장소의 이름으로, 보통 Git에서 원격 저장소에 대한 별칭으로 설정. 원격 저장소의 URL과 별칭이 연결되어 있습니다.
- `main`: 로컬 저장소에서 푸시할 브랜치 이름. 원격 저장소에 해당 브랜치로 변경 사항 푸시.
- 따라서 `git push -u origin main` 명령은 로컬의 `main` 브랜치에서 변경 사항을 `origin`이라는 원격 저장소의 `main` 브랜치로 푸시하면서, 두 브랜치 간의 연결을 설정하는 역할을 합니다. 이후에는 `-u` 옵션 없이 `git push` 명령만으로 변경 사항을 푸시할 수 있게 됩니다.

**git remote -v**
- 로컬 저장소에 설정된 모든 원격 저장소 보여줌.
**git push** : 로컬내용을 원격으로 업데이트. 로컬 -> 원격
**git pull** : 원격 내용을 로컬로 업데이트. 원격 -> 로컬

**git 생성 과정**
홈페이지에서 repository 생성

git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin <URL.git>
git push -u origin main

**github pages 설정**
1. git에 repository연결
2. ![[첨부 파일 소스/Image File 1/Pasted image 20240324204348.png]]Packagage.json 마지막에 "homepage추가"
3. ![[첨부 파일 소스/Image File 1/Pasted image 20240324204440.png]]script에 위 코드 추가
   터미널에서 "npm run deploy" 하면 npm run build 실행고고
   gh pages가 "homepage" 주소에 build파일 업로드


**Git 개념**
깃은 버전 관리를 도와주는 시스템이다. 깃 허브는 원격 저장소의 기능을 할 뿐이다.

**용어**
**Repository** :저장소. git은 원격 저장소와 로컬 저장수 두 종류의 저장소 제공
**원격 저장소(Remote repo)** : 파일이 원격 저장소 전용 서버에서 관리되며 여러 사람이 함께 공유하기 위한 저장소다.
**로컬 저장소(Local repo)** : 내 PC에 파일이 저장되는 개인 전용 저장소.
**Wroking Directory** : 저장소를 어느 한 시점을 바라보는 작업자의 현재 시점.
**SnapShot** : 특정 시점에서 파일, 폴더 또는 워크스페이스의 상태를 의미. 스냅샷을 통해 특정 시점에 어떤 파일에 어떤 내용이 기록되어 있었는지, 폴더 구조는 어땠는지 등 저장소의 모든 정보를 확인할 수 있다.
Git에서는 새로운 버전을 기록하기 위한 명령인 커밋을 실행하면 스냅샷이 저장된다.
**Checkout** : 이전 버전 작업을 불러오는 것.
**Head** : 현재 작업중인 Branch
**Branch** : 가지 또는 **분기점**을 의미하며, 작업을 할때에 현재 상태를 복사하여 
Branch에서 작업을 한 후에 완전하다 싶을때 Merge를 하여 작업을 한다.
Branch는 로컬에서 독립적으로 관리되고, 원격 저장소에 push하거나 원격 저장소로부터 pull할 때 **동기화(원격 저장소와 로컬 저장의 상태를 일치시키는 동작)** 된다.

==**VIM에디터**==
rebase를 통해 열리는 창 조작 방법.
`i`를 눌러서 앞에 문자를 수정할 수 있다.
`ESC`를 누른 뒤 `:wq`를 통해 저장 후 종료할 수 있다.


![[첨부 파일 소스/Image File 1/Pasted image 20240422233338.png]]
**<깃의 저장소 구성>**

working directory에서 작업 후 add하면 Index로이동하게 되고, commit하면 Local repo로 이동한다. 마지막으로 push를 진행하면 Remote repo로 파일이 이동한다.


## 개념2
git은 기본적으로 로컬 파일의 버전 관리를 도와주는 프로그램이다. 로컬에서 버전을 저장하고 브랜치를 관리하는 등 다양한 작업을 할 수 있다. 이를 원격에 파일을 저장하고 협업을 도와주게 할 수 있는 저장소가 github와 같은 것이다.

기본적으로 로컬에서 작업을 하고 원격 저장소와는 데이터를 주고 받는 작업들을 한다.
origin/main은 원격 저장소의 브랜치를 가리키고, 로컬에서는 기본적으로 main과 연결되어있으며 `git checkout -u branch origin/main`으로 연결하고 있는 브랜치를 변경할 수 있다.

`git pull` : 원격에서 데이터를 내려받기만 하는 git fetch와 달리 fetch와 merge를 같이 실행해주는 작업이 pull이다. 이를 merge 대신 커밋 트리를 깔끔하게 하기 위해 rebase를 사용하려면 pull 뒤에 `-- rebase`를 추가하면 merge 대신 rebase를 해준다.


## 프로그래밍 요구 사항 1

- Node.js 20.17.0 버전에서 실행 가능해야 한다.
- 프로그램 실행의 시작점은 `App.js`의 `run()`이다.
- `package.json` 파일은 변경할 수 없으며, **제공된 라이브러리와 스타일 라이브러리 이외의 외부 라이브러리는 사용하지 않는다.**
- 프로그램 종료 시 `process.exit()`를 호출하지 않는다.
- 프로그래밍 요구 사항에서 달리 명시하지 않는 한 파일, 패키지 등의 이름을 바꾸거나 이동하지 않는다.
- 자바스크립트 코드 컨벤션을 지키면서 프로그래밍한다.
    - 기본적으로 [JavaScript Style Guide](https://github.com/woowacourse/woowacourse-docs/tree/main/styleguide/javascript)를 원칙으로 한다.

## 프로그래밍 요구 사항 2

- indent(인덴트, 들여쓰기) depth를 3이 넘지 않도록 구현한다. 2까지만 허용한다.
    - 예를 들어 while문 안에 if문이 있으면 들여쓰기는 2이다.
    - 힌트: indent(인덴트, 들여쓰기) depth를 줄이는 좋은 방법은 함수(또는 메서드)를 분리하면 된다.
- 3항 연산자를 쓰지 않는다.
- 함수(또는 메서드)가 한 가지 일만 하도록 최대한 작게 만들어라.
- Jest를 이용하여 정리한 기능 목록이 정상적으로 작동하는지 테스트 코드로 확인한다.
    - 테스트 도구 사용법이 익숙하지 않다면 아래 문서를 참고하여 학습한 후 테스트를 구현한다.
        - [Using Matchers](https://jestjs.io/docs/using-matchers)
        - [Testing Asynchronous Code](https://jestjs.io/docs/asynchronous)
        - [Jest로 파라미터화 테스트하기: test.each(), describe.each()](https://www.daleseo.com/jest-each)

## 프로그래밍 요구 사항 3

- 함수(또는 메서드)의 길이가 15라인을 넘어가지 않도록 구현한다.
    - 함수(또는 메서드)가 한 가지 일만 잘 하도록 구현한다.
- else를 지양한다.
    - 때로는 if/else, when문을 사용하는 것이 더 깔끔해 보일 수 있다. 어느 경우에 쓰는 것이 적절할지 스스로 고민해 본다.
    - 힌트: if 조건절에서 값을 return하는 방식으로 구현하면 else를 사용하지 않아도 된다.
- 구현한 기능에 대한 단위 테스트를 작성한다. 단, UI(System.out, System.in, Scanner) 로직은 제외한다.
    - 단위 테스트 작성이 익숙하지 않다면 `LottoTest`를 참고하여 학습한 후 테스트를 작성한다