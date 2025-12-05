<details> <summary>ENG (English Version)</summary>

## Chapter 10 – File Systems and Disk Management

**Section 1: Linux File System Types**
- File System Definition: Structured method for managing files and directories; Linux supports various types based on internal organization.
- ext Evolution: ext (1992, 2GB max, 255B filenames), ext2 (1993, 32TB max, standard until ext3), ext3 (2001, journaling for crash recovery), ext4 (2008, 1EB volumes, 16TB files, online defrag, 64K subdirs).
- XFS: High-performance journaling FS by SGI (1993), 16EB max, default for Rocky Linux; Ubuntu uses ext4.
- Other FS: Supports Unix/Windows compatibility (FAT, NTFS, ISO9660) and virtual FS (proc, sysfs, tmpfs) for special purposes.
- Supported FS Check: /proc/filesystems lists kernel-supported FS; "nodev" indicates virtual/memory-based FS.

**Section 2: Linux File System Structure**
- Core Concepts: Files managed by inodes; directories are files containing name:inode lists; devices accessed via special files.
- ext4 Structure: Disk divided into block groups (typically 4KB blocks); Group 0 has superblock/group descriptor; others have copies or start with bitmaps.
- Components: Data/inode bitmaps track usage; inode table stores file metadata (type, permissions, size, timestamps, owner); data blocks hold content or dir listings.
- Single vs Multiple FS: Entire hierarchy as one FS at /, or split across /, /usr, /home for isolation (root FS safest).

**Section 3: File System Mounting**
- Mount Concept: Connects FS to directory hierarchy; mount point is connection directory (e.g., / for root).
- /etc/fstab: Auto-mount config with 6 fields—device (UUID preferred), mount point, FS type (ext4/xfs), options (defaults), dump (0), fsck order (0).
- mount/umount: mount shows current mounts (/etc/mtab); mount /dev/sdX /mnt connects; umount /mnt disconnects (fails if busy).
- USB Mounting: Linux USB auto-recognized as /dev/sdX; Windows FAT32 uses vfat, NTFS uses ntfs; manual mount after umount if auto-mounted.

**Section 4: Adding Disks**
- VM Disk Addition: VMware adds NVMe/SCSI disks via settings; NVMe naming /dev/nvme0nXpY (controller:ns:partition).
- fdisk Partitioning: fdisk -l lists disks; n creates partitions (p=primary, +sizeM); t sets type (83=Linux, 8e=LVM, fd=RAID); w writes changes.
- FS Creation: mkfs -t ext4 /dev/nvme0nXp1 or mke2fs -t ext4 formats; shows block/inode counts, superblock backups.
- LVM: PV (physical volumes), VG (volume groups combine PVs), LV (logical volumes from VG); pvcreate/vgcreate/lvcreate; flexible resizing.
- RAID: Software RAID via mdadm; RAID0 stripes across disks for speed (no redundancy); mdadm --create /dev/md0 --level=0 --raid-devices=2 /dev/sdX /dev/sdY.

**Section 5: Disk Management**
- df/du: df -hT shows FS usage (total/used/free/%/type); du -sh /dir summarizes directory usage.
- fsck/e2fsck: Checks/repairs FS (unmounted); fsck -f forces check; e2fsck -y auto-repairs; badblocks detects bad sectors.
- Recovery: dumpe2fs finds backup superblocks; e2fsck -b backup_location recovers corrupted primary superblock.
- Swap: swapon/swappoff manages swap space; mkswap formats swap files/partitions; fallocate creates swap files for memory extension.

**Section 6: Disk Quotas**
- Quota Types: Per-user (usrquota) or group (grpquota); soft (grace period) vs hard limits (absolute max) for blocks/inodes.
- Setup: Add quota options to /etc/fstab, remount, quotacheck creates aquota.user/.group, quotaon activates.
- Management: edquota edits limits; quota shows usage/grace; edquota -p copies settings; supports journaling (jqfmt=vfsv0).

</details>

<details> <summary>KOR (한국어 버전)</summary>

## 10장 – 파일 시스템과 디스크 관리

