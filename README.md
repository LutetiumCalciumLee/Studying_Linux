<details> <summary>ENG (English Version)</summary>

## Chapter 11 – Network Configuration

**Section 1: Network Basics**
- TCP/IP Protocol: 5-layer communication standard; layers perform distinct roles using various supporting protocols; TCP (transport) and IP (network) represent the whole suite.
- MAC Address: Hardware address (48-bit, colon/hyphen-separated hex); first 3 octets = manufacturer (IEEE-assigned), last 3 = serial number; immutable in most NICs.
- IP Address: 32-bit (4 bytes); identifies computers on internet; divided into network (prefix) and host portions based on class (A/B/C); IPv4 exhausted, IPv6 developed.
- IP Classes: Class C common—first 3 bytes network, last byte host (1–254 usable after 0=network, 255=broadcast); CIDR notation replaces classes (/24 = 255.255.255.0).
- Netmask/Broadcast: Netmask isolates network portion via AND operation (C-class default 255.255.255.0); broadcast sends to all on network (host portion all 1s).
- Hostname: Hierarchical name (domain.host); used for human recognition; server computers require meaningful hostnames; DNS maps hostnames to IPs.
- Port Number: Distinguishes services on same IP (Layer 4, transport); defined in /etc/services file; standard ports (22=SSH, 80=HTTP, 443=HTTPS); custom apps use non-standard ports.

**Section 2: Network Configuration**
- Settings Required: IP address, netmask/broadcast, gateway (router), DNS; must obtain from network administrator; one error breaks connectivity.
- NetworkManager: Daemon managing network; stores settings in connection profiles; CLI tools (nmcli), GUI (Settings>Network, nm-connection-editor) interface with it.
- nmcli: Command-based tool for network management; subcommands: networking (on/off), connection (show/add/modify/delete/up/down), device (status/show).
- nmcli connection: Add (fixed IP with IPv4 CIDR), show (list profiles), up/down (activate/deactivate), modify (change settings with +/- for add/remove), delete (remove profile).
- ip Command: Lower-level network tool; changes don't persist on reboot unless in config files; address (show/add/del), route (show/add/del), link (up/down).
- ifconfig: Traditional interface config; shows/sets IP, netmask, broadcast; down/up to disable/enable; manual IP set format: `ifconfig ens160 192.168.147.130 netmask 255.255.255.0`.
- route Command: Manages routing table; add default via gateway, add destination via gateway; show displays routes; del removes.
- DNS: Domain Name Service maps hostnames to IPs; configured in /etc/resolv.conf (nameserver) or via nmcli; nslookup queries DNS servers.

**Section 3: Hostname Configuration**
- Hostname Output: uname -n, hostname, hostnamectl show—display system hostname (default localhost.localdomain).
- Hostname Set: hostname newname (temporary), hostnamectl set-hostname newname (persistent to /etc/hostname), nmcli gen hostname newname.
- /etc/hostname: File storing persistent hostname; must be unique on same network; changing requires network admin coordination.

**Section 4: Network Status Verification**
- ping: Tests connectivity; -c count limits packets; can use IP or domain; shows packet loss, round-trip times (min/avg/max).
- netstat: Network statistics; -r shows routing table, -p shows process using port, -i shows interface stats, -s shows protocol stats.
- Ports: LISTEN state indicates active service; netstat -tan shows TCP connections; well-known ports (22, 80, 443, 3306, etc.).
- arp: Address Resolution Protocol; maps MAC to IP on same network; shows connected systems.
- tcpdump: Packet capture tool; -c count, -w file saves to binary file, -r file reads captures, -X shows ASCII content, tcp port N filters by port.
- tcpdump Output: Shows source/destination, protocol, packet flags; binary format requires -w save, -r read, or -X for text; powerful but security-sensitive (data exposure).

</details>

<details> <summary>KOR (한국어 버전)</summary>

## 11장 – 네트워크 설정

