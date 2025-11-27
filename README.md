<details> <summary>ENG (English Version)</summary>

## Chapter 4 – Text Editing

**Section 1: Linux Text Editors**
- Editor Types: Line editors (edit one line at a time, inconvenient) vs screen editors (like Notepad or gedit, edit with full-screen view and cursor movement).
- ex Editor: Line editor usually used through vi to provide powerful additional commands.
- vi/vim: Standard screen editor on Linux; uses ex commands, has simple keystroke-based commands, fast but different from typical GUI editors so requires practice.
- nano and pico: Simple editors originally from the University of Washington; nano is an open-source replacement for pico and is available on Rocky Linux while pico usually is not.
- emacs: Feature-rich, complex editor mainly used by advanced users; GNU Emacs is popular and free but typically not preinstalled.
- Modal vs Non-Modal Editors: Modal editors separate input mode and command mode; non-modal editors use control keys (Ctrl, Alt) for editing without explicit mode switching.

**Section 2: Using vi**
- vi Modes: Has input mode, command mode, and last-line mode; text is entered in input mode, edited and managed (delete, search, save) in command/last-line modes.
- Mode Switching: Starts in command mode; keys i, I, a, A, o, O switch to input mode; Esc returns to command mode; :, /, ? enter last-line mode; Enter executes last-line commands.
- Starting vi: Can start with or without a filename; existing file opens, nonexistent name creates a new buffer; if no name is given, it can be set later in last-line mode.
- Saving and Exiting: From command/last-line mode, users can save and quit, quit without saving, or save under a different filename using appropriate ex-style commands.
- Entering Input Mode: i inserts text at cursor; o inserts a new line below the current line and enters input mode; Esc ends input mode and returns to command mode.
- Cursor Movement: Uses keyboard only; h/j/k/l or dedicated keys like w, b, e move by word, ^ moves to line start, $ to line end, H/M move to top/middle of screen, etc.

**Section 3: Searching, Replacing, and Editing in vi**
- Searching Text: Use /pattern to search forward and ?pattern to search backward from the cursor; n repeats the search for the next match.
- Replacing Text: In last-line mode, :s/old/new/ replaces in current line, :3,4s/old/new/ limits replacement to lines 3–4; adding g applies replacement to all matches in the range.
- Global Replace: :%s/old/new/g or :1,$s/old/new/g replaces all occurrences in the entire file and reports how many were changed.
- Reading Other Files: :r filename inserts another file’s content into the current buffer at the specified location (e.g., after a given line).
- Switching Files: :e otherfile switches to editing another file; :n moves to the next file when multiple filenames were provided at startup; :e! forces switching without saving.
- Using Shell Commands: :! command runs a single shell command without leaving vi; :sh temporarily drops to a shell, and exit returns to vi.
- Useful Extra Commands: Ctrl+l redraws the screen; J joins the current line with the next; . repeats the last command (except movement); ~ toggles the case of the character under the cursor.

</details>

<details> <summary>KOR (한국어 버전)</summary>

## 4장 – 문서 편집

**리눅스의 문서 편집기**
- 편집기 종류: 한 줄씩만 작업하는 행 편집기와 화면 전체에서 내용을 보며 커서를 옮겨 작업하는 화면 편집기로 나뉜다.
- ex 편집기: 단독보다는 vi와 함께 사용하며, vi의 기능을 강화하는 다양한 명령을 제공하는 행 편집기이다.
- vi(vim): 리눅스에서 가장 일반적으로 사용하는 화면 편집기로, ex 명령을 그대로 쓸 수 있고 키 조합이 단순해 빠른 편집이 가능하지만 GUI 메모장과 방식이 달라 처음에는 낯설 수 있다.
- nano와 pico: 초보자도 쓰기 쉬운 편집기로, 라이선스 이슈 때문에 GNU에서 pico 기반 nano를 만들었고, 로키 리눅스에는 nano만 기본 제공된다.
- emacs: 기능이 매우 많지만 사용법이 복잡해 전문가 위주로 쓰이며, GNU Emacs가 대표적이고 무료이지만 대부분 배포판에서 별도 설치가 필요하다.
- 모드형 vs 비모드형: 모드형은 입력 모드와 명령 모드를 구분하고, 비모드형은 Ctrl·Alt 같은 조합키로 편집 기능을 수행해 모드 전환 없이 작업한다.

**vi 사용법**
- vi 모드 구조: 입력 모드, 명령 모드, 마지막 행 모드가 있으며, 입력 모드에서 내용을 쓰고 나머지 모드에서 삭제·검색·저장 같은 작업을 수행한다.
- 모드 전환: vi는 처음 명령 모드로 시작하고, i/I/a/A/o/O를 누르면 입력 모드로 들어가며 Esc를 누르면 다시 명령 모드로 돌아온다.
- 마지막 행 모드: 명령 모드에서 :, /, ?를 누르면 마지막 행 모드가 되고, 여기서 저장·종료, 검색, 치환 같은 ex 형식 명령을 입력해 Enter로 실행한다.
- vi 시작: 파일명을 지정하면 해당 파일을 열고, 없는 파일명은 새 파일로 취급하며, 파일명을 생략하면 나중에 마지막 행 모드에서 저장할 때 이름을 정할 수 있다.
- 저장과 종료: 명령 모드 또는 마지막 행 모드에서 편집 내용을 저장·종료하거나, 저장하지 않고 종료하거나, 다른 이름으로 저장하는 명령을 사용할 수 있다.
- 입력 모드 진입: i는 현재 위치에 삽입, o는 다음 줄에 새 줄을 만들고 그 줄에서 입력을 시작하며, Esc를 누르면 다시 명령 모드로 전환된다.
- 커서 이동: 마우스를 쓰지 않고 키보드로만 이동하며, w/b/e로 단어 단위 이동, ^로 행의 시작, $로 행의 끝, H/M 등으로 화면 기준 이동을 할 수 있다.

**vi에서 검색·치환·추가 기능**
- 문자열 검색: 마지막 행 모드에서 /문자열로 아래 방향, ?문자열로 위 방향 검색을 수행하고, n을 누르면 다음 일치 항목으로 이동한다.
- 문자열 바꾸기: :s/old/new/로 현재 행의 첫 일치만, :s/old/new/g로 해당 행의 모든 일치를 바꾸며, :3,4s/old/new/로 특정 행 범위만 치환할 수 있다.
- 전체 파일 치환: :%s/old/new/g 또는 :1,$s/old/new/g로 파일 전체에서 문자열을 찾아 모두 바꾸고, 몇 개가 바뀌었는지 마지막 행에 표시된다.
- 다른 파일 읽어오기: :r 파일명으로 현재 편집 중인 파일의 특정 위치에 다른 파일 내용을 삽입할 수 있다.
- 파일 전환: :e 다른파일 로 현재 작업을 마치고 다른 파일 편집으로 넘어가며, vi를 여러 파일명과 함께 실행한 경우 :n으로 다음 파일로 이동한다.
- 셸 명령 사용: :! 명령으로 vi를 종료하지 않고 한 번의 셸 명령을 실행하고, :sh로 잠시 셸로 나갔다가 exit로 다시 vi로 복귀할 수 있다.
- 기타 유용한 명령: Ctrl+l로 화면을 다시 그려 주고, J로 현재 행과 다음 행을 하나로 연결하며, .로 직전 명령을 반복하고, ~로 커서 위치 글자의 대·소문자를 토글한다.

</details>
