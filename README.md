<details> <summary>ENG (English Version)</summary>

## Chapter 5 – Using the Shell

**Section 1: Shell Functions and Types**
- Shell Roles: Acts as an interface between user and Linux kernel, providing command interpreter, programming, and environment-setup functions.
- Command Interpreter: Reads commands or scripts, decides if they are built-ins or external programs, spawns child processes for external commands, and displays a prompt while waiting.
- Programming Feature: Supports shell scripts that automate repeated command sequences using the shell’s own control syntax.
- Environment Setup: Uses initialization files to configure PATH, default permissions, environment variables, and user-specific startup settings at login.
- Bourne Shell (sh): Simple and fast, historically common for admin scripts, but has limited user-friendly features and is often symlinked to bash on modern systems.
- C Shell (csh) and Korn Shell (ksh): C shell adds user conveniences with C-like syntax, while Korn shell maintains Bourne compatibility plus C shell features with better performance.
- Bash Shell (bash): Default Linux shell, Bourne-compatible and includes useful features from C and Korn shells; GPL-licensed and widely known as the standard Linux shell.

**Section 2: Basic Shell Usage**
- Checking and Changing Shell: User’s default login shell is recorded in /etc/passwd; grep can check it, and chsh (with valid paths from /etc/shells or chsh -l) can change it.
- Login Shell vs Subshell: The login shell starts at user login; running another shell from the prompt creates a subshell chain, which ends with Ctrl+d or exit, returning to the parent shell.
- Built-in Commands: Some commands like cd are built into the shell (no separate binary); file shows /usr/bin/cd as a script, whereas typical executables like /usr/bin/pwd are binary files.
- Output Commands: echo outputs strings and variable values; printf supports formatted output using % specifiers and backslash escapes.
- Special Characters Overview: The shell interprets special characters such as *, ?, [], ~, -, |, ;, quotes, backquotes, backslash, and redirection operators before executing commands.
- Globbing (*, ?, []): * matches zero or more characters, ? matches any single character, and [] matches one character from a set or range (often combined with other patterns).
- Directory Shorthands (~, -): ~ refers to the current user’s home directory (or another user with ~user), and - refers to the previous directory in cd operations.
- Command Connectors (;, |): ; runs multiple commands sequentially; | pipes the standard output of the left command into the standard input of the right command.
- Quotes (' ', " "): Single quotes disable all special character interpretation; double quotes disable most but still allow $, `, and \ to retain special meaning.
- Command Substitution (` `): Backquotes execute the enclosed text as a command and substitute the command’s output into the surrounding command line.
- Escape Character (\): A backslash in front of a special character cancels its special effect so it is treated as a literal; also used inside quoted strings when needed.

**Section 3: Redirecting Input and Output**
- Standard Streams: Standard input (keyboard), standard output (screen), and standard error (screen) are associated with file descriptors 0, 1, and 2.
- Redirection Concept: Redirects standard streams to or from files using operators like >, >>, <, and their numbered versions with file descriptors.
- Output Overwrite (>): Redirects standard output to a file, creating it if missing or overwriting it if it exists; typically uses > as shorthand for 1>.
- Output Append (>>): Appends command output to the end of an existing file or creates a new file if it does not exist.
- Error Redirection (2>): Redirects standard error messages to a file using file descriptor 2; cannot omit the “2” when redirecting stderr.
- Redirecting Both Output and Error: Combining > and 2> allows saving normal output and error messages separately or together, depending on syntax used.
- Discarding Errors: Redirecting errors to /dev/null effectively ignores them, since any data written there is discarded and cannot be recovered.

**Section 4: Bash Environment Variables**
- Shell vs Environment Variables: Shell variables exist only in the current shell; environment variables are inherited by subshells and act like global variables across shell levels.
- Naming Conventions: Environment variable names are typically uppercase by convention, while shell variables may use lowercase; both store user, path, and prompt-related data.
- Viewing Variables: set prints both shell and environment variables; env prints only environment variables.
- Printing Specific Variables: echo with a leading $ (e.g., $SHELL) outputs the value of a specific variable.
- Defining Variables: Assignments must have no spaces around “=”; shell variables defined this way are not environment variables until exported.
- Exporting Variables: export converts a shell variable into an environment variable or defines and exports in one step; export -n converts an environment variable back to a local shell variable.
- Unsetting Variables: Removing variables ensures they no longer produce output when referenced, effectively clearing custom settings.

**Section 5: Aliases and History**
- Alias Concept: Aliases create short or customized names for longer commands, command sequences, or frequently used options to improve convenience and safety.
- Viewing Aliases: Running alias with no arguments lists all currently defined aliases; default aliases depend on the system configuration.
- Common Aliases: Examples include l. for ls -d .* (showing dot-prefixed paths) and ll for ls -l; such aliases bundle useful options into single commands.
- Defining and Removing Aliases: Use alias name='command' without spaces around “=” and quote multi-word commands; remove aliases with unalias when they are no longer needed.
- Safe Deletion Example: Wrapping rm in an alias that adds -i forces confirmation before deletion, reducing the risk of accidental data loss.
- Limits of Aliases: Bash aliases do not accept arguments directly; for parameterized behavior, shell functions should be used instead of aliases.

</details>

<details> <summary>KOR (한국어 버전)</summary>

## 5장 – 셸 사용법

**셸의 기능과 종류**
- 셸의 역할: 리눅스 커널과 사용자 사이에서 명령을 해석·전달하는 중재자로, 명령어 해석, 프로그래밍, 사용자 환경 설정 기능을 제공한다.
- 명령어 해석 기능: 사용자가 입력한 명령이나 스크립트를 읽어 내장 명령인지 외부 명령인지 확인하고, 외부 명령이면 자식 프로세스를 생성해 실행한 뒤 다시 프롬프트로 돌아온다.
- 프로그래밍 기능: 셸 스크립트를 통해 여러 명령을 묶어 반복 작업을 자동화할 수 있으며, 제어문·반복문 등의 구문을 제공한다.
- 환경 설정 기능: 초기화 파일을 통해 PATH, 기본 권한, 각종 환경 변수를 설정하고 로그인 시 사용자별 초기 환경을 자동으로 적용한다.
- 본셸(sh): 구조가 단순하고 처리 속도가 빨라 예전부터 시스템 관리용 스크립트에 널리 쓰였으나, 사용자 편의 기능은 부족하며 요즘에는 bash와 심볼릭 링크로 연결된 경우가 많다.
- C셸(csh)·콘셸(ksh): C셸은 C 언어와 유사한 문법과 편의 기능을 제공하고, 콘셸은 본셸과 호환성을 유지하면서 C셸의 장점과 빠른 처리 속도를 겸비한다.
- 배시셸(bash): 본셸과 호환되면서 C셸·콘셸의 편리한 기능을 포함한 GPL 기반 공개 셸로, 대부분 리눅스의 기본 셸로 제공된다.

**셸 기본 사용법과 특수문자**
- 셸 확인·변경: 현재 기본 셸은 /etc/passwd에서 확인할 수 있고, chsh와 /etc/shells에 등록된 경로를 이용해 로그인 셸을 변경할 수 있다.
- 로그인 셸과 서브 셸: 로그인 시 실행되는 기본 셸 외에 프롬프트에서 추가로 셸을 실행하면 서브 셸이 생성되고, exit나 Ctrl+d로 종료하면 이전 셸로 돌아간다.
- 셸 내장 명령: cd처럼 별도 실행 파일 없이 셸 내부에 포함된 명령이 있으며, file 명령을 이용해 일반 실행 파일과 스크립트를 구분할 수 있다.
- 출력 명령: echo는 문자열과 변수 값을 간단히 출력하고, printf는 포맷 문자열과 이스케이프 문자를 사용해 형식을 지정한 출력이 가능하다.
- 특수문자 개요: 셸은 명령 실행 전에 *, ?, [ ], ~, -, |, ;, 작은따옴표·큰따옴표, 백쿼터, 역슬래시, 리다이렉션 기호 등을 해석해 적절한 의미로 변환한다.
- 글로빙(*, ?, [ ]): *(별표)는 0개 이상의 임의 문자열, ?(물음표)는 1글자, [ ]는 괄호 안에 나열된 문자 중 하나 또는 범위를 의미하며, 주로 여러 파일명을 간편하게 지정할 때 사용된다.
- 디렉터리 특수문자(~, -): ~는 자신의 홈 디렉터리(또는 ~사용자ID 형태로 다른 사용자의 홈)를 나타내고, -는 cd 명령에서 바로 직전에 있던 디렉터리를 의미한다.
- 명령 연결(;, |): ;(세미콜론)은 여러 명령을 왼쪽부터 순서대로 실행하고, |(파이프)는 왼쪽 명령의 표준 출력을 오른쪽 명령의 표준 입력으로 전달한다.
- 작은따옴표·큰따옴표: 작은따옴표(' ')는 안에 있는 모든 특수문자를 일반 문자로 만들고, 큰따옴표(" ")는 $, `, \를 제외한 대부분 특수문자의 기능을 막는다.
- 백쿼터(` `): 백쿼터로 감싼 부분을 명령으로 해석해 실행 결과를 문자열로 치환하며, 명령 결과를 다른 명령의 인자로 쓰고 싶을 때 사용한다.
- 역슬래시(\): 특수문자 앞에 붙여 그 문자를 일반 문자처럼 처리하게 만들며, 따옴표 안에서 특정 문자를 탈출시키는 용도로도 사용된다.

