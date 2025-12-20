<details>
<summary>ENG (English Version)</summary>

## **1. What is Linux?**
- Open-source UNIX-like OS kernel, invented by Linus Torvalds in 1991.
- Popular for flexibility, stability, and being free.
- Used in servers, desktops, embedded systems.

## **2. Advantages of Linux**
- Open-source & free: Cost-efficient and customizable.
- Stability & Security: Rarely crashes, virus-resistant.
- Multitasking and multi-user supported.
- Runs on various hardware (low to high spec).

## **3. Disadvantages of Linux**
- Steep learning curve for beginners.
- Compatibility issues with some commercial software.
- Requires more command-line interaction.

## **4. Linux Architecture**
- **Kernel**: Core managing CPU, memory, devices.
- **Shell**: Interface between user and kernel.
- **File System**: Hierarchical, root directory "/".
- **Utilities**: Various command-line tools (e.g., ls, cp, mv).

## **5. Linux File System**
- Everything is a file.
- Hierarchical structure starting from `/`.
- Important directories:
  - `/bin`: Essential binaries
  - `/etc`: Config files
  - `/home`: User directories
  - `/dev`: Devices
  - `/var`: Variable data
  - `/tmp`: Temporary files

## **6. Basic Linux Commands**
- **File operations**: `ls`, `cd`, `cp`, `mv`, `rm`, `touch`, `mkdir`
- **Permissions**: `chmod`, `chown`, `umask`
- **Processes**: `ps`, `top`, `kill`, `nice`
- **Package Management**: `apt`, `yum`, `dpkg`, `rpm`
- **Others**: `man`, `echo`, `cat`, `grep`, `find`

## **7. File Permissions**
- Three types: read (r), write (w), execute (x)
- Assigned to: owner, group, others
- Numeric notation: `chmod 755` etc.
- Symbolic: `chmod u+x file`

## **8. Linux Shell**
- Command-line interpreter: bash, sh, zsh
- Executes commands and scripts.
- Supports variables, control structures (if, for, while).
- Allows automation via shell scripting.

