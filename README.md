## Git

git은 로컬에서 사용하는 버전 관리 시스템으로 브랜치 생성, 브랜치 복구, 삭제 병합 등의 작업이 가능하다. 

하지만 로컬에서 사용되는 프로그램이기 때문에 다른 사람과 실시간으로 작업을 공유할 수 는 없다. 

<br>

## Github

gihub는 git 저장소를 관리하기 위한 클라우드 기반의 호스팅 서비스이다. 그렇기 때문에 다른사람과의 소스코드를 공유할 수도 있고, 클라우드 서버에 소스를 올리기 때문에 다른 사람과의 공동 작업도 가능하다. 

분산 버전 제어, 엑세스 제어, 소스코드 관리, 버그 추적, 기능 요청 및 작업 관리 등의 기능을 제공한다. 

<br>

## Git의 세가지 영역

Git 프로젝트는 깃 디렉터리, 워킹 트리, Staging Area라는 세 가지 영역이 있다. 

- **git 디렉터리**

최초 git init 명령어로 깃 저장소가 생성될 때 .git이라는 이름으로 생성되는데 git 프로젝트의 모든 메타데이터와 객체 데이터베이스가 저장된다.

Clone으로 원격 저장소를 복사해서 가져올 때 이 .git 디렉터리를 만들고 원격 저장소의 모든 데이터를 복사해 가져온다. 

---

- **워킹트리 (워킹 디렉터리)**

git 디렉터리에서 특정 버전을 Checkout 해온 것으로 프로젝트 작업이 진행되는 곳이다. 

---

- **Staging Area**

git 디렉터리에 파일로 존재한다. 

워킹트리에서 작업한 내용이 git 디렉터리에 커밋되기 전에 거쳐가는 공간이다. 

<br>

정리해보면

워킹트리에서 작업을 한다. 

Staging Area에 파일을 stage하여 커밋할 스냅샷을 만든다. 

Staging Area에 있는 파이릉ㄹ 커밋하여 git 저장소에 영구적으로 저장한다.

<br>

## Git 기본 명령어

### git init

로컬 git 저장소 설정.

git init 명령어를 입력한 디렉토리 하위에 .git 디렉토리가 생성 됩니다. 

(.git에는 git과 관련된 정보가 저장되어 있음.)

<br>

### git status

작업 중인 파일 상태 확인 

git status 명령어를 입력하면 Untracked와 Tracked라는 키워드를 볼 수 있다. 

- **Untracked**:  git이 해당 파일을 추적 관리하지 않은 상태로 git이 전혀 관리하지 않고있기 때문에 
파일이 삭제될 경우 복구가 불가능하다.
- **Tracked**: git이 해당 파일을 추적 및 관리하는 상태로 git add 명령어를 통해 Staging Area에 
포함되었거나 Commit을 통해 git 디렉터리에 저장된 파일을 의미한다.

<br>

### git add

변경 사항을 저장하여 Tracked 상태로 변경시킨다. 

```bash
git add [-A] [file name]
```

git add -A 또는 git add . 명령어를 통해 변경된 모든 사항을 add할 수 있고, 

원하는 파일만 add도 가능하다. 

<br>

### git commit

```bash
git commit [ -m <msg> ]
```

add된 변경 사항을 이력에 추가하는 명령어로 -m 옵션으로 이력에 대한 메세지 작성이 가능하다. 

메세지를 여러줄 입력하길 원한다면 git commit 후 여러줄 작성하여 저장한다. 

최근 커밋한 내용을 수정하길 원한다면 —amend 옵션을 이용할 수 있다. 

```bash
git commit --amend -m "내용 입력"
```

<br>

### git rebase

이전 또는 여러 개의 커밋을 수정하고 싶을 때 사용하는 명령어

![rebase 통합](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/f00efd17-24d3-4788-b415-53a91afe02d0/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_1.13.54.png)

rebase 통합

![merge 통합](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cd62fb31-1477-4c89-9e57-25562c134f6d/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_1.20.12.png)

merge 통합

rebase는 브랜치의 기준을 한 커밋에서 다른 커밋으로 변경하여 마치 다른 커밋에서 브랜치를 만든 것처럼 보이게 한다. 

기능 브랜치를 메인 브랜치에 통합하는 방법에는 merge와 rebase 두가지로 나눌 수 있는데 rebase 사용을 선호한다. 

```bash
git switch feature
git rebase main
```

커밋이 공개 리포지토리롤 푸시된 후에는 절대 rebase를 수행해서는 안된다. 
rebase는 이전 커밋을 새 커밋으로 대체하고 프로젝트 기록의 일부가 사라진 것처럼 보이게 하기 때문이다. 

<br>

### git log

이력 확인 명령어

```bash
git log [<options>] [<revision range>] [[--] <path>...]
```