**네트워크 기초**
- TCP/IP 프로토콜: 5계층 통신 표준으로, 계층별로 고유 역할 수행 및 다양한 프로토콜 지원; TCP(전송 계층)와 IP(네트워크 계층)가 전체 대표.
- MAC 주소: 하드웨어 주소(48비트, 콜론/하이픈 16진수); 앞 3옥텟=제조사(IEEE 지정), 뒤 3옥텟=일련번호; 대부분 NIC에서 불변.
- IP 주소: 32비트(4바이트)로 인터넷의 컴퓨터 식별; 네트워크 부분과 호스트 부분으로 분리(클래스 A/B/C에 따라 다름); IPv4 고갈, IPv6 개발됨.
- IP 클래스: C 클래스 일반적—앞 3바이트 네트워크, 뒤 1바이트 호스트(0=네트워크, 255=브로드캐스트, 1~254 할당 가능); CIDR 표기(/24=255.255.255.0).
- 넷마스크/브로드캐스트: 넷마스크는 AND 연산으로 네트워크 부분 추출(C 클래스 기본값 255.255.255.0); 브로드캐스트는 같은 네트워크의 모든 호스트에 메시지 전송(호스트 부분 모두 1).
- 호스트 이름: 계층식 이름(도메인.호스트)으로 인간 친화적; 서버 시스템은 의미 있는 호스트명 필수; DNS가 호스트명을 IP로 매핑.
- 포트 번호: 같은 IP에서 서비스 구분(계층 4 전송 계층); /etc/services에 정의; 표준 포트(22=SSH, 80=HTTP, 443=HTTPS); 커스텀 앱은 비표준 포트 사용.

**네트워크 설정**
- 필수 설정: IP 주소, 넷마스크/브로드캐스트, 게이트웨이(라우터), DNS; 반드시 네트워크 관리자에게 받아야 함; 하나라도 틀리면 연결 실패.
- NetworkManager: 네트워크 관리 데몬으로 연결 프로파일에 설정 저장; CLI 도구(nmcli), GUI(설정>네트워크, nm-connection-editor) 인터페이스 제공.
- nmcli: 명령 기반 네트워크 도구; 서브명령: networking(on/off), connection(show/add/modify/delete/up/down), device(status/show).
- nmcli connection: add(고정 IPv4 CIDR 지정), show(프로파일 목록), up/down(활성화/비활성화), modify(+/-로 추가/제거 설정), delete(프로파일 삭제).
- ip 명령: 저수준 네트워크 도구로, 변경사항이 부팅 후 지속되지 않음(설정 파일에 저장 필요); address(show/add/del), route(show/add/del), link(up/down).
- ifconfig: 전통적 인터페이스 설정 명령; IP·넷마스크·브로드캐스트 표시/설정; down/up으로 비활성화/활성화; 수동 IP 설정: `ifconfig ens160 192.168.147.130 netmask 255.255.255.0`.
- route 명령: 라우팅 테이블 관리; add default via 게이트웨이, add 목적지 via 게이트웨이; show 경로 확인; del 삭제.
- DNS: 도메인명을 IP로 매핑하는 서비스; /etc/resolv.conf(nameserver) 또는 nmcli로 설정; nslookup으로 DNS 서버 질의.

**호스트 이름 설정**
- 호스트 이름 출력: uname -n, hostname, hostnamectl show로 시스템 호스트명 확인(기본값 localhost.localdomain).
- 호스트 이름 설정: hostname 새이름(임시), hostnamectl set-hostname 새이름(/etc/hostname에 영구 저장), nmcli gen hostname 새이름.
- /etc/hostname: 영구 호스트명 저장 파일로, 같은 네트워크에서 유일해야 함; 변경 시 네트워크 관리자와 협의 필수.

**네트워크 상태 확인**
- ping: 연결 테스트; -c 카운트로 패킷 수 제한; IP 또는 도메인명 사용 가능; 패킷 손실, 왕복 시간(최소/평균/최대) 표시.
- netstat: 네트워크 통계; -r로 라우팅 테이블, -p로 포트 사용 프로세스, -i로 인터페이스 통계, -s로 프로토콜별 통계 확인.
- 포트: LISTEN 상태는 서비스 활성 표시; netstat -tan으로 TCP 연결 확인; 잘 알려진 포트(22, 80, 443, 3306 등).
- arp: 주소 결정 프로토콜로 같은 네트워크의 MAC과 IP 매핑; 연결된 시스템 표시.
- tcpdump: 패킷 캡처 도구; -c 카운트, -w 파일로 바이너리 저장, -r 파일로 읽기, -X로 ASCII 표시, tcp port N으로 포트 필터링.
- tcpdump 출력: 송수신처·프로토콜·패킷 플래그 표시; 바이너리 형식으로 -w 저장, -r 읽기 또는 -X 텍스트 필요; 보안 민감(데이터 노출 위험).

</details>
