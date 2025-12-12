<details> <summary>ENG (English Version)</summary>

## Chapter 14 – NFS and Samba

**Section 1: NFS Installation and Operation**
- NFS Overview: NFS (Network File System) connects disks from remote systems via network and mounts them into the local directory hierarchy; requires an NFS server to export directories and clients to mount them.
- NFS Package: nfs-utils package is included by default on Rocky Linux; verify with rpm -qa or install with dnf if missing.
- Server Configuration: NFS server exports directories in /etc/exports file; each line specifies exported directory and client addresses (hostname, IP, or wildcard *); exporting makes directory available to specified clients.
- Server Setup: Create share directory (/home/share) with 707 permissions; add entry to /etc/exports; run exportfs -ra to apply; start nfs-server.service; open nfs port in firewall.
- exportfs Command: exportfs -ra re-exports all entries in /etc/exports; exportfs -o exports current list without saving to file.
- Client Mount: Use mount serverIP:/share /mnt to connect; df -h shows NFS mount; files created on server appear on client and vice versa.
- Persistent Mount: Add NFS entries to /etc/fstab for automatic mounting on boot; common NFS options include rw (read-write), ro (read-only), async, hard, soft, intr.
- showmount Command: showmount -e serverIP displays exported directories from NFS server; requires firewall ports to be open on server side.

**Section 2: Samba Installation and Operation**
- Samba Overview: Samba enables directory and printer sharing between Windows and Linux; two scenarios: (1) Linux accesses Windows shares (Linux=Samba client, Windows=Samba server), (2) Windows accesses Linux shares (Linux=Samba server, Windows accesses via network drive).
- Windows Share Setup: Create folder (C:\SambaWin), share via Properties>Share>Advanced Share, add "Everyone" user with read/write permissions.
- Windows Share User: Create Windows user account (e.g., root) and set password for Samba authentication.
- Linux Samba Client: Install samba-client and samba-common packages; use smbclient -L //windowsIP -U windowsUser to list shares; create mount point and mount with cifs (requires cifs-utils).
- Mount Windows Share: mount -t cifs //windowsIP/sharename /mountpoint -o username=user,password=pass; cifs filesystem type; verify with df and file operations.
- Linux Samba Server: Install samba package; configure /etc/samba/smb.conf with workgroup, server string, and share sections; each share specifies path, comment, and permissions (public, writable).
- Start Services: Start smb.service and nmb.service; open Samba ports in firewall; disable SELinux if access denied.
- User Access: Set Samba password for Linux user with smbpasswd username (separate from Linux password); users authenticate with this password when accessing.
- Windows Network Drive: Explorer > Network > Map network drive, enter \\linuxIP\sharename or \\linuxIP\username (for user home), authenticate with Samba credentials; drive appears as network location.
- Linux Samba Client: smbclient //linuxIP/username -U user connects to Samba share; use ls to list files, get/put for transfers.

</details>

<details> <summary>KOR (한국어 버전)</summary>

## 14장 – NFS와 삼바

**NFS 설치와 운영**
- NFS 개요: NFS(Network File System)는 네트워크를 통해 원격 시스템의 디스크를 연결해 로컬 디렉터리 구조에 마운트하는 방식이며, NFS 서버가 디렉터리를 공유하고 클라이언트가 마운트.
- NFS 패키지: nfs-utils 패키지는 Rocky Linux에 기본 설치되어 있으며, rpm -qa로 확인하거나 dnf로 설치.
- 서버 설정: /etc/exports 파일에서 공유 디렉터리와 클라이언트 주소(호스트명, IP, 와일드카드 *)를 지정하는 방식으로 설정.
- 서버 구축: /home/share 디렉터리 생성(권한 707), /etc/exports에 항목 추가, exportfs -ra로 적용, nfs-server.service 시작, 방화벽에서 nfs 포트 열기.
- exportfs 명령: exportfs -ra는 /etc/exports의 모든 항목 재적용, exportfs -o는 현재 공유 목록 표시.
- 클라이언트 마운트: mount serverIP:/share /mnt로 연결, df -h로 NFS 마운트 확인, 양쪽 모두에서 파일 생성 및 확인 가능.
- 영구 마운트: /etc/fstab에 NFS 항목 추가해 부팅 시 자동 마운트, rw(읽기/쓰기), ro(읽기전용), async, hard, soft, intr 등의 NFS 옵션 사용.
- showmount 명령: showmount -e serverIP로 NFS 서버의 공유 디렉터리 확인, 서버 방화벽에서 포트 개방 필요.

**삼바 설치와 운영**
- 삼바 개요: 리눅스에서 윈도 디렉터리·프린터 공유 시 사용하는 프로토콜로, ① 리눅스가 삼바 클라이언트(윈도 공유 접속), ② 리눅스가 삼바 서버(윈도에서 리눅스 공유 접속) 두 가지 방식.
- 윈도 공유 설정: C:\SambaWin 폴더 생성, 속성>공유>고급 공유에서 "선택한 폴더 공유" 체크, "Everyone" 사용자에게 읽기/쓰기 권한 부여.
- 윈도 공유 사용자: 윈도 계정 추가(예: root) 후 암호 설정해 삼바 인증용 자격 증명 제공.
- 리눅스 삼바 클라이언트: samba-client, samba-common 패키지 설치, smbclient -L //윈도IP -U 윈도사용자로 공유 목록 확인, 마운트 포인트 생성 후 cifs 파일 시스템으로 마운트(cifs-utils 필수).
- 윈도 공유 마운트: mount -t cifs //윈도IP/공유명 /마운트포인트 -o username=user,password=pass; cifs 파일 시스템 타입 사용, df로 확인 및 파일 작업 가능.
- 리눅스 삼바 서버: samba 패키지 설치, /etc/samba/smb.conf에서 workgroup, server string, 공유 섹션(경로, 설명, 공개 여부, 쓰기 가능 여부) 설정.
- 서비스 시작: smb.service, nmb.service 시작, 방화벽에서 삼바 포트 열기, 접근 거부 시 SELinux 해제.
- 사용자 접근: smbpasswd 사용자명으로 삼바 암호 설정(리눅스 암호와 별도), 접속 시 이 암호로 인증.
- 윈도 네트워크 드라이브: 탐색기>네트워크>네트워크 드라이브 연결에서 \\리눅스IP\공유명 또는 \\리눅스IP\사용자명 입력, 삼바 자격 증명으로 인증 후 네트워크 위치로 표시.
- 리눅스 삼바 클라이언트: smbclient //리눅스IP/사용자명 -U 사용자로 삼바 공유 연결(프롬프트 smb: \>), ls로 파일 목록, get/put으로 파일 전송.

</details>