## **9. Shell Scripting Basics**
- Start with `#!/bin/bash`
- Use variables (`VAR=value`), echo, conditionals.
- Control flow: if/else, loops (for, while).
- Example:
```bash
#!/bin/bash
for i in {1..5}
do
  echo "Line $i"
done
````

## **10. Package Management**

* **Debian-based**: `apt`, `dpkg`
* **Red Hat-based**: `yum`, `dnf`, `rpm`
* Install, update, remove software.

## **11. Process Management**

* `ps`, `top`, `kill`, `nice`, `renice`
* Background (`&`) and foreground processes.
* `jobs`, `fg`, `bg` for job control.

## **12. Networking in Linux**

* `ifconfig`, `ip`, `ping`, `netstat`, `ss`
* Configuration via `/etc/network/` or `nmcli`
* SSH: `ssh user@host`, `scp`, `rsync`

## **13. System Monitoring & Logs**

* Monitor: `top`, `htop`, `free`, `df`, `du`
* Logs: `/var/log/` (e.g., syslog, auth.log)
* `journalctl` for systemd logs

## **14. User & Group Management**

* Add/remove users: `adduser`, `deluser`
* Set passwords: `passwd`
* Groups: `groupadd`, `usermod -aG`
* File ownership: `chown`

## **15. Crontab & Scheduling**

* Automate tasks: `crontab -e`
* Syntax: `* * * * * command`

  * Minute, Hour, Day, Month, Weekday
* Use for backups, updates, etc.

## **16. Important Configuration Files**

* `/etc/passwd`, `/etc/shadow`: user info
* `/etc/fstab`: disk mounting
* `/etc/hosts`: local hostname mapping
* `/etc/crontab`: system-wide cron jobs

</details>

<details>
<summary>KOR (한국어 버전)</summary>

## **1. 리눅스란?**

* 1991년 리누스 토발즈가 개발한 오픈소스 UNIX 계열 운영체제 커널.
* 무료, 유연성, 안정성이 장점.
* 서버, 데스크탑, 임베디드 장치 등에 사용.

## **2. 리눅스의 장점**

* 오픈소스 및 무료.
* 뛰어난 안정성과 보안성.
* 멀티태스킹 및 다중 사용자 지원.
* 저사양부터 고사양까지 폭넓은 호환성.

## **3. 리눅스의 단점**

* 초보자에게는 진입장벽 높음.
* 상용 소프트웨어와의 호환성 이슈.
* 터미널 기반 명령어 필요.

## **4. 리눅스 구조**

* **커널**: 핵심 기능(CPU, 메모리, 장치 관리).
* **셸(Shell)**: 사용자와 커널 사이 인터페이스.
* **파일 시스템**: 계층 구조, 루트는 `/`.
* **유틸리티**: 다양한 명령어 도구.

## **5. 파일 시스템 구조**

* 모든 것이 파일로 취급.
* 루트(`/`)에서 시작되는 계층적 구조.
* 주요 디렉토리:

  * `/bin`: 필수 명령어
  * `/etc`: 설정 파일
  * `/home`: 사용자 폴더
  * `/dev`: 장치 파일
  * `/var`: 로그 등 가변 데이터
  * `/tmp`: 임시 파일

## **6. 기본 명령어**

* **파일 관련**: `ls`, `cd`, `cp`, `mv`, `rm`, `touch`, `mkdir`
* **권한 관련**: `chmod`, `chown`, `umask`
* **프로세스 관리**: `ps`, `top`, `kill`, `nice`
* **패키지 관리**: `apt`, `yum`, `dpkg`, `rpm`
* **기타**: `man`, `echo`, `cat`, `grep`, `find`

## **7. 파일 권한**

* 읽기(r), 쓰기(w), 실행(x)
* 사용자, 그룹, 기타 사용자로 구분.
* 숫자 표현: `chmod 755`
* 기호 표현: `chmod u+x 파일명`

## **8. 셸(Shell)**

* bash, sh, zsh 등 명령어 인터프리터.
* 명령어 실행, 변수 사용, 제어구조 지원.
* 셸 스크립트를 통해 자동화 가능.

## **9. 셸 스크립트 기본**

* `#!/bin/bash`로 시작.
* 변수, 조건문, 반복문 사용.
* 예시:

```bash
#!/bin/bash
for i in {1..5}
do
  echo "Line $i"
done
```

## **10. 패키지 관리**

* **Debian 계열**: `apt`, `dpkg`
* **Red Hat 계열**: `yum`, `dnf`, `rpm`
* 설치, 삭제, 업데이트 기능 제공.

## **11. 프로세스 관리**

* `ps`, `top`, `kill`, `nice`, `renice`
* 백그라운드/포그라운드 작업 제어: `&`, `jobs`, `fg`, `bg`

## **12. 네트워크 명령어**

* `ifconfig`, `ip`, `ping`, `netstat`, `ss`
* 설정: `/etc/network/`, `nmcli`
* SSH: `ssh`, `scp`, `rsync`로 원격 접속/복사

## **13. 시스템 모니터링 및 로그**

* 모니터링: `top`, `htop`, `free`, `df`, `du`
* 로그 위치: `/var/log/`
* `journalctl`: systemd 기반 로그 확인

## **14. 사용자 및 그룹 관리**

* 사용자 추가/삭제: `adduser`, `deluser`
* 비밀번호 설정: `passwd`
* 그룹 관리: `groupadd`, `usermod -aG`
* 소유권 변경: `chown`

## **15. 작업 스케줄링 (Crontab)**

* `crontab -e`로 자동 작업 설정
* 형식: `* * * * * 명령어` (분 시 일 월 요일)
* 주기적 백업, 자동 실행에 사용

## **16. 주요 설정 파일**

* `/etc/passwd`, `/etc/shadow`: 사용자 정보
* `/etc/fstab`: 디스크 마운트 정보
* `/etc/hosts`: 호스트 이름 매핑
* `/etc/crontab`: 시스템 전체 예약 작업

</details>
