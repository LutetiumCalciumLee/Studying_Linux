<details> <summary>ENG (English Version)</summary>

## Chapter 7 – Linux Boot and Shutdown

**Section 1: Linux System Boot Process**
- Boot Definition: Spans from power-on through kernel initialization to login prompt display; divided into hardware boot and Linux OS boot phases.
- BIOS Stage: First activates when power is turned on, checks connected hardware, loads 512B Master Boot Record (MBR) from boot disk, and loads the bootloader.
- Bootloader Role: Finds and loads the Linux kernel from disk into memory; typically offers menu to select among multiple OSes; GRUB is the standard Linux bootloader.
- Kernel Initialization: After bootloader loads kernel, kernel checks hardware devices, creates kernel processes and threads for internal operations (displayed in brackets), maintains low PID numbers.
- systemd Service Stage: After kernel initialization, systemd activates various system services; boot progress shown via boot splash image (Alt+d toggles message display); services show OK or FAIL status; messages accessible via dmesg or /var/log/boot.log.
- Init vs systemd: Traditionally init was PID 1; now systemd replaces init in modern systems like Rocky Linux; systemd then starts GDM (Gnome Display Manager) for login prompt.

**Section 2: systemd Services**
- Init Process and Runlevels: Init (PID 1) was the ancestor of all processes; executed shell scripts from /etc/rc.d/init.d; system state divided into 7 runlevels (0-6, plus S).
- systemd Advantages: Socket-based, shell-independent boot, mount control, fsck control, state snapshots, SELinux integration, signal delivery, safe session shutdown.
- systemd Units: systemd manages the system via units (named as service.type), stored as configuration files in /usr/lib/systemd/system and /etc/systemd/system.
- systemctl Command: Used to manage services; can start, stop, restart, and check status of units; unit type suffix can be omitted.
- Viewing Units: systemctl (no args) shows active units; systemctl -a shows all; systemctl -t type filters by type.
- Unit Status: systemctl status servicename shows detailed status (PID, active/inactive).
- Starting/Stopping Services: systemctl start/stop/restart servicename controls services; requires root privileges.
- Target Units: systemd replaces runlevels with target files (graphical.target, multi-user.target, etc.); runlevelX.target files are symlinks for compatibility.
- Default Target: systemctl get-default shows current target; set-default changes default boot target.
- Changing Target: systemctl isolate target changes the current target; init 3 or telinit 3 changes to runlevel 3 (multi-user.target).
- Single-User Mode: systemctl isolate rescue.target switches to single-user mode (runlevel 1) for system repairs; requires root access only.

**Section 3: System Shutdown**
- Shutdown Methods: shutdown command, changing runlevel to 0/6, halt, poweroff, reboot, or power button (last resort only).
- shutdown Command: Most proper shutdown method; offers various options for timing and messaging.
- Immediate Shutdown: shutdown -h now terminates immediately.
- Delayed Shutdown with Message: shutdown -h +minutes "message" gives users time; common practice is shutdown -h +2.
- System Reboot: shutdown -r now for immediate reboot; shutdown -r +minutes schedules reboot.
- Cancel Shutdown: shutdown -c cancels a pending shutdown.
- Message Only: shutdown -k +time sends termination message without actually shutting down (for testing).
- Alt Methods: halt, poweroff, reboot commands offer quick shutdown but less gracefully; runlevel 0 halts, runlevel 6 reboots.

**Section 4: Daemon Processes**
- Daemon Concept: Background services that provide specific functions and respond to requests (systemd manages most modern daemons).

**Section 5: Boot Loader**
- GRUB: Standard Linux bootloader providing menu selection and kernel loading.
- Boot Sequence: BIOS → MBR → Bootloader → Kernel → systemd → Services → Login.

</details>

<details> <summary>KOR (한국어 버전)</summary>

## 7장 – 리눅스의 부팅과 종료

