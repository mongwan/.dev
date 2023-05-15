---
title: "윈도우 재설치하고 설치한 것들"
date: "2023-05-15T16:50:18.000Z"
---

> 사용하던 노트북에 어느날부터 갑자기 이상한 텍스트가 입력되고, 트랙패드도 간헐적으로 멈추는 증상이 나타났다. 드라이버 충돌인지, 바이러스인지는 모르겠지만 찾아서 해결하기 귀찮아 그냥 포맷해버렸다. 포맷하고 다시 개발환경 설정하려니까 한번 메모해두면 좋을 것 같아서 메모

## 개발 관련 프로그램
이것저것 설치했는데, 개발 관련해서는 요즘 쓰는 환경만 설치했다.
- Anaconda
- Docker Desktop
- VS Code
- Microsoft Visual C++ 2010~2022 Redistributable
- WSL
    - Ubuntu 20.04
- [D2 Coding](https://github.com/naver/d2codingfont)
- ~~PowerToys~~

## iCloud 설치 오류
암호 관리자로 iCloud를 사용하고 있어서 Windows 환경에서도 iCloud를 우선적으로 설치해야 해서, 가장 먼저 Windows Store에서 iCloud를 설치하려고 했다. 근데 msvcp140.dll이 없어 설치가 안된다는 에러가 떴다. 검색해보니 Visual C++ 런타임이 없어 그런거 같아, 설치했는데 또 몇 개는 설치가 안되어 계속 에러가 떴다.  

[이 글](https://www.autodesk.co.kr/support/technical/article/caas/sfdcarticles/sfdcarticles/KOR/How-to-remove-and-reinstall-Microsoft-Visual-C-Runtime-Libraries.html)을 참고해서, 설치되어 있던 모든 버전을 제거하고, [여기](https://learn.microsoft.com/ko-kr/cpp/windows/latest-supported-vc-redist)에서 전체 Visual C++ 런타임을 하나씩 다 설치했더니 해결되었다.

## WSL 2 설정
Windows 10을 사용중이라, 재설치했더니 WSL이 1 버전으로 다운그레이드되었다.  
1. 우선 Windows 버전을 최신 버전으로 업데이트
2. Powershell에서 `wsl --update` 로 업데이트
3. `wsl --set-default-version 2` 설정
4. `wsl --list --verbose`로 설치된 리눅스 확인
5. `wsl --set-version Ubuntu-20.04 2` WSL2로 변환  
내가 설치했던 우분투는 20.04 버전이라 이 커맨드로 WSL2로 변환했다. 미리 `--set-default-version` 해두면 굳이 변환할 필요가 없다.

## zsh 설정
그냥 기본 환경에 깔려 있는 bash를 사용해도 되지만.. 안 예쁘기도 하고 다른 장치랑 비슷하게 하려고 zsh와 oh-my-zsh를 설치했다.  
1. zsh 설치 `sudo apt install zsh`
2. oh-my-zsh 설치 `sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`
3. 테마 설정 `code .zshrc`

### .zshrc 파일에 추가한 것들:
- `ZSH_THEME="agnoster"`
- `plugins=(git zsh-autosuggestions)`
- `alias zshconfig="code ~/.zshrc"`
- `alias ohmyzsh="code ~/.oh-my-zsh"`
- `alias we="explorer.exe ."`  
we로 `explorer.exe .`를 설정해두면, 해당 폴더를 바로 Windows 탐색기에서 열수 있어 편리하다.  
Windows Terminal이나 VS Code 설정이 동기화가 되어서 폰트 깨짐 이슈 같은 건 발생을 안했는데, 나타나면 폰트 변경해서 해결할 수 있다.

## SSH key 설정
GitHub 키를 SSH로 사용하고 있어서, WSL 환경에서 SSH 키를 설정해야 했다. [이 글](https://docs.github.com/ko/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)을 참고해서 ssh 키를 생성하고 추가했다.

1. `ssh-keygen -t ed25519 -C "{내 메일}"`
2. `ssh-add ~/.ssh/id_ed25519`
3. `code ~/.ssh/id_ed25519.pub`으로 공개키 확인 후 복사
4. [Github 설정](https://github.com/settings/keys)에 붙여넣고 추가
---

## References
더 늘어날 수도 있는데, 일단은 생각나는게 더 없어 여기서 마무리
- https://www.autodesk.co.kr/support/technical/article/caas/sfdcarticles/sfdcarticles/KOR/How-to-remove-and-reinstall-Microsoft-Visual-C-Runtime-Libraries.html
- https://learn.microsoft.com/ko-kr/cpp/windows/latest-supported-vc-redist
- https://hacktiming.tistory.com/15
- https://docs.github.com/ko/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
- https://zeddios.tistory.com/1207