**입출력 방향 변경**
- 표준 입출력과 파일 디스크립터: 표준 입력(0), 표준 출력(1), 표준 오류(2)는 기본적으로 키보드와 화면에 연결되어 있으며, 각 스트림은 파일 디스크립터 번호로 관리된다.
- 리다이렉션 개념: >, >>, < 같은 기호를 사용해 표준 입출력 장치를 파일로 바꾸는 작업을 리다이렉션이라고 한다.
- 출력 덮어쓰기(>): > 또는 1>는 표준 출력을 지정한 파일로 보내며, 파일이 없으면 새로 만들고 있으면 기존 내용을 지우고 새 출력으로 덮어쓴다.
- 출력 추가하기(>>): >>는 파일이 없으면 새로 만들고, 있으면 파일 끝에 출력 결과를 이어 붙인다.
- 오류 리다이렉션(2>): 2>는 표준 오류(2번 파일 디스크립터)를 파일로 보내므로, 일반 출력과는 별도로 오류 메시지를 따로 저장할 수 있다.
- 출력·오류 동시 리다이렉션: >와 2>를 함께 사용하면 정상 출력과 오류를 각각 또는 동시에 파일로 저장할 수 있으며, 로그 관리에 유용하다.
- 오류 버리기: /dev/null로 리다이렉션하면 해당 스트림의 출력은 모두 버려지며, 불필요한 오류 메시지를 무시하고 싶을 때 사용된다.