그동안의 로그를 확인할 수 있는 명령어로 다양한 옵션을 조합하여 원하는 형태의 로그를 출력할 수 있다. 

![스크린샷 2022-08-07 오전 12.13.12.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/76178cde-32ab-4ff0-964a-e7037f66ca85/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_12.13.12.png)

깃 저장소를 클론하여 git log를 확인해보면 다른 사람이 작업한 이력까지 모두 확인할 수 있다. 

저장소의 커밋히스토리를 시간순으로 보여주며 커밋의 SHA-1 체크섬, 저자 이름, 저자 이메일, 커밋 날짜, 커밋 메세지를 모두 확인 가능하다. 

몇 가지 옵션을 알아보면

- **—oneline**: 커밋 정보를 한 줄로 표시하여 히스토리를 간결하게 확인 가능
    
    ![스크린샷 2022-08-07 오전 12.20.42.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e87f4dc9-863c-4e5a-b086-b7be8e16f40c/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_12.20.42.png)
    
- **—branches**: 현재 존재하는 각 브랜치별 최신 커밋 확인 옵션
- **—graph**: 현재 브랜치들의 상태를 막대로 나타내는 옵션으로 —branches와 함께 사용해야 작동이 된다. 
                직관적으로 브랜치가 나뉘고 병합된 시점을 명확히 확인할 수 있다.
    
    ![스크린샷 2022-08-07 오전 12.22.21.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/edd91515-62bc-42c1-8a5b-6aa7d7ef312e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_12.22.21.png)
    
- **-p 또는 —patch:** 커밋의 diff 결과를 보여주는 옵션으로 무엇을 커밋했는지 빠르게 조회가 가능하다.
    
    ![스크린샷 2022-08-07 오전 12.24.38.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/8a2a57da-dd76-4f83-a474-8df6dad08486/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_12.24.38.png)
    
- **—stat:** 히스토리의 통계를 보여주는 옵션으로 각 커밋의 통계 정보를 조회할 수 있다.
    
    ![스크린샷 2022-08-07 오전 12.25.42.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/00753106-17d5-4523-adee-102b1f8aec43/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA_2022-08-07_%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB_12.25.42.png)
    
<br>

### git reset

이전 상태로 되돌리는 명령어 (이력 삭제)

```bash
git reset [<commit>] [--soft | --mixed [-N] | --hard | --merge | --keep]
```

특정 커밋까지 이력을 초기화하여 작업했던 내용을 취소할 수 있다. 이력이 지워지므로 조심해서 사용해야 한다. 

- **git reset HEAD [file]:** add한 파일 취소, [file]이 없으면 파일 전체 취소
- **git reset —soft HEAD^:** commit을 취소하고, 해당 파일을 staged 상태로 보존
- **git reset (—mixed) HEAD^:** commit을 취소하고, 해당 파일을 unstaged 상태로 보존
- **git reset —hard HEAD^:** commit을 취소하고, 해당 파일을 unstaged로 워킹 디렉터리에서 삭제
- **git reset {commit id} —hard:** 해당 commit까지 이력을 초기화

<br>

### git revert

이전 상태의 이력을 유지하는 명령어

```bash
git revert <commit>...
```

특정 커밋을 취소하는 새로운 커밋을 만드는 명령어로 다시 원래의 상태로 작업을 이어서하고 다시 커밋하는 방식으로 사용된다. 

ex) 삭제한 커밋을 되돌리려면 git revert {삭제한 commit id} 로 커밋을 취소할 수 있다. 

이전에 삭제되었던 커밋은 다시 생성되고, 새로 생성된 커밋은 삭제되며 revert에 대한 새로운 커밋이 생성된다는 점에 유의해야 한다. 

<br>

## Git Branch

### git switch -c

브랜치 생성 및 이동

```bash
git switch (-c | -C) <new-branch>
```

현재 브랜치를 기준으로 새로운 브랜치를 생성하여 그 브랜치로 이동한다. 

옵션 -c를 이용하면 생성과 동시에 이동을 한꺼번에 할 수 있다. 

‘git switch <생성된 브랜치>’는 단순히 브랜치 이동 명령어로 이전에는 ‘checkout’이라는 명령어를 이용했으나 
checkout 하나의 키워드에 많은 기능이 들어있어 버전이 업그레이드 되면서  switch와 restore가 도입되었다. 

- **switch**: switch branch
- **restore**: restore working tree files

<br>

### git restore

git의 파일 조작을 위한 기능을 지원하는 명령어 

```bash
git restore [file]
```

- **git restore [file]** : 특정 파일 HEAD commit으로 복구
- **git restore —source [commit id] [file]**: 특정 파일을 특정 commit으로 복구
- **git restore —staged [file]** : Staging Area에 올라간 파일을 다시 Unstaging

<br>

### git merge

브랜치 병합 명령어

```bash
git merge [branch name]
```
