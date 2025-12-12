<details> <summary>ENG (English Version)</summary>

## Chapter 13 – Database Server and Web Server

**Section 1: Database**
- Database Definition: A database (DB) is an organized collection of related data that minimizes redundancy and maintains structured relationships among data elements.
- Relational Database: Data is represented as tables (rows and columns), providing flexibility in table creation and field combination/separation.
- Key Terminology: Data (values stored in each item), Table (data organized in rows and columns with a name), Database (related tables organized together with a name), Field (table column; also called column), Record (one row of data; also called tuple), Key (field value that uniquely identifies each record; cannot have duplicates).
- SQL Basics: SQL is the language for creating relational databases, creating tables, inserting/deleting/modifying data; each SQL statement ends with semicolon; SQL is case-insensitive by default.
- Database SQL: Show databases lists existing DBs; Create database dbname creates new DB; Drop database dbname deletes DB and all its tables; Use dbname selects a working database.
- Table SQL: Show tables lists existing tables; Create table with field name and datatype; Describe (or Explain) table shows table structure; Alter table can add/modify/drop fields or add primary keys; Drop table deletes the table.
- Record Operations: Insert into inserts new record(s); Update modifies existing record(s) based on conditions; Delete removes record(s); Select retrieves record(s) with optional where clauses and joins.
- Joins: Multiple tables can be queried together using common key fields (usually primary keys) to retrieve related data across tables, called a join operation.
- Access Control: Grant statement assigns database permissions to users; administrators create databases and grant all privileges on them to regular users.

**Section 2: MariaDB Installation and Use**
- Installation: MariaDB is installed via dnf with the mariadb-server package; the daemon is named mariadb.service and the daemon process runs as user mysql for compatibility.
- Access: Use mariadb or mysql command to connect; default prompt is "MariaDB [(none)]>" and exit quits the client.
- Database Creation: Show databases lists built-in databases (information_schema, etc.); Create database st_db creates new database; Use st_db selects database for work.
- Table Creation: Create table st_info (ST_ID int, NAME varchar(20), DEPT varchar(25)) default charset=utf8; define field names and types; charset=utf8 prevents Korean corruption.
- Primary Key: Alter table tablename modify field int Not Null allows non-null values; Alter table ... add constraint name primary key (field) adds primary key constraint.
- Records: Insert into tablename values (...) adds records; Select * from table displays all records; Select col from table where condition retrieves specific data; Update tablename set col=val where condition modifies records.
- Management: mariadb-admin status shows server status (uptime, threads, queries, etc.); mariadb-admin version displays version; mariadb-admin password sets root password.

