<details> <summary>ENG (English Version)</summary>

## Chapter 9 – User Management

**Section 1: User Account-Related Files**
- /etc/passwd: Core file storing user account info; readable by all; contains login ID, UID, GID, home directory, login shell; historically stored passwords but now uses /etc/shadow for security.
- /etc/passwd Structure: Seven fields per line—login ID (32 chars max, lowercase/uppercase/digits/underscore/hyphen), x (legacy password field), UID (0-999 reserved for system; 1000+ for users), GID (group membership), description, home directory, login shell.
- UID vs System Accounts: Linux identifies users by UID, not login name; users with same UID are treated as same user; system UIDs (0-999) shouldn't be modified; duplicate UIDs (if UID=0, treated as root).
- GID and Groups: Every Linux user belongs to at least one group; primary group set during user creation; details stored in /etc/group file; secondary groups also assignable.
- /etc/shadow: Separate file for encrypted passwords accessible only by root; stores login ID, encrypted password, last change date (Unix epoch: days since Jan 1, 1970), and password aging fields.
- Password Aging: MIN (minimum days before reuse), MAX (maximum days until expiration), WARNING (days before expiration alert), INACTIVE (days login allowed after expiration), EXPIRE (account expiration date), Flag (reserved).
- /etc/login.defs: Configuration file defining default account settings; well-commented for understanding each parameter.
- /etc/group: Stores group information including group name, group password placeholder (x), GID, and member list (comma-separated).
- /etc/gshadow: Encrypted group passwords stored here; contains group name, encrypted password, administrators (who can change password/members), and member list.

**Section 2: User Account Management Commands**
- useradd Command: Creates user accounts; options map to /etc/passwd fields; generates home directory if not exists; create group matching username by default.
- useradd Options: -u UID, -g GID (primary), -G secondary_groups, -c description, -d home_directory, -s login_shell, -e expiration_date, -f inactive_days.
- Default Settings: useradd -D shows defaults from /etc/default/useradd (GROUP, HOME, INACTIVE, EXPIRE, SHELL, SKEL, CREATE_MAIL_SPOOL); modify with useradd -D options.
- /etc/skel Directory: Default files copied to new user's home directory on account creation (e.g., .bash_profile); populate with common startup files if needed.
- Password Setup: New accounts have no password (!!); administrator must set with passwd command; user should change immediately after login.
- usermod Command: Modifies existing accounts; -u changes UID, -d changes home directory, -l changes login ID, -e/-f set expiration/inactive days.
- Password Aging with chage: Command dedicated to managing password aging (MIN, MAX, WARNING, INACTIVE, EXPIRE); integrates with passwd/usermod.
- userdel Command: Deletes user accounts; -r option removes home directory and files; may need find+rm for files outside home directory; check for running processes first.

**Section 3: Group Management Commands**
- groupadd: Creates groups; auto-assigns next available GID if not specified; -g sets specific GID (can be duplicate).
- groupmod: Modifies GID with -g option; renames group with -n (auto-updates file/directory ownership).
- groupdel: Deletes group by name.
- gpasswd: Sets group password, adds/removes members; -a adds member, -d removes member.
- newgrp: Temporarily switches current working group; requires group password if user not in group; changes GID and membership during session.

**Section 4: User Information Management Commands**
- UID vs EUID: UID (Real UID/RUID) is login account's ID; EUID (Effective UID) is ID running current command; differ when SetUID file executed or su used.
- who: Shows logged-in users with terminal, login time, external IP/hostname; -H adds headers, -q counts users, -b shows last boot, -r shows runlevel.
- last: Displays login/logout history with timestamps and terminal/IP; shows system boot times and shutdowns.
- whoami/who am i/id: whoami and id show EUID; who am i shows UID (Real UID); id also lists group memberships.
- groups: Lists groups current or specified user belongs to; no options shows current user's groups.
- SetUID and SetGID: SetUID allows executing file as owner; SetGID runs as group owner; su lets temporary user switching; both reveal UID/EUID differences.
- sudo: Grant specific commands to users via /etc/sudoers; visudo edits safely; format is username HOST=(runas_user) COMMANDS; critical for privilege delegation.
- sudo Cautions: Don't give all permissions to non-root users (password compromise = root compromise); select users and commands carefully.
- passwd Advanced: passwd -l locks account (adds ! to shadow), -u unlocks, -d removes password entirely; cryptographic one-way, verified on login.
- chown: Changes file/directory owner and group; -R applies recursively; format chown owner:group file; only root can use.
- chgrp: Changes group only (when chown isn't needed for owner change); -R for recursion.

</details>

<details> <summary>KOR (한국어 버전)</summary>

## 9장 – 사용자 관리

**사용자 계정 관련 파일**
- /etc/passwd: 사용자 계정 정보 저장 기본 파일로 모두 읽기 가능, 로그인 ID·UID·GID·홈 디렉터리·로그인 셸 등 포함, 과거 암호도 저장했으나 보안상 /etc/shadow로 분리.
- /etc/passwd 구조: 7개 필드—로그인 ID(32자 이내, 소문자·대문자·숫자·언더스코어·하이픈 사용 가능), x(레거시 암호 필드), UID(0~999는 시스템용, 1000부터 일반 사용자), GID(그룹 소속), 설명, 홈 디렉터리, 로그인 셸.
- UID와 시스템 계정: Linux는 로그인명이 아닌 UID로 사용자 식별, 같은 UID는 같은 사용자로 취급, 시스템 UID(0~999) 임의 수정 금지, UID 중복 주의(UID=0이면 root로 인식).
- GID와 그룹: 모든 Linux 사용자는 최소 1개 이상 그룹 소속, 주 그룹은 생성 시 지정, /etc/group에 정보 저장, 2차 그룹도 할당 가능.
- /etc/shadow: root만 접근 가능한 별도 파일로 암호화된 암호 저장, 로그인 ID·암호·최종 변경일(Unix 에포크: 1970.1.1 기준 경과 일수)·패스워드 에이징 항목 포함.
- 패스워드 에이징: MIN(재사용 최소 기간)·MAX(최대 사용 기간)·WARNING(만료 전 경고 일수)·INACTIVE(만료 후 로그인 허용 기간)·EXPIRE(계정 만료일)·Flag(예약).
- /etc/login.defs: 계정 설정 기본값 정의 파일로, 주석이 상세해 각 항목 역할 이해 용이.
- /etc/group: 그룹 정보 저장—그룹명, 그룹 암호 자리(x), GID, 멤버 목록(쉼표 구분).
- /etc/gshadow: 암호화된 그룹 암호 저장 파일—그룹명, 암호, 관리자(암호·멤버 변경 가능), 멤버 목록.

**사용자 계정 관리 명령**
- useradd: 사용자 생성 명령, 옵션이 /etc/passwd 필드에 대응, 홈 디렉터리 자동 생성, 기본값으로 사용명과 같은 그룹 생성.
- useradd 옵션: -u UID·-g GID(주 그룹)·-G 2차그룹·-c 설명·-d 홈디렉터리·-s 로그인셸·-e 계정만료일·-f 유휴기간.
- 기본값 설정: useradd -D로 /etc/default/useradd의 기본값 확인(GROUP·HOME·INACTIVE·EXPIRE·SHELL·SKEL·CREATE_MAIL_SPOOL), useradd -D 옵션으로 수정.
- /etc/skel 디렉터리: 신규 사용자 홈 디렉터리에 자동 복사될 초기화 파일 위치(.bash_profile 등), 공통 파일 배포 시 활용.
- 암호 설정: 신규 계정은 암호 없음(!!), 관리자가 passwd로 설정 필수, 사용자는 첫 로그인 후 변경 권장.
- usermod: 기존 계정 수정, -u로 UID 변경, -d로 홈디렉터리 변경, -l로 로그인ID 변경, -e/-f로 만료일/유휴기간 설정.
- chage: 패스워드 에이징 전용 관리 명령으로 MIN·MAX·WARNING·INACTIVE·EXPIRE 설정, passwd/usermod와 연동.
- userdel: 사용자 삭제, -r로 홈디렉터리까지 함께 제거, 홈 외 파일은 find+rm으로 별도 처리, 실행 중인 프로세스 확인 필수.

**그룹 관리 명령**
- groupadd: 그룹 생성, GID 미지정 시 자동 할당, -g로 GID 지정(중복 가능).
- groupmod: GID 변경은 -g, 그룹명 변경은 -n(자동으로 파일·디렉터리 소유권도 변경).
- groupdel: 그룹명으로 그룹 삭제.
- gpasswd: 그룹 암호 설정, -a로 멤버 추가, -d로 멤버 제거.
- newgrp: 현재 작업 그룹을 임시 전환, 사용자가 속하지 않은 그룹일 시 그룹 암호 필요, 세션 중 GID·소속 변경.

**사용자 정보 관리 명령**
- UID vs EUID: UID(실제 UID/RUID)는 로그인 계정 ID, EUID(유효 UID)는 현재 명령 실행 주체 ID, SetUID 파일 실행 또는 su 사용 시 달라짐.
- who: 로그인 사용자 표시(터미널·로그인시간·외부IP/호스트명), -H로 헤더 추가, -q로 인원 집계, -b로 마지막 부팅 시간, -r로 현재 런레벨 표시.
- last: 로그인·로그아웃 기록 표시(시간·터미널/IP), 시스템 부팅·종료 시간도 확인 가능.
- whoami/who am i/id: whoami·id는 EUID 표시, who am i는 UID(실제 UID) 표시, id는 그룹 목록도 함께 표시.
- groups: 현재 또는 지정 사용자가 속한 그룹 목록, 옵션 없으면 현재 사용자 그룹 표시.
- SetUID와 SetGID: SetUID는 파일을 소유자로 실행, SetGID는 그룹 소유자로 실행, su로 임시 사용자 전환, UID/EUID 차이 확인 가능.
- sudo: /etc/sudoers에서 특정 명령 권한 부여, visudo로 안전 편집, 형식은 사용자명 HOST=(실행사용자) 명령, 권한 위임의 핵심 도구.
- sudo 주의사항: 비root 사용자에게 전체 권한 부여 금지(암호 유출=root 침해), 사용자·명령 신중 선택.
- passwd 심화: passwd -l로 계정 잠금(shadow에 ! 추가), -u로 잠금 해제, -d로 암호 완전 삭제, 암호는 암호화되어 로그인 시 재검증.
- chown: 파일·디렉터리 소유자·그룹 변경, -R로 재귀 적용, 형식 chown 소유자:그룹 파일, root만 사용 가능.
- chgrp: 그룹만 변경(소유자 변경 불필요 시), -R로 재귀 적용.

</details>

