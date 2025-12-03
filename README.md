<details> <summary>ENG (English Version)</summary>

## Chapter 8 – Software Management

**Section 1: Installing RPM Packages**
- RPM Overview and Features: Red Hat’s RPM tool installs binary packages without compiling, places files into appropriate directories, allows bulk removal, upgrades existing packages in place, verifies installation state, and provides package information.
- RPM Package Naming: Names contain package name, version, release (build sequence and target distro like el9_2 and rocky tags), architecture (e.g., x86_64), and .rpm extension.
- Basic rpm Commands: rpm -qa lists installed packages; rpm -qa | grep checks if a specific package is installed; rpm -qf /path/to/file finds which package owns a file; rpm -qi /name shows detailed info; -qip/-qif show details for a given package file or a file’s owning package.
- Installing and Upgrading: rpm -ivh pkg.rpm installs with progress; rpm -Uvh upgrades if installed or installs if new; -U is typically preferred over -i.
- Downloading RPMs: Packages for Rocky can be obtained from sites such as pkgs.org, which categorize packages by distribution and version.
- Dependency Handling: When installing a package like xterm, required libraries (e.g., libXaw.so.7, libXmu.so.6, libXt.so.6) must be installed first to satisfy dependencies.

**Section 2: Installing Packages with dnf**
- dnf Basics: High-level package manager on Rocky/Red Hat-based systems that resolves dependencies automatically and accesses online repositories.
- Installing and Removing: dnf install packagename installs packages; dnf remove or dnf erase packagename removes them along with unneeded dependencies.
- Updating: dnf update or dnf upgrade refreshes packages to newer versions from repositories.
- Searching and Info: dnf search keyword finds relevant packages; dnf info packagename shows description, version, repo, and other metadata.

**Section 3: File Archive and Compression**
- tar Archiving: tar gathers multiple files/directories into a single archive (tar file) without compression; commonly used before compressing.
- gzip and gunzip: gzip compresses files, usually producing .gz; gunzip or gzip -d decompresses them; tar with -z option can create/extract .tar.gz in one step.
- bzip2 and bunzip2: bzip2 produces .bz2 with better compression than gzip; bunzip2 decompresses; bzcat can view contents of compressed tar archives like ch2.tar.bz2.
- Common Workflows: tar cf archive.tar dir; gzip or bzip2 archive.tar for compression; tar xzf or tar xjf to extract compressed tar archives.

**Section 4: Software Compilation**
- Compiler Concept: A compiler translates high-level languages (like C) into machine code (executables); GNU C Compiler (gcc) is standard on Linux.
- Checking/Installing gcc: rpm or dnf is used to check if gcc is installed; if only libraries exist but not compiler, install via dnf install gcc.
- Compiling C Programs: Write source (e.g., with vi) and compile using gcc source.c; if no errors, default executable is a.out unless overridden.
- Running Executables: Execute with ./a.out when the current directory is not in PATH; otherwise “command not found” will occur.
- Renaming Output: Use gcc -o program source.c to specify a custom executable name instead of a.out.
- make and Makefile: make automates multi-file builds based on rules defined in a Makefile; it compiles and links multiple .c files into one executable.
- Creating Makefiles: Makefiles define variables (e.g., TARGET, OBJECTS) and rules; gcc -c compiles .c to .o, and linking rules combine .o files into the final executable.

</details>

<details> <summary>KOR (한국어 버전)</summary>

## 8장 – 소프트웨어 관리

