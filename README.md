<details> <summary>ENG (English Version)</summary>

## Chapter 2 – Directory and File Usage

**Section 1: Linux Files and Directories**
- File System Concept: Linux manages system information and devices using files like UNIX
- File and Directory Basics: Directories provide hierarchical structure; files are collections of related information; Linux organizes all files hierarchically
- File Types: Regular files (text, executable, image), directories, symbolic links, device files
- File Type Identification: Using `file` command to verify file types
- Directory Hierarchy: Tree structure with root directory (/) as the starting point; subdirectories and parent directories organized hierarchically
- Root Directory and Subdirectories: Root (/) at top level; subdirectories contain additional directories; subdirectories use .. (parent) and . (current)
- Root Directory Structure: Unique directory with no parent; contains basic subdirectories (etc, usr, home, tmp, etc.)
- Working Directory and Home Directory: Working directory (current directory) checked with `pwd`; home directory (~) assigned to each user for file storage
- Absolute and Relative Paths: Absolute paths start from root (/); relative paths use current location as reference
- File and Directory Naming Rules: Up to 255 characters; case-sensitive; files starting with . are hidden; special characters should be avoided

**Section 2: Directory-Related Commands**
- Checking Current Directory: `pwd` command displays current working directory
- Changing Directories: `cd` command moves to specified directories; supports both absolute and relative paths
- Ways to Return to Home Directory: `cd /home/user1` (absolute path), `cd ~` (home symbol), `cd` (no argument)
- Listing Directory Contents: `ls` command shows files and subdirectories in directory; various options available
- Viewing All Files: `-a` option displays hidden files (starting with .)
- Distinguishing File Types: `-F` option shows file type indicators (/ for directory, @ for symbolic link, * for executable)
- Using Multiple Options: Options combined after single hyphen (e.g., `ls -aF`)
- Specifying Target Directory: `ls` can display contents of specified directories without changing to them
- Detailed Information: `-l` option displays comprehensive file information (permissions, links, owner, size, modification date)
- Directory Information: `-d` option shows directory's own information instead of contents
- Similar Commands: `dir` and `vdir` commands provide similar directory viewing functionality
- Creating Single Directory: `mkdir` command creates one directory with specified name
- Creating Multiple Directories: `mkdir` can create multiple directories simultaneously
- Creating Intermediate Directories: `-p` option automatically creates missing parent directories in path
- Deleting Empty Directories: `rmdir` command removes only empty directories
- Deleting Non-Empty Directories: `rm -rf` forcefully deletes directories with contents (use cautiously)

**Section 3: File-Related Commands**
- Displaying File Contents Continuously: `cat` command outputs entire file content; `-n` option adds line numbers
- Viewing Files Screen-by-Screen: `more` command displays content page by page; shows progress indicator at bottom
- Displaying End of File: `tail` command shows last 10 lines by default; `-숫자` option specifies number of lines
- Continuous File Monitoring: `-f` option displays file updates periodically; useful for tracking file changes
- Copying Files: `cp` command copies files; first argument is source, second is destination
- File Copy Options: `-i` option prompts before overwriting; `-r` option required for copying directories
- Moving and Renaming Files: `mv` command moves files to different directories or renames files
- Deleting Files: `rm` command removes files; `-i` option prompts before deletion; `-r` option for directories
- File Links: Creates new names for existing files using `ln` command; includes hard links and symbolic links
- Linux File Structure: Files composed of filename + inode + data block; inode contains file metadata and data block addresses
- Hard Links: `ln` command creates hard links; same inode number; multiple names for same file
- Symbolic Links: `ln -s` creates symbolic links (like shortcuts); different inode; can link directories and cross file systems
- Hard Link vs. Symbolic Link: Hard links have same inode, same file system requirement; symbolic links have different inode, more flexible
- Creating Empty Files: `touch` command creates empty files or updates file modification time
- Changing Access/Modification Time: `touch -t` option allows specifying exact timestamp
- File Content Search: `grep` command searches for specific strings within files; `-n` option displays line numbers
- Finding Files: `find` command locates files by name, date, owner, and other criteria; `-exec` or `-ok` options execute commands on found files
- Locating Commands: `whereis` and `which` commands find command locations; return absolute paths
- Whereis vs. Which: `whereis` searches standard directories; `which` considers aliases and PATH environment variable

</details>

<details> <summary>KOR (한국어 버전)</summary>

## 2장 – 디렉터리와 파일 사용법

**리눅스의 파일과 디렉터리**
- 파일 시스템 개념: Linux는 Unix처럼 시스템 정보와 장치를 관리하기 위해 파일 사용
- 파일과 디렉터리의 기초: 디렉터리는 계층 구조 제공; 파일은 관련 정보들의 집합; Linux는 모든 파일을 계층적으로 조직화
- 파일의 종류: 일반 파일 (텍스트, 실행, 이미지), 디렉터리, 심볼릭 링크, 장치 파일
- 파일 종류 확인: `file` 명령으로 파일 타입 식별
- 디렉터리 계층 구조: 루트 디렉터리 (/)를 시작점으로 하는 트리 구조; 서브 디렉터리와 부모 디렉터리 계층적으로 구성
- 루트 디렉터리와 서브 디렉터리: 최상단 루트 (/); 디렉터리 아래 추가 디렉터리 포함; 부모(..)와 현재(.) 기호 사용
- 루트 디렉터리 구조: 부모 디렉터리 없는 유일한 디렉터리; 기본 서브 디렉터리 포함 (etc, usr, home, tmp 등)
- 작업 디렉터리와 홈 디렉터리: 작업 디렉터리 `pwd`로 확인; 홈 디렉터리 (~)는 각 사용자에게 할당
- 절대 경로명과 상대 경로명: 절대 경로는 루트(/)에서 시작; 상대 경로는 현재 위치 기준
- 파일과 디렉터리 이름 규칙: 최대 255자; 대소문자 구분; .(마침표)로 시작하면 숨김 파일; 특수문자 사용 자제

