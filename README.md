<details> <summary>ENG (English Version)</summary>

## Chapter 16 – Virtualization Services

**Section 1: Virtualization Service Overview**
- Virtualization Concept: Divides physical resources (CPU, memory, disk) into multiple virtual resources or aggregates multiple physical resources into a single virtual system.
- Virtualization Types: Virtual Machines (VMs—full OS isolation, e.g., VMware Player), Container Virtualization (app-level isolation, e.g., Docker/Kubernetes), Network Virtualization (VPNs), Storage Virtualization (LVM).
- Use Cases: Improves resource utilization, enables diverse OS environments, provides scalability, reduces costs (hardware, power, space).
- Hypervisor Type 1: Bare-metal (direct hardware access)—VMware vSphere/ESXi, Hyper-V, Xen, KVM; Full Virtualization (no guest OS mods, slower via DOM0 mediation), Paravirtualization (hypercalls, faster but guest mods needed).
- Hypervisor Type 2: Hosted (runs on host OS)—VMware Workstation, VirtualBox; I/O goes through host OS causing performance overhead.
- Container Advantages: Lightweight (shares host kernel, no guest OS), portable (isolated environments), high performance (direct resource access).

**Section 2: Virtual Machine Practice**
- KVM Overview: Kernel-based Virtual Machine (Linux kernel 2.6.20+); Type 1 hypervisor requiring CPU virtualization (Intel VT-x/AMD-V); uses KVM (kernel module), QEMU (emulator), Virt-Manager (GUI).
- KVM Setup: Enable CPU virtualization in BIOS/VM settings; install KVM/QEMU/Virt-Manager packages (+EPEL repo); verify lsmod | grep kvm; start libvirtd service; create network bridge (br0).
- Bridge Network: nmcli creates br0 bridge (ens160 slave), assigns IP/gateway/DNS; virbr0.xml enables bridge for VMs; restart libvirtd.
- VM Creation: virt-manager GUI—select Rocky Linux ISO, set RAM/CPU/disk (10GB), customize name; installs guest OS like physical machine.
- Cockpit Console: Web-based management (dnf install cockpit cockpit-machines); access https://IP:9090; manages firewall, users, network, VMs, updates, containers, logs, monitoring.

**Section 3: Container Virtualization Practice**
- Docker: Container platform; Docker Image (packaged app+runtime), Docker Hub (hub.docker.com repository).
- Docker Install: Add CentOS Docker repo, dnf install docker-ce, systemctl enable/start docker; docker --version verifies.
- Docker Test: docker run hello-world confirms operation; docker pull nginx downloads image; docker run -p 9511:80 nginx maps port.
- Docker Commands: docker images (list images), docker ps (running containers), docker pull/run for deployment.
- Conda: Python environment manager; download Miniconda, bash installer, conda --version; create env (conda create -n yolo_env python=3.10), activate/deactivate, pip install ultralytics.
- YOLO Example: detection.py uses YOLOv8 for object detection on images (test.jpg → result_output.jpg), prints classes/confidence.

</details>

<details> <summary>KOR (한국어 버전)</summary>

## 16장 – 가상화 서비스

**가상화 서비스 개요**
- 가상화 개념: 물리 자원(CPU·메모리·디스크)을 여러 가상 자원으로 분할하거나 여러 물리 자원을 하나의 가상 시스템으로 통합.
- 가상화 유형: 가상머신(VM—전체 OS 격리, VMware Player), 컨테이너 가상화(앱 수준 격리, Docker/Kubernetes), 네트워크 가상화(VPN), 스토리지 가상화(LVM).
- 활용 용도: 자원 활용도 향상, 다양한 OS 환경 구축, 확장성(트래픽 대응), 비용 절감(하드웨어·전력·공간).
- 하이퍼바이저 유형 1: 베어메탈(직접 하드웨어 접근)—vSphere/ESXi, Hyper-V, Xen, KVM; 전가상화(게스트 OS 수정 불필요, DOM0 중재로 느림), 반가상화(하이퍼콜, 빠름 but 수정 필요).
- 하이퍼바이저 유형 2: 호스트 기반(호스트 OS 위)—Workstation, VirtualBox; I/O가 호스트 OS 경유로 성능 저하.
- 컨테이너 장점: 경량(호스트 커널 공유), 이식성(격리 환경), 고성능(직접 자원 접근).

**가상머신 실습**
- KVM 개요: 리눅스 커널 가상화 모듈(2.6.20+), 유형 1 하이퍼바이저(VT-x/AMD-V 필수); KVM(커널), QEMU(에뮬레이터), Virt-Manager(GUI).
- KVM 구축: BIOS/VM에서 가상화 활성화, KVM/QEMU/Virt-Manager 설치(EPEL 저장소), lsmod | grep kvm 확인, libvirtd 서비스 시작, 네트워크 브릿지(br0) 생성.
- 브릿지 네트워크: nmcli로 br0 생성(ens160 슬레이브), IP/게이트웨이/DNS 설정, virbr0.xml 활성화, libvirtd 재시작.
- VM 생성: virt-manager에서 Rocky ISO 선택, RAM/CPU/디스크(10GB) 설정, 이름 지정 후 물리 설치와 동일하게 진행.
- Cockpit 콘솔: 웹 관리(dnf cockpit cockpit-machines), https://IP:9090 접속; 방화벽·사용자·네트워크·VM·업데이트·컨테이너·로그·모니터링.

**컨테이너 가상화 실습**
- 도커: 컨테이너 플랫폼; 도커 이미지(앱+런타임 패키지), 도커 허브(hub.docker.com).
- 도커 설치: CentOS 저장소 추가, dnf docker-ce, systemctl docker 활성화/시작, docker --version 확인.
- 도커 테스트: docker run hello-world(동작 확인), docker pull nginx(이미지 다운), docker run -p 9511:80 nginx(포트 매핑).
- 도커 명령: docker images(이미지 목록), docker ps(실행 컨테이너), pull/run으로 배포.
- Conda: Python 환경 관리; Miniconda 다운로드·설치, conda --version; conda create -n yolo_env python=3.10, activate/deactivate, pip ultralytics.
- YOLO 예제: detection.py로 YOLOv8 객체 감지(test.jpg → result_output.jpg), 클래스·신뢰도 출력.

</details>