**리눅스 파일 시스템 종류**
- 파일 시스템 정의: 파일·디렉터리를 구조적으로 관리하는 체계; 내부 구조에 따라 다양한 형식 존재.
- ext 계열 발전: ext(1992, 2GB 최대, 255B 파일명), ext2(1993, 32TB 최대, ext3 전 표준), ext3(2001, 저널링으로 충돌 복구), ext4(2008, 1EB 볼륨, 16TB 파일, 온라인 조각모음, 64K 서브디렉터리).
- XFS: SGI 개발 고성능 저널링 FS(1993), 16EB 최대, Rocky Linux 기본; Ubuntu는 ext4 기본.
- 기타 FS: Unix/Windows 호환(FAT, NTFS, ISO9660) 및 가상 FS(proc, sysfs, tmpfs) 지원.
- 지원 FS 확인: /proc/filesystems로 커널 지원 FS 목록; "nodev"는 가상/메모리 기반 FS 표시.

**리눅스 파일 시스템 구조**
- 핵심 개념: 파일은 inode 관리, 디렉터리는 이름:inode 목록 파일, 장치는 특수 파일로 접근.
- ext4 구조: 디스크를 블록 그룹(일반 4KB)으로 구분; 그룹 0은 슈퍼블록/그룹 디스크립터 포함, 나머지는 복사본 또는 비트맵부터 시작.
- 구성 요소: 데이터/inode 비트맵(사용 여부), inode 테이블(파일 메타데이터: 종류·권한·크기·시간·소유자), 데이터 블록(내용 또는 디렉터리 목록).
- 단일 vs 다중 FS: 전체를 /에 하나의 FS로 구성하거나 /, /usr, /home 등 분리(루트 FS 안전).

**파일 시스템 마운트**
- 마운트 개념: FS를 디렉터리 계층에 연결; 마운트 포인트는 연결 디렉터리(/는 루트).
- /etc/fstab: 자동 마운트 설정(6필드: 장치 UUID, 마운트포인트, FS종류 ext4/xfs, 옵션 defaults, 덤프 0, fsck 순서 0).
- mount/umount: mount으로 현재 마운트 확인(/etc/mtab); mount /dev/sdX /mnt 연결; umount /mnt 해제(busy면 디렉터리 이동 후 재시도).
- USB 마운트: Linux USB는 /dev/sdX로 인식; Windows FAT32는 vfat, NTFS는 ntfs; 자동 마운트 후 수동 umount.

**디스크 추가 설치**
- VM 디스크 추가: VMware 설정에서 NVMe/SCSI 추가; NVMe 명명 /dev/nvme0nXpY(컨트롤러:ns:파티션).
- fdisk 파티션: fdisk -l 디스크 목록; n으로 파티션 생성(p=기본, +sizeM); t로 타입 변경(83=Linux, 8e=LVM, fd=RAID); w 저장.
- FS 생성: mkfs -t ext4 /dev/nvme0nXp1 또는 mke2fs -t ext4 포맷; 블록/inode 수, 슈퍼블록 백업 위치 표시.
- LVM: PV(물리 볼륨), VG(PV 그룹화), LV(VG에서 논리 볼륨); pvcreate/vgcreate/lvcreate; 크기 유연 조정.
- RAID: mdadm 소프트웨어 RAID; RAID0은 병렬 스트라이핑으로 속도 향상(중복 없음); mdadm --create /dev/md0 --level=0 --raid-devices=2.

**디스크 관리**
- df/du: df -hT로 FS 사용량(전체/사용/여유/%/종류); du -sh /dir로 디렉터리 사용량 요약.
- fsck/e2fsck: FS 검사·복구(언마운트 상태); fsck -f 강제 검사; e2fsck -y 자동 복구; badblocks 배드 섹터 검사.
- 복구: dumpe2fs로 백업 슈퍼블록 위치 확인; e2fsck -b 백업위치로 기본 슈퍼블록 복구.
- 스왑: swapon/swappoff 관리; mkswap 포맷; fallocate로 스왑 파일 생성해 메모리 확장.

**디스크 사용량(쿼터) 설정**
- 쿼터 유형: 사용자(usrquota)/그룹(grpquota); 소프트(유예기간) vs 하드(절대 최대) 제한(블록/아이노드).
- 설정: /etc/fstab에 쿼터 옵션 추가, 리마운트, quotacheck으로 aquota.user/.group 생성, quotaon 활성화.
- 관리: edquota로 제한 편집; quota로 사용량/유예 확인; edquota -p 설정 복사; 저널링 지원(jqfmt=vfsv0).

</details>