**RPM 패키지 설치**
- RPM 개요와 특징: 레드햇에서 만든 패키지 관리 도구로, 바이너리 패키지를 컴파일 없이 설치하고 관련 디렉터리에 바로 배치하며, 한 번에 삭제·업그레이드·검증 및 정보 조회가 가능하다.
- 패키지 이름 구성: 패키지 이름, 버전, 릴리즈(빌드 순서와 대상 배포판 el9_2, rocky 태그 등), 아키텍처(x86_64 등), 확장자 .rpm으로 구성된다.
- 기본 rpm 명령: rpm -qa로 전체 설치 목록 조회, rpm -qa | grep로 특정 패키지 설치 여부 확인, rpm -qf 파일경로로 해당 파일의 패키지 조회, rpm -qi 이름으로 상세 정보, -qip/-qif로 패키지 파일이나 특정 파일이 속한 패키지 정보 확인.
- 설치와 업그레이드: rpm -ivh 패키지.rpm으로 설치, rpm -Uvh로 설치/업그레이드 겸용 사용하며, -U가 기존 설치 시 업그레이드, 미설치 시 신규 설치를 수행하므로 실무에서 더 자주 쓰인다.
- RPM 다운로드: Rocky용 패키지는 pkgs.org 같은 사이트에서 배포판·버전별로 구분되어 제공되며, 브라우저로 링크를 복사해 rpm 파일을 내려받는다.
- 의존성 문제: xterm 설치 시 특정 라이브러리(libXaw.so.7, libXmu.so.6, libXt.so.6 등)가 필요하다는 오류가 나면, 해당 의존 패키지를 먼저 설치해야 한다.

**dnf를 이용한 패키지 설치**
- dnf 기본 개념: Rocky/Red Hat 계열에서 사용하는 고수준 패키지 관리자이며, 온라인 저장소를 이용해 자동으로 의존성을 해결해 준다.
- 설치·삭제: dnf install 패키지명으로 설치하고, dnf remove/erase 패키지명으로 제거하며 불필요한 의존 패키지도 함께 정리한다.
- 업데이트: dnf update 또는 dnf upgrade로 설치된 패키지를 최신 버전으로 갱신한다.
- 검색·정보: dnf search 키워드로 관련 패키지 검색, dnf info 패키지명으로 설명·버전·저장소 등의 상세 정보를 확인한다.

**파일 아카이브와 압축**
- tar 아카이브: 여러 파일·디렉터리를 묶어 하나의 tar 파일(묶기만 하고 압축은 하지 않음)로 만드는 도구이며, 보통 압축 전 단계로 사용된다.
- gzip/gunzip: gzip으로 파일을 .gz 형식으로 압축하고, gunzip 또는 gzip -d로 압축을 해제하며, tar -z 옵션으로 .tar.gz를 한 번에 생성·해제할 수 있다.
- bzip2/bunzip2: bzip2는 .bz2 파일로 gzip보다 더 높은 압축률을 제공하고, bunzip2로 해제하며, bzcat으로 ch2.tar.bz2 같은 압축 파일의 내용을 바로 확인할 수 있다.
- 일반적인 흐름: tar cf archive.tar 디렉터리로 아카이브 생성 후 gzip/bzip2로 압축, tar xzf 또는 tar xjf로 압축된 tar 아카이브를 해제한다.

**소프트웨어 컴파일**
- 컴파일러 개념: C 같은 고급 언어를 기계어 실행 파일로 변환하는 도구이며, 리눅스에서는 GNU C 컴파일러(gcc)를 사용한다.
- gcc 설치 확인: rpm이나 dnf로 gcc 관련 패키지 유무를 확인하고, 컴파일러가 없다면 dnf install gcc로 설치한다.
- C 프로그램 컴파일: vi로 소스 파일을 작성한 뒤 gcc 소스.c 형태로 컴파일하며, 오류가 없으면 기본 실행 파일 a.out이 생성된다.
- 실행 방법: 현재 디렉터리가 PATH에 없으므로 ./a.out처럼 경로를 포함해 실행해야 하며, 그렇지 않으면 명령을 찾을 수 없다는 오류가 난다.
- 실행 파일명 지정: gcc -o 프로그램명 소스.c로 a.out 대신 원하는 이름으로 실행 파일을 만들 수 있다.
- make와 Makefile: make는 Makefile에 정의된 규칙을 읽어 여러 소스 파일을 자동으로 컴파일·링크하며, 복잡한 빌드를 하나의 명령으로 처리하게 해준다.
- Makefile 작성: TARGET, OBJECTS 같은 매크로를 정의하고, gcc -c로 .c를 .o로 컴파일한 뒤 .o 파일을 링크해 최종 실행 파일을 만드는 규칙을 작성한다.

</details>

