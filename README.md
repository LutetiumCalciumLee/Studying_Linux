<details> <summary>ENG (English Version)</summary>

## Chapter 15 – Linux Security Basics

**Section 1: Information Security Fundamentals**
- Information Security Definition: Protects information assets from threats while maintaining Confidentiality (authorized access only), Integrity (data unaltered), and Availability (accessible when needed)—known as the CIA triad.
- Confidentiality: Ensures only authorized users access information through authentication, access controls (read/write permissions), and data encryption.
- Integrity: Guarantees data remains complete and accurate using electronic signatures and verification techniques to detect tampering.
- Availability: Ensures authorized users can access information/services when needed; requires monitoring for attacks, power issues, hardware/software failures.
- Security Practices: Disable unnecessary services/ports (default deny), apply software patches promptly, perform regular system checks (processes, users, disk space), maintain backups, and continuous learning for evolving threats.

**Section 2: System Logs**
- Log Files: Messages from kernel, services, and applications stored primarily in /var/log; used for status monitoring, incident investigation, and intrusion tracking; files owned by root with 600 permissions.
- Major Logs: /var/log/messages (system events), secure (authentication), maillog (mail), cron (scheduled jobs), dmesg (kernel ring buffer); rotated by date to manage size.
- Log Management: Traditional syslog replaced by systemd journal; journalctl views binary journal logs in text format; rsyslog daemon manages some traditional files and coexists with journal.
- rsyslog Configuration: /etc/rsyslog.conf defines rules with filters (facility+priority) and actions (file storage, email, console); filters use facility names (kern, user, mail) and priorities (emerg, alert, crit, err, warning, notice, info, debug).
- journalctl Commands: journalctl (all logs), -n N (last N lines), -o verbose (detailed fields), -f (follow real-time), -p priority (filter by severity), --since/until (time range), -b (current boot), -F field=value (field filter).

**Section 3: Firewall Management**
- Firewall Role: firewalld.service blocks unauthorized network access; prevents attacks proactively unlike logs which are reactive; supports dynamic IPv4/IPv6 management without service restarts.
- GUI Tool: firewall-config (dnf install) manages runtime (temporary) or permanent rules; zones (public, trusted, etc.) control trust levels; services/ports/protocols/ICMP/masquerading/port forwarding configurable.
- CLI Commands: firewall-cmd --state (status), --list-services (allowed services), --add-service=service/--permanent (add), --remove-service=service (remove), --add-port=port/protocol (ports), --reload (apply changes).

**Section 4: Security Management Tools**
- Nmap: Network scanner detects open ports, OS versions; nmap localhost scans local ports; nmap -O IP detects remote OS; nmap -sU scans UDP; nmap 192.168.0.0/24 scans network (install via dnf nmap).
- PAM (Pluggable Authentication Modules): Centralized authentication framework; /etc/pam.d/service files configure modules for auth/account/password/session interfaces with control flags (required, requisite, sufficient, optional).
- PAM Structure: Each line: control_flag module_path [args]; modules in /lib64/security; examples include pam_listfile.so (user blacklisting), pam_shells.so (valid shells), includes other config files.
- SELinux: Security-Enhanced Linux implements Mandatory Access Control (MAC) beyond Discretionary Access Control (DAC); /etc/selinux/config sets enforcing/permissive/disabled and policy type; protects against privilege escalation.

</details>

<details> <summary>KOR (한국어 버전)</summary>

## 15장 – 리눅스 보안의 기초

**정보 보안의 기초**
- 정보 보안 정의: 정보 자산을 위협으로부터 보호해 기밀성(허가된 사용자만 접근), 무결성(데이터 변조 방지), 가용성(필요 시 접근 가능)을 유지하는 것, CIA 삼각형으로 불림.
- 기밀성: 사용자 인증, 접근 제어(읽기/쓰기 권한), 데이터 암호화로 불법 공개/노출 방지.
- 무결성: 데이터의 완전성과 정확성 보장, 전자 서명 등으로 원본 동일성 검증.
- 가용성: 인가된 사용자가 필요 시 정보/서비스 접근 가능, 공격·전력·하드웨어/소프트웨어 결함 대비 주기적 점검 필요.
- 보안 관행: 불필요 서비스/포트 차단(기본 거부), 소프트웨어 패치 즉시 적용, 시스템 점검(프로세스·사용자·디스크 등), 백업 유지, 지속 학습.

**시스템 로그**
- 로그 파일: 커널·서비스·애플리케이션 메시지 저장, 주로 /var/log에 위치; 시스템 상태 확인·사고 조사용, root 소유 600 권한.
- 주요 로그: /var/log/messages(시스템 이벤트), secure(인증), maillog(메일), cron(스케줄), dmesg(커널); 날짜별 로테이션으로 크기 관리.
- 로그 관리: 전통 syslog를 systemd journal 대체, journalctl로 바이너리 로그 텍스트 출력; rsyslog 일부 로그 관리하며 journal과 공존.
- rsyslog 설정: /etc/rsyslog.conf에 필터(기능명+우선순위: kern, user, mail + emerg, crit, err 등)와 동작(파일 저장, 메일, 콘솔) 규칙 정의.
- journalctl 명령: journalctl(전체), -n N(최근 N줄), -o verbose(상세 필드), -f(실시간 추적), -p 우선순위(심각도 필터), --since/until(시간 범위), -b(현재 부팅), -F 필드=값(필드 필터).

**방화벽 관리**
- 방화벽 역할: firewalld.service로 네트워크 접근 차단, 로그와 달리 사전 방어; 동적 IPv4/IPv6 관리로 서비스 재시작 없이 설정 변경 가능.
- GUI 도구: firewall-config(dnf 설치)로 런타임(임시) 또는 영구 설정; 존(public, trusted 등)별 신뢰도 관리, 서비스/포트/프로토콜/ICMP/마스커레이딩/포트포워딩 설정.
- CLI 명령: firewall-cmd --state(상태), --list-services(허용 서비스), --add-service=서비스/--permanent(추가), --remove-service(삭제), --add-port=포트/프로토콜(포트), --reload(적용).

**보안 관리 도구**
- Nmap: 포트·OS 스캔 도구; nmap localhost(로컬 포트), nmap -O IP(원격 OS), nmap -sU(UDP), nmap 192.168.0.0/24(네트워크), dnf nmap으로 설치.
- PAM: 중앙 집중 인증 프레임워크; /etc/pam.d/서비스별 설정 파일에 auth/account/password/session 인터페이스별 모듈과 제어 플래그(required, sufficient 등) 정의.
- PAM 구조: 제어플래그 모듈경로 [인자]; /lib64/security에 모듈, 예: pam_listfile.so(사용자 블랙리스트), pam_shells.so(셸 검증).
- SELinux: 강제 접근 제어(MAC) 구현, DAC 보완; /etc/selinux/config에서 enforcing/permissive/disabled와 정책 타입 설정, 권한 상승 방지.

</details>