**Section 3: Web Server Installation and Use**
- Apache Installation: httpd package installed via dnf; httpd.service is the daemon; ps shows multiple httpd processes running.
- Apache Activation: Systemctl start httpd starts the server; firewall must allow http service; default directory is /var/www/html (accessible via http://IP).
- Web Pages: HTML files in /var/www/html are served directly; create index.html to replace default page.
- User Web Pages: /etc/httpd/conf.d/userdir.conf enables user web pages; comment out "UserDir disabled" and set "UserDir public_html" to allow users to host pages in ~/public_html directory (accessible via http://IP/~username).
- User Permissions: User must create public_html directory with 755 permissions (chmod 755 public_html); files within need proper permissions; may need to disable SELinux if access is denied.
- APM Stack: Apache + PHP + MariaDB (formerly MySQL) creates APM; install php, php-gd, php-mysqlnd packages; restart httpd after PHP install.
- PHP Testing: Create phpinfo.php file with <?php phpinfo(); ?> and access via http://IP/phpinfo.php to verify Apache-PHP integration.
- Gnuboard Setup: Download Gnuboard5 (open-source bulletin board), extract to /var/www/html, create database, configure via web browser at http://IP/gnuboard5 installation page.
- Database User: Create MariaDB user account (not Linux user) with appropriate privileges for Gnuboard; admin account set during Gnuboard installation.
- Board Management: Create board groups, create boards within groups, set permissions; copy board URL to embed in user web pages via HTML links.

</details>

<details> <summary>KOR (한국어 버전)</summary>

## 13장 – DB 서버와 웹 서버

**데이터베이스**
- 데이터베이스 정의: 서로 관련성 있는 데이터를 데이터 간 중복성을 최소화하면서 체계적으로 모아놓은 것.
- 관계형 데이터베이스: 데이터를 테이블(행과 열)로 표현하여 테이블 생성 및 필드 분할·결합을 유연하게 처리.
- 용어: 데이터(각 항목 값), 테이블(행·열 형태 데이터), 데이터베이스(관련 테이블의 집합), 필드(테이블 열), 레코드(테이블 한 행), 키(레코드를 구분하는 필드값, 중복 불가).
- SQL 기초: 관계형 데이터베이스 생성·관리·쿼리 언어로, 각 문장은 세미콜론으로 끝나고 기본적으로 대소문자 구분 안 함.
- 데이터베이스 SQL: Show databases(기존 DB 목록), Create database(새 DB 생성), Drop database(DB 및 테이블 삭제), Use(작업 DB 선택).
- 테이블 SQL: Show tables(기존 테이블 목록), Create table(필드명·자료형 지정해 생성), Describe/Explain(테이블 구조 확인), Alter table(필드 추가·수정·삭제, 기본키 추가), Drop table(테이블 삭제).
- 레코드 작업: Insert into(새 레코드 삽입), Update(조건 기반 데이터 수정), Delete(조건 기반 삭제), Select(조건부 검색, 조인 지원).
- 조인: 여러 테이블을 기본키 같은 공통 필드로 연결해 관련 데이터를 한 번에 검색하는 방식.
- 접근 권한: Grant 문장으로 사용자에게 데이터베이스 권한 부여; 관리자가 DB 생성 후 일반 사용자에게 모든 권한 할당.

**MariaDB 설치와 사용**
- 설치: dnf로 mariadb-server 패키지 설치; 데몬명 mariadb.service, 프로세스 사용자명 mysql(호환성).
- 접속: mariadb 또는 mysql 명령으로 연결, 기본 프롬프트 "MariaDB [(none)]>", exit로 종료.
- 데이터베이스: Show databases(시스템 DB 포함), Create database st_db(생성), Use st_db(선택).
- 테이블 생성: Create table st_info (ST_ID int, NAME varchar(20), ...) default charset=utf8; 한글 방지를 위해 charset=utf8 필수.
- 기본키: Alter table tablename modify field int Not Null(널값 불허용), Alter table ... add constraint name primary key(field)(기본키 추가).
- 레코드: Insert into tablename values(...)(삽입), Select * from table(전체 검색), Select col from table where condition(조건 검색), Update tablename set col=val where condition(수정).
- 관리: mariadb-admin status(서버 상태: 가동시간, 스레드 수, 질의 수 등), mariadb-admin version(버전 정보), mariadb-admin password(루트 암호 설정).

**웹 서버 설치와 사용**
- 아파치 설치: dnf로 httpd 패키지 설치; httpd.service 데몬, ps로 여러 프로세스 확인.
- 활성화: Systemctl start httpd 시작; 방화벽에서 http 서비스 허용; 기본 디렉터리 /var/www/html(http://IP로 접속).
- 웹 페이지: /var/www/html에 HTML 파일 배치, index.html이 기본 표시됨.
- 사용자 웹: /etc/httpd/conf.d/userdir.conf에서 "UserDir disabled" 주석 처리, "UserDir public_html" 설정하면 ~/public_html 디렉터리에서 호스트 가능(http://IP/~username).
- 사용자 권한: public_html 디렉터리 생성, chmod 755 설정; 접근 거부 시 SELinux 해제 필요.
- APM 스택: Apache + PHP + MariaDB 조합으로 php, php-gd, php-mysqlnd 패키지 설치, httpd 재시작.
- PHP 확인: phpinfo.php에 <?php phpinfo(); ?> 작성, http://IP/phpinfo.php 접속해 아파치-PHP 연동 검증.
- 그누보드 설치: 공개 게시판 소프트웨어를 /var/www/html로 압축 해제, DB 생성 후 http://IP/gnuboard5 설치 페이지에서 설정.
- 데이터베이스 사용자: MariaDB 사용자 계정(리눅스 계정 아님) 생성 및 권한 부여; 그누보드 설치 시 관리자 계정 설정.
- 게시판 관리: 게시판 그룹 생성 → 게시판 생성 → 권한 설정; 게시판 URL을 사용자 웹 페이지 HTML에 링크로 삽입.

</details>