**디렉터리 관련 명령**
- 현재 디렉터리 확인: `pwd` 명령으로 현재 작업 디렉터리 표시
- 디렉터리 이동: `cd` 명령으로 지정 디렉터리로 이동; 절대/상대 경로 모두 지원
- 홈 디렉터리로 돌아가기: `cd /home/user1` (절대 경로), `cd ~` (홈 기호), `cd` (인자 없음)
- 디렉터리 내용 확인: `ls` 명령으로 파일과 서브 디렉터리 표시; 다양한 옵션 제공
- 숨김 파일 보기: `-a` 옵션으로 .(마침표)로 시작하는 숨김 파일 표시
- 파일 종류 표시: `-F` 옵션으로 파일 타입 기호 표시 (/ 디렉터리, @ 심볼릭 링크, * 실행 파일)
- 여러 옵션 사용: 하이픈 하나 뒤에 옵션 나열 (예: `ls -aF`)
- 지정 디렉터리 내용: `ls`로 현재 위치 이동 없이 특정 디렉터리 내용 표시
- 상세 정보 표시: `-l` 옵션으로 권한, 링크, 소유자, 크기, 수정 시간 등 표시
- 디렉터리 정보: `-d` 옵션으로 디렉터리 자체 정보 표시
- 유사 명령어: `dir`, `vdir` 명령으로 비슷한 디렉터리 확인 기능 제공
- 단일 디렉터리 생성: `mkdir` 명령으로 하나의 디렉터리 생성
- 여러 디렉터리 동시 생성: `mkdir`로 여러 디렉터리 한 번에 생성
- 중간 디렉터리 자동 생성: `-p` 옵션으로 경로의 missing 디렉터리 자동 생성
- 빈 디렉터리 삭제: `rmdir` 명령으로 빈 디렉터리만 삭제 가능
- 내용 있는 디렉터리 삭제: `rm -rf`로 강제 삭제 (사용 주의)

**파일 관련 명령**
- 파일 내용 연속 출력: `cat` 명령으로 전체 파일 내용 표시; `-n` 옵션으로 행 번호 추가
- 화면 단위 파일 보기: `more` 명령으로 페이지 단위 표시; 하단에 진행률 표시
- 파일 끝부분 출력: `tail` 명령으로 기본 10행 표시; `-숫자` 옵션으로 행 수 지정
- 파일 지속적 모니터링: `-f` 옵션으로 파일 변경 주기적 표시; 파일 변화 추적 용이
- 파일 복사: `cp` 명령으로 파일 복사; 첫 번째 인자는 원본, 두 번째는 목적지
- 파일 복사 옵션: `-i` 옵션으로 덮어쓰기 전 확인; `-r` 옵션은 디렉터리 복사 필요
- 파일 이동과 이름 변경: `mv` 명령으로 파일 이동 또는 이름 변경
- 파일 삭제: `rm` 명령으로 파일 삭제; `-i` 옵션으로 삭제 전 확인; `-r` 옵션은 디렉터리용
- 파일 링크: `ln` 명령으로 기존 파일에 새 이름 추가; 하드 링크와 심볼릭 링크 포함
- Linux 파일 구조: 파일명 + inode + 데이터 블록으로 구성; inode는 파일 메타데이터와 데이터 블록 주소 저장
- 하드 링크: `ln` 명령으로 생성; 동일 inode 번호; 같은 파일에 여러 이름
- 심볼릭 링크: `ln -s`로 생성 (바로가기처럼); 다른 inode; 디렉터리와 파일 시스템 간 링크 가능
- 하드 링크 vs. 심볼릭 링크: 하드 링크는 동일 inode, 같은 파일 시스템 제약; 심볼릭 링크는 다른 inode, 더 유연
- 빈 파일 생성: `touch` 명령으로 빈 파일 생성 또는 수정 시간 변경
- 접근/수정 시간 변경: `touch -t` 옵션으로 특정 타임스탬프 지정
- 파일 내용 검색: `grep` 명령으로 파일 내 특정 문자열 검색; `-n` 옵션으로 행 번호 표시
- 파일 찾기: `find` 명령으로 이름, 날짜, 소유자 등 조건으로 파일 검색; `-exec` 또는 `-ok` 옵션으로 명령 실행
- 명령 위치 찾기: `whereis`, `which` 명령으로 명령 위치 검색; 절대 경로 반환
- Whereis vs. Which: `whereis`는 표준 디렉터리 검색; `which`는 alias와 PATH 환경 변수 고려

</details>
