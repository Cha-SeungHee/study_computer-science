#### Terminal tool
- MAC : iTerm2
- Windows : cmder (Git 내장)

#### iTerm2 설정
- Theme : Agnoster (다른 테마도 가능하나 Agnoster가 블럭 형태 각 directory를 구분/표시해주기 때문에 많이 사용)
- Font : Powerline font 중 하나 다운로드한 뒤에 iTerm2에서 설정 (미설치시 branch 표시 등 깨짐)

#### 각 Commit 구성요소
- hash code (내용 또는 directory 기반) 보유
- message
- author
- date/time

#### Git의 3가지 Local 작업환경
1) Working directory : 파일 수정 directory
- untracked
- tracked (modified/unmodified)
2) Staging area : 수정 완료된 파일들을 저장해두는 공간
3) .git directory (repository) : Git version history에 저장

Checkout을 통해 원하는 버전의 파일을 repository로부터 working directory로 이동 가능

PC 문제 생길 시 history를 잃어버릴 수 있기 때문에 remote 서버에 push
