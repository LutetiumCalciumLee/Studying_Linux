<details> <summary>ENG (English Version)</summary>

## Chapter 6 – Process Management

**Section 1: Process Concepts**
- Process Definition: A currently running program on the system, identified by a unique process ID (PID) starting from 1 and incrementing.
- Parent-Child Relationship: Parents create children; children can create their own children; systemd (PID 1) and kthreadd (PID 2) are the system's initial processes, with systemd becoming the parent of all orphan processes.
- Daemon Processes: Long-running background services that wait for requests and provide services such as web servers or databases.
- Orphan Process: A child process whose parent has terminated; process 1 (systemd) automatically adopts it to ensure proper termination.
- Zombie Process: A child process that has terminated but whose exit status has not yet been read by the parent; occupies a process table slot and can't be killed with normal signals; solved when parent reads status or terminates.

**Section 2: Process Management Commands**
- ps Command Overview: Lists running processes; supports UNIX/SVR4 (-), BSD (no dash), and GNU (--).
- Basic ps Output: PID (process number), TTY (terminal), TIME (CPU usage), CMD (command); ps alone shows only user terminal processes.
- ps -f Option: Displays detailed info including parent PID (PPID), CPU % (C), and start time.
- ps a and ps aux: BSD options; a shows terminal processes, aux adds CPU/memory usage info for all processes.
- ps -e and ps -ef: UNIX options; -e shows all processes system-wide, -ef adds details; -ef is most often used.
- User and PID Filtering: -u for user, -p for specific PID; both can combine with -f for details.
- pgrep: Searches processes by name/pattern, returns PID; -l shows command names.
- kill: Sends signals to terminate processes; kill -l lists signals; 15 is graceful, 9 is forced termination.
- pkill and killall: pkill terminates by name and may kill many; killall matches exact command name.
- top: Real-time monitor showing system and process stats, CPU/memory usage, and interactive controls.
- System Information Tool: GNOME-based GUI that displays process name, user, resource usage, and lets you stop processes.

**Section 3: Foreground and Background Processes**
- Foreground vs. Background: Foreground occupies terminal and requires completion; background runs independently and allows continued use.
- Job Control: Enables managing multiple processes in one terminal.
- Foreground Process: User waits for completion and prompt before executing next command.
- Background Process: Launched with & and keeps terminal available; viewed with jobs.
- Bringing Background to Foreground: Use fg or fg %job#; terminal then suspends for that job.
- Suspending Foreground: Ctrl+z pauses foreground job, shell regains control.
- jobs Command: Lists current jobs, their numbers, status, and commands.

**Section 4: Job Scheduling**
- at Command: Schedules a command once at a chosen future time.
- atq: Views scheduled 'at' jobs and their info.
- at -d/atrm: Delete scheduled jobs before execution.
- crontab: Manages repetitive scheduled tasks with crontab files for weekly, daily, hourly jobs.
- crontab Format: Six fields per line (minute, hour, day, month, weekday, command); "*" means "all values".
- crontab -e: Edit/create user's crontab; uses specified editor, stores in /var/spool/cron by username.
- crontab -l: Shows crontab file contents.
- crontab -r: Deletes crontab file; admins can target users.
- at/cron Permission Files: /etc/at.allow/.deny and /etc/cron.allow/.deny control user access; .allow takes priority, empty .deny allows all.

</details>

<details> <summary>KOR (한국어 버전)</summary>

## 6장 – 프로세스 관리

**프로세스의 개념**
- 프로세스 정의: 시스템에서 실행 중인 프로그램으로, 번호(PID)는 1부터 시작해 고유하게 부여된다.
- 부모-자식 관계: 부모가 자식을 생성하고, 자식도 자식을 생성할 수 있으며, systemd(1번)와 kthreadd(2번)가 초기 프로세스가 된다. 고아 프로세스는 systemd가 새로운 부모가 되어 관리한다.
- 데몬 프로세스: 서비스 요청이 오면 즉시 반응하는 대기 프로세스로 웹서버, 데이터베이스 등이 여기에 속한다.
- 고아 프로세스: 부모가 먼저 종료된 뒤 자식이 남는 경우, systemd가 이를 관리한다.
- 좀비 프로세스: 자식이 종료됐으나 부모가 종료 신호를 읽지 않아 테이블에 남는 상태로, 보통 kill로 제거되지 않으며 부모 종료나 SIGCHLD로 해결한다.

**프로세스 관리 명령**
- ps 명령 개요: 실행 중 프로세스를 표시하며 UNIX(-), BSD(하이픈 없음), GNU(--) 옵션을 지원한다.
- ps 기본 출력: PID(번호), TTY(터미널), TIME(CPU 사용량), CMD(명령); 옵션 없이 현재 터미널만 표시.
- ps -f: PPID(부모번호), CPU 사용률 등 상세 정보.
- ps a/aux: BSD 옵션. a는 터미널 전용, aux는 시스템 전체의 CPU·메모리 등 자세한 정보.
- ps -e/-ef: UNIX 옵션. -e는 전체, -ef는 추가 정보 포함. -ef가 가장 많이 사용됨.
- 사용자/PID별 조회: -u, -p로 각각 사용자·프로세스 지정해서 조회하며, -f와 조합해 상세 정보 확인.
- pgrep: 프로세스 이름 검색, PID 반환. -l로 명령명 같이 표시.
- kill: 시그널로 종료. kill -l로 시그널 종류 확인, 15(정상종료), 9(강제종료) 등이 자주 사용됨.
- pkill/killall: 이름으로 프로세스를 한 번에 종료. pkill은 패턴, killall은 CMD 명 전체 일치.
- top: 실시간 모니터링; 시스템 요약·프로세스 세부 정보·CPU/메모리 사용률 등 표시.
- 시스템 정보 도구: Rocky Linux GNOME에서 제공하는 GUI로 프로세스 정보 확인 및 종료 가능.

**포그라운드/백그라운드 작업**
- 포그라운드 vs 백그라운드: 포그라운드는 터미널 점유, 백그라운드는 독립 실행으로 즉시 터미널 사용 가능.
- 작업 제어: 여러 작업을 동시에 관리.
- 포그라운드: 완료 후 프롬프트 복귀까지 기다림.
- 백그라운드: &로 실행하며 jobs 명령으로 조회.
- 포그라운드 전환: fg 또는 fg %번호로 백그라운드 작업을 앞으로 가져옴.
- 일시중지: Ctrl+z로 잠시 멈춰서 셸이 제어권을 재획득.
- jobs: 현재 작업, 번호, 상태, 명령 표시.

**작업 예약**
- at: 미래 특정 시각에 단일 작업 예약.
- atq: at 예약 목록 확인.
- at -d/atrm: 예약 삭제.
- crontab: 주기적 작업 예약/관리.
- crontab 형식: 분, 시, 일, 월, 요일, 명령 6개 필드. *은 전체 값.
- crontab -e: 편집기로 파일 생성/수정.
- crontab -l: 현재 파일 내용 확인.
- crontab -r: 파일 삭제, 관리자도 특정 사용자 지정 가능.
- at/cron 권한: /etc/at.allow/.deny, /etc/cron.allow/.deny로 사용자별 접근 제어. .allow 우선, 빈 .deny는 전체 허용.

</details>
