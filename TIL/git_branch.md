# branch

## 기본 명령어

* branch 생성

  ````bash
  $ git branch __브랜치 이름__
  ````

* branch 이동

```bash
$ git checkout __브랜치 이름__

```

* branch 생성 및 이동

````bash
$ git checkout -b__브랜치이름__
````

* branch 병합

````bash
(master) $ git merge __브랜치이름__
````

> master 브랜치에 __브랜치이름_ 을 병합

* branch 목록

```bash
$ git branch
* master
  ppt
```



* branch 삭제

````bash
$ git branch -d __브랜치이름__
Deleted branch ppt (was ff03b20)
````





파일이 삭제되고 생성된 것처럼 보이지만 git log  --oneline 들어가보면 .. 

HEAD > 커밋 히스토리상의 위치. 헤드에 정보가 있다. 내가 어디에 있는지를 알려줌. HEAD -> master (마스터에 있는 곳을 보고있군)

즉 브런치를 생성하고, 해드를 옮겨줄 수 있음. 그리고 보여지는 파일은, 내가 그 시점의 스샷을 보여준다고 보면 됨. 그 시점의 사진. 파일이 사라지는 것이 아님. 

git checkout master >> head의 위치를 master로 옮김 

git checkout ppt >> head의 위치를 ppt로 옮김 

git merge ppt >> ppt를 master와 합침 