**리눅스 시스템의 부팅**
- 부팅의 정의: 전원 켜짐부터 로그인 프롬프트까지의 과정을 말하며, 하드웨어 부팅과 Linux 부팅 두 단계로 나뉜다.
- BIOS 단계: 전원 켜지면 최초 동작, 하드웨어 상태 확인, 부트 디스크에서 512B의 마스터 부트 레코드(MBR) 로딩, 부트 로더를 메모리에 적재.
- 부트 로더 역할: 디스크에서 리눅스 커널을 찾아 메모리에 로딩하며, 다중 OS 선택 메뉴 제공, GRUB이 표준 부트 로더.
- 커널 초기화: 부트 로더가 커널을 로딩하면 하드웨어 장치 점검, 커널 프로세스·스레드 생성으로 메모리·디바이스 관리 수행, 대괄호[ ]로 표시되고 낮은 PID 할당.
- systemd 서비스 단계: 커널 초기화 후 다양한 시스템 서비스 활성화, 부트 스플래시 이미지 표시(Alt+d로 메시지 전환), 각 서비스 상태(OK/FAIL) 표시, dmesg 명령이나 /var/log/boot.log로 확인 가능.
- Init vs systemd: 전통적으로 init가 PID 1이었으나, Rocky Linux 같은 현대 시스템에서는 systemd로 대체되고, GDM(그놈 디스플레이 매니저)을 실행해 로그인 프롬프트 표시.

**systemd 서비스**
- Init 프로세스와 런레벨: Init는 모든 프로세스의 조상(PID 1), /etc/rc.d/init.d에서 셸 스크립트 실행, 시스템 상태를 7개의 런레벨(0~6, S)로 구분.
- systemd 장점: 소켓 기반, 셸 독립 부팅, 마운트·fsck 제어, 상태 스냅숏, SELinux 통합, 시그널 전달, 안전한 세션 종료.
- systemd 유닛: systemd가 서비스명.종류 형태로 유닛 관리, /usr/lib/systemd/system과 /etc/systemd/system에 설정 파일 저장.
- systemctl 명령: 서비스 시작·종료·재시작·상태 확인에 사용, 유닛 종류 접미사 생략 가능, root 권한 필요.
- 유닛 조회: systemctl (옵션 없음)은 활성 유닛만 표시, -a는 전체, -t type으로 종류별 필터링.
- 유닛 상태: systemctl status 서비스명으로 상세 정보(PID, active/inactive) 확인.
- 서비스 제어: systemctl start/stop/restart 서비스명으로 제어, root 권한 필수.
- Target 유닛: systemd는 런레벨을 target 파일로 대체(graphical.target, multi-user.target 등), runlevelX.target은 호환성을 위한 심볼릭 링크.
- 기본 Target: systemctl get-default로 현재 target 확인, set-default로 기본 부팅 target 변경.
- Target 변경: systemctl isolate target으로 현재 target 전환, init 3이나 telinit 3으로 런레벨 3(multi-user.target) 변경 가능.
- 단일 사용자 모드: systemctl isolate rescue.target으로 단일 사용자 모드(런레벨 1)로 전환해 시스템 점검, root만 접근 가능, reboot나 systemctl default로 다중 사용자 모드 복귀.

**리눅스 시스템의 종료**
- 종료 방법: shutdown 명령, 런레벨 0/6 변경, halt, poweroff, reboot, 전원 버튼(최후의 수단).
- shutdown 명령: 가장 정상적인 종료 방법, 다양한 옵션 제공.
- 즉시 종료: shutdown -h now로 즉시 종료.
- 지연 종료 및 메시지: shutdown -h +분 "메시지"로 시간 확보 후 메시지 전송, shutdown -h +2가 일반적 관행.
- 시스템 재시작: shutdown -r now로 즉시 재부팅, shutdown -r +분으로 예약 재부팅.
- 종료 취소: shutdown -c로 대기 중인 종료 취소.
- 메시지만 전송: shutdown -k +시간으로 실제 종료 없이 메시지만 전송(테스트용).
- 다른 방법: halt·poweroff·reboot 명령으로 빠른 종료 가능하나 우아하지 못함, 런레벨 0(종료), 런레벨 6(재부팅).

**데몬 프로세스**
- 데몬 개념: 특정 서비스를 제공하는 백그라운드 프로세스로, systemd가 대부분의 현대 데몬을 관리.

**부트 로더**
- GRUB: 리눅스의 표준 부트 로더로 OS 선택 메뉴와 커널 로딩 기능 제공.
- 부팅 순서: BIOS → MBR → 부트 로더 → 커널 → systemd → 서비스 → 로그인.

</details>