**배시셸 환경 변수**
- 셸 변수 vs 환경 변수: 셸 변수는 현재 셸에서만 유효한 지역 변수이고, 환경 변수는 서브 셸에도 전달되는 전역 변수처럼 동작한다.
- 변수 조회: set 명령은 셸 변수와 환경 변수를 모두 출력하고, env는 환경 변수만 출력한다.
- 개별 변수 출력: echo $변수명 형태로 특정 변수의 값을 확인할 수 있으며, 예를 들어 SHELL 변수에는 로그인 셸 경로가 저장되어 있다.
- 변수 설정: 변수명=값 형태로 공백 없이 지정해야 하며, 이렇게 만든 것은 처음에는 셸 변수로만 존재한다.
- 환경 변수로 승격: export 변수명 또는 export 변수명=값 형식으로 셸 변수를 환경 변수로 등록해 서브 셸에도 전달되도록 만들 수 있다.
- 환경 변수 해제·되돌리기: export -n으로 환경 변수 상태를 해제해 셸 변수로 되돌릴 수 있고, 필요 없어진 변수는 완전히 해제해 출력되지 않도록 할 수 있다.

**앨리어스와 히스토리**
- 앨리어스 개념: 자주 쓰는 명령이나 긴 명령어 묶음에 별명을 붙여 짧게 호출할 수 있도록 하는 기능으로, 명령 단축과 실수 방지에 활용된다.
- 앨리어스 조회: 인자 없이 alias를 실행하면 현재 설정된 모든 앨리어스 목록이 출력되며, 기본 제공 항목은 시스템마다 다르다.
- 대표 예시: l.은 ls -d .*처럼 숨김 경로를 보여 주고, ll은 ls -l을 대신 실행하도록 설정된 경우가 많다.
- 설정·삭제 방법: alias 이름='명령' 형식으로 공백 없이 지정하고, 명령 안에 공백이 있을 때는 작은따옴표로 묶어야 하며, 더 이상 쓰지 않을 때는 unalias로 삭제한다.
- 안전한 rm 예시: rm에 -i 옵션을 강제로 붙여 매번 삭제 여부를 확인하게 하는 앨리어스를 설정하면 실수로 파일을 지우는 상황을 줄일 수 있다.
- 인자 전달 한계: 배시셸의 앨리어스는 인자를 직접 전달받아 처리할 수 없으며, 인자를 필요로 하는 복잡한 동작은 셸 함수로 구현하는 것이 일반적이다.

</details>
