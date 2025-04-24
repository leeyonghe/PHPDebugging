# MacOS 환경에서 PHP 리얼타임 디버깅 환경 구축

## 준비사항
1. **MAMP 설치**  
    - MAMP는 MacOS에서 PHP와 MySQL을 실행할 수 있는 로컬 서버 환경입니다. [MAMP 공식 웹사이트](https://www.mamp.info/)에서 다운로드 및 설치하세요.
    - 설치 후, MAMP의 기본 설정을 확인하고 PHP 버전을 선택하세요.

2. **VS Code 설치**  
    - Visual Studio Code는 가볍고 강력한 코드 편집기입니다. [VS Code 공식 웹사이트](https://code.visualstudio.com/)에서 다운로드 및 설치하세요.
    - 설치 후, PHP 개발에 필요한 확장 프로그램을 추가로 설치하세요. 예: `PHP Intelephense`, `PHP Debug`.

## 디버깅 방법
1. **Xdebug 설치 및 설정**  
    - PHP 디버깅을 위해 Xdebug를 설치합니다. MAMP에 포함된 PHP 버전에 맞는 Xdebug를 다운로드하세요.
    - `php.ini` 파일을 열어 아래와 같은 설정을 추가합니다:
      ```ini
      [Xdebug]
      zend_extension="/path/to/xdebug.so"
      xdebug.mode=debug
      xdebug.start_with_request=yes
      xdebug.client_host=127.0.0.1
      xdebug.client_port=9003
      ```
    - 설정 후 MAMP를 재시작합니다.

2. **VS Code에서 디버깅 환경 설정**  
    - VS Code에서 디버깅을 위해 `.vscode/launch.json` 파일을 생성하고 아래 내용을 추가합니다:
      ```json
      {
         "version": "0.2.0",
         "configurations": [
            {
              "name": "Listen for Xdebug",
              "type": "php",
              "request": "launch",
              "port": 9003
            }
         ]
      }
      ```
    - 디버깅 탭에서 "Listen for Xdebug"를 선택하고 디버깅을 시작합니다.

3. **브라우저에서 디버깅 활성화**  
    - 브라우저에서 디버깅을 활성화하려면 Xdebug Helper와 같은 브라우저 확장을 설치하세요.
    - 확장에서 디버깅 모드를 활성화한 후, 디버깅하려는 PHP 파일을 실행합니다.

4. **중단점 설정 및 디버깅 시작**  
    - VS Code에서 디버깅하려는 PHP 파일을 열고 중단점을 설정합니다.
    - 브라우저에서 해당 PHP 파일을 실행하면 VS Code에서 디버깅이 시작됩니다.

이제 MacOS에서 PHP 리얼타임 디버깅 환경이 준비되었습니다!