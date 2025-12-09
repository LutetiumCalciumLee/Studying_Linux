<details> <summary>ENG (English Version)</summary>

## Chapter 12 – Remote Access and FTP

**Section 1: Telnet and SSH**
- Telnet Overview: Application-layer protocol and program for remote login that requires both a Telnet client and telnet-server package; on Rocky Linux the Telnet server runs under systemd (telnet.socket) and is blocked by the firewall by default.
- Local and Windows Telnet Use: `telnet 0` or `telnet localhost` connects to the local host; Windows Telnet must be enabled via “Turn Windows features on or off,” and firewall rules must allow port 23, but Korean text is often broken in the default Windows client.
- PuTTY as Telnet Client: PuTTY provides a Windows terminal that supports Telnet, allows UTF‑8 character set selection, and avoids broken Korean output when connecting to Rocky Linux.
- Telnet Security Issue: Telnet transmits all data, including IDs and passwords, in plain text so traffic can be captured and inspected with packet sniffers like tcpdump, exposing especially root passwords.
- SSH Concept: SSH (Secure Shell) offers Telnet-like remote access while encrypting the entire session; Rocky Linux usually ships with OpenSSH server and client, and if not, openssh must be installed and enabled.
- SSH Key Prompt: On first SSH connection the client is asked to trust and store the server’s RSA host key, and once accepted it is reused without prompting on subsequent logins.
- PuTTY as SSH Client: On Windows, selecting “SSH” in PuTTY and specifying the Rocky Linux host/IP allows secure remote login using the same user accounts as on the console.

**Section 2: File Transfer**
- FTP Basics: FTP is a TCP/IP layer‑5 protocol for file transfer that works between Linux and any other OS implementing the FTP standard.
- vsftpd Server Installation: Rocky Linux does not install an FTP server by default; vsftpd must be added with dnf and then configured mainly through /etc/vsftpd/vsftpd.conf.
- vsftpd Operation: After configuration and service start, users can connect with an FTP client, authenticate, and upload or download files subject to vsftpd settings and filesystem permissions.

**Section 3: Mail Sending and Receiving**
- Mail Server Check: A mail server listens on SMTP port 25 and can be tested with Telnet; receiving a “220 …” banner means the server is up and responding.
- mailx / s‑nail Client: Traditional Unix mail client mailx is replaced by s‑nail on CentOS Stream 9/Rocky, and the mailx command is provided as a symbolic link to s‑nail.
- Sending Mail: Running `s-nail user1` prompts for Subject and then mail body; Ctrl+z or Ctrl+c cancels, while Ctrl+d finishes input and sends, and -s sets the subject when sending text from a file via standard input redirection.
- Mail Storage and Reading: Incoming mail is stored under /var/spool/mail/username, and invoking s‑nail with no arguments opens the inbox where internal commands let users read messages, reply (r), delete (d), undelete, and quit with q or x.

</details>

<details> <summary>KOR (한국어 버전)</summary>

## 12장 – 원격 접속과 FTP

**텔넷과 SSH**
- 텔넷 개요: 원격 로그인을 위한 응용 계층 프로토콜이자 프로그램으로, 텔넷 클라이언트와 telnet-server 패키지가 모두 필요하며 Rocky Linux에서는 systemd의 telnet.socket으로 동작하고 방화벽에서 기본 차단된다.
- 로컬·윈도 텔넷 사용: `telnet 0` 또는 `telnet localhost`로 로컬 접속이 가능하고, 윈도에서는 “Windows 기능 켜기/끄기”에서 텔넷 클라이언트를 활성화한 뒤 방화벽에서 23번 포트를 허용해야 하지만, 기본 클라이언트는 한글이 깨지기 쉽다.
- PuTTY 텔넷 클라이언트: PuTTY는 텔넷을 지원하는 윈도 터미널 프로그램으로, 기본 문자 집합을 UTF‑8로 설정해 Rocky Linux에 접속해도 한글이 깨지지 않는다.
- 텔넷 보안 문제: 텔넷은 ID·패스워드를 포함한 모든 데이터가 평문으로 전송되므로 tcpdump 같은 패킷 캡처 도구로 쉽게 가로챌 수 있어, 특히 root 암호 유출 위험이 크다.
- SSH 개념: SSH(Secure Shell)는 텔넷과 동일하게 원격 접속을 제공하면서 전체 세션을 암호화하며, Rocky Linux에는 보통 OpenSSH 서버·클라이언트가 포함되어 있지 않다면 설치 후 활성화해야 한다.
- SSH 키 프롬프트: SSH로 처음 접속하면 RSA 호스트 키를 신뢰·저장할지 묻고, 한 번 등록하면 이후에는 같은 키를 자동으로 사용해 서버를 검증한다.
- PuTTY SSH 접속: 윈도에서는 PuTTY에서 접속 형식으로 “SSH”를 선택하고 Rocky Linux 호스트/IP를 지정해 콘솔 로그인과 동일한 계정으로 안전하게 접속할 수 있다.

**파일 송수신**
- FTP 기본: FTP는 TCP/IP 5계층에 속하는 파일 전송 프로토콜로, 이를 구현한 다른 운영체제와도 파일을 주고받을 수 있다.
- vsftpd 서버 설치: Rocky Linux에는 FTP 서버가 기본 설치되어 있지 않으므로 dnf로 vsftpd 패키지를 설치한 뒤 /etc/vsftpd/vsftpd.conf 파일에서 주요 설정을 변경한다.
- vsftpd 동작: 설정과 서비스 기동이 끝나면 FTP 클라이언트가 접속·인증을 거쳐, vsftpd 설정과 파일 시스템 권한이 허용하는 범위에서 파일 업로드·다운로드를 수행한다.

**메일 송수신**
- 메일 서버 점검: 메일 서버는 SMTP 25번 포트에서 대기하며, 텔넷으로 접속했을 때 “220 …” 배너가 출력되면 정상 동작 중으로 판단할 수 있다.
- mailx / s‑nail 클라이언트: 전통적인 mailx 메일 클라이언트는 Rocky에서 s‑nail 패키지로 대체되며, mailx 명령은 s‑nail에 대한 심볼릭 링크로 제공된다.
- 메일 보내기: `s-nail user1`처럼 실행하면 Subject(제목)와 본문을 입력한 뒤 Ctrl+d로 메일을 전송하며, -s 옵션과 표준 입력 리다이렉션을 이용해 파일에 작성한 본문을 제목과 함께 전송할 수 있다.
- 메일 저장·읽기: 수신 메일은 /var/spool/mail/사용자명에 저장되고, 인자 없이 s‑nail을 실행하면 받은 편지함이 열리며, 내부 명령으로 읽기, 답장(r), 삭제(d), undelete, 종료(q/x) 등을 수행해 메일을 관리할 수 있다.

</details>

