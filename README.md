# Setting Up Real-Time PHP Debugging Environment on MacOS  
# MacOS 환경에서 PHP 리얼타임 디버깅 환경 구축  

## Requirements / 준비사항  
1. **Install MAMP / MAMP 설치**  
  - MAMP is a local server environment for running PHP and MySQL on MacOS. Download and install it from the [MAMP official website](https://www.mamp.info/).  
  - After installation, check MAMP's default settings and select the PHP version.  
  - MAMP는 MacOS에서 PHP와 MySQL을 실행할 수 있는 로컬 서버 환경입니다. [MAMP 공식 웹사이트](https://www.mamp.info/)에서 다운로드 및 설치하세요.  
  - 설치 후, MAMP의 기본 설정을 확인하고 PHP 버전을 선택하세요.  

2. **Check and Select PHP Version / PHP 버전 확인 및 선택**  
  - Before setting up the debugging environment, check the PHP version in use.  
  - Download the Xdebug version compatible with the PHP version provided by MAMP.  
  - You can check the PHP version in MAMP's settings or by running `php -v` in the terminal.  
  - 디버깅 환경을 설정하기 전에 사용 중인 PHP 버전을 확인하세요.  
  - Xdebug는 PHP 버전에 따라 호환되는 버전을 설치해야 하므로, MAMP에서 제공하는 PHP 버전과 일치하는 Xdebug를 다운로드하세요.  
  - PHP 버전은 MAMP의 설정 화면 또는 터미널에서 `php -v` 명령어로 확인할 수 있습니다.  
  - 여기에서는 PHP 버전 8.4.1 사용합니다.
  - Here, PHP version 8.4.1 is used.

3. **Install VS Code / VS Code 설치**  
  - Visual Studio Code is a lightweight yet powerful code editor. Download and install it from the [VS Code official website](https://code.visualstudio.com/).  
  - After installation, add extensions required for PHP development, such as `PHP Intelephense` and `PHP Debug`.  
  - Visual Studio Code는 가볍고 강력한 코드 편집기입니다. [VS Code 공식 웹사이트](https://code.visualstudio.com/)에서 다운로드 및 설치하세요.  
  - 설치 후, PHP 개발에 필요한 확장 프로그램을 추가로 설치하세요. 예: `PHP Intelephense`, `PHP Debug`.  

## Debugging Steps / 디버깅 방법  
1. **Install and Configure Xdebug / Xdebug 설치 및 설정**  
  - Install Xdebug for PHP debugging. Download the Xdebug version compatible with the PHP version included in MAMP.  
  - Open the `php.ini` file and add the following configuration:  
  - PHP 디버깅을 위해 Xdebug를 설치합니다. MAMP에 포함된 PHP 버전에 맞는 Xdebug를 다운로드하세요.  
  - `php.ini` 파일을 열어 아래와 같은 설정을 추가합니다:  
  - `/Applications/MAMP/bin/php/php8.4.1/conf` folder contains the `php.ini` file.  
  - `/Applications/MAMP/bin/php/php8.4.1/conf` 폴더에 `php.ini` 파일이 있습니다.  
    ```ini  
    [Xdebug]  
    zend_extension="/Applications/MAMP/bin/php/php8.4.1/lib/php/extensions/no-debug-non-zts-20240924/xdebug.so";  
    xdebug.mode=debug  
    xdebug.start_with_request=yes  
    xdebug.client_host=127.0.0.1  
    xdebug.client_port=9003  
    xdebug.log=/Applications/MAMP/logs/xdebug.log  
    ```  
  - Restart MAMP after making the changes.  
  - 설정 후 MAMP를 재시작합니다.  

2. **Set Up Debugging in VS Code / VS Code에서 디버깅 환경 설정**  
  - Create a `.vscode/launch.json` file in VS Code and add the following content:  
  - VS Code에서 `.vscode/launch.json` 파일을 생성하고 아래 내용을 추가합니다:  
    ```json  
    {  
     "version": "0.2.0",  
     "configurations": [  
      {  
        "name": "Launch Built-in web server",  
        "type": "php",  
        "request": "launch",  
        "runtimeExecutable": "/Applications/MAMP/bin/php/php8.4.1/bin/php",  
        "runtimeArgs": [  
         "-dxdebug.mode=debug",  
         "-dxdebug.start_with_request=yes",  
         "-S",  
         "localhost:9003",  
         "-t",  
         "${workspaceRoot}/html"  
        ],  
        "cwd": "${workspaceRoot}/html",  
        "port": 9003  
      }  
     ]  
    }  
    ```  
  - In the Debug tab, select "Listen for Xdebug" and start debugging.  
  - 디버깅 탭에서 "Listen for Xdebug"를 선택하고 디버깅을 시작합니다.  

3. **Enable Debugging in Browser / 브라우저에서 디버깅 활성화**  
  - To enable debugging in the browser, install a browser extension like Xdebug Helper.  
  - Activate debugging mode in the extension and run the PHP file you want to debug.  
  - 브라우저에서 디버깅을 활성화하려면 Xdebug Helper와 같은 브라우저 확장을 설치하세요.  
  - 확장에서 디버깅 모드를 활성화한 후, 디버깅하려는 PHP 파일을 실행합니다.  

4. **Set Breakpoints and Start Debugging / 중단점 설정 및 디버깅 시작**  
  - Open the PHP file you want to debug in VS Code and set breakpoints.  
  - Run the PHP file in the browser, and debugging will start in VS Code.  
  - VS Code에서 디버깅하려는 PHP 파일을 열고 중단점을 설정합니다.  
  - 브라우저에서 해당 PHP 파일을 실행하면 VS Code에서 디버깅이 시작됩니다.  

## How to Run / 실행 방법  
1. Place the project files in the web server's root directory (e.g., MAMP's `htdocs` folder).  
  - 프로젝트 파일을 웹 서버의 루트 디렉토리(예: MAMP의 `htdocs` 폴더)에 배치하세요.  
2. Open the browser and navigate to `http://localhost:9003/html/index.php`.  
  - 브라우저를 열고 `http://localhost:9003/html/index.php`로 이동하세요.  
3. Check the output and debug as needed.  
  - 출력 결과를 확인하고 필요한 경우 디버깅을 진행하세요.  

## Prerequisites / 요구사항  
- PHP 8.4.1 or higher / PHP 8.4.1 이상  
- Xdebug installed and configured (refer to `php.ini`)  
- Xdebug 설치 및 설정 완료 (`php.ini` 파일 참조)