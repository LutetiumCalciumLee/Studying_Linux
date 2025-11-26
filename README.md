<details> <summary>ENG (English Version)</summary>

## Chapter 3 – File Access Permission Management

**Section 1: File Access Permissions**
- Multi-User System: Linux, as a multi-user OS, restricts arbitrary access to others’ files using security mechanisms.
- Concept of Permissions: Basic security feature that controls who can read, write, or execute a file, based on user categories (owner, group, others).
- Types of Permissions: Read (view content only), Write (modify/delete content), Execute (run programs or access directories).
- Permission Notation: Represented as characters per category (r, w, x, or - if absent), forming 9 characters like `rw-r--r--`.
- Meaning of Groups: Shows that owner may have read/write while group and others may have read-only, etc.

**Section 2: Changing Permissions with Symbols**
- chmod Command: Owners and admins can change permissions; normal users can change permissions of their own files.
- Symbolic Mode Components: User categories (u, g, o, a), operators (+, -, =), and permission symbols (r, w, x).
- Typical Operations: Removing owner write (u-w), adding group write/execute (g+wx), adding execute for others (o+x).
- Combined Operations: Multiple changes in one command (e.g., `u+w,g-w`) without spaces after the comma.
- Practice Cases: Granting or removing execute permission for group/others, adjusting owner vs group write permissions.

**Section 3: Changing Permissions with Numbers**
- Numeric Mode Concept: Represents presence/absence of r, w, x as bits (1/0) and converts them to octal numbers 0–7.
- Converting rwx to Numbers: r=4, w=2, x=1; sum of enabled bits gives one digit (e.g., r-x → 4+1=5).
- Mapping Patterns: Frequently used values are 7, 6, 5, 4, 0; three digits represent owner, group, others.
- chmod with Numbers: Uses three-digit octal like 644, 444, 474, etc., where each position corresponds to a user category.
- Example Changes: Removing owner write from 644 → 444; giving group write/execute to make r--rwxr-- → 474; 755 or 700 for typical secure settings.

**Section 4: Default Permissions (umask)**
- Default Permission Concept: When files/directories are created, Linux applies default permissions based on system settings.
- Typical Defaults: Regular files – owner read/write, group/others read; directories – owner read/write/execute, group/others read/execute.
- Checking umask: Running `umask` shows current mask value; `umask -S` shows it in symbolic form.
- Meaning of Mask: Mask marks permissions that will NOT be granted (bit 1 means that permission is removed on creation).
- Effect on Creation: Changing umask modifies default permissions (e.g., resulting in files like 600 for han.txt).

**Section 5: How umask Works**
- Bit-Based Operation: For each permission bit, if mask bit is 1, that permission is cleared; if 0, requested permission passes through.
- Calculation Method: Often understood as “maximum permission minus mask” for quick reasoning.
- Different Masks: Default mask values vary by distribution and version; users adjust them to protect files/directories appropriately.
- Separate Effects on Files and Directories: A mask suitable for files may not be ideal for directories, so both should be tested.
- Practice: Adjusting umask so that owner and group get read/write while others get read-only, then verifying with newly created files.

</details>

<details> <summary>KOR (한국어 버전)</summary>

## 3장 – 파일 접근 권한 관리

**파일 접근 권한**
- 다중 사용자 시스템: 리눅스는 여러 사용자가 동시에 사용하는 시스템이므로, 다른 사용자가 내 파일에 임의로 접근하지 못하도록 보안 기능을 제공한다.
- 접근 권한 개념: 파일을 읽기, 쓰기, 실행할 수 있는지 제어하는 가장 기본적인 보안 장치로, 사용자 범주(소유자, 그룹, 기타)에 따라 다르게 설정할 수 있다.
- 권한 종류: 읽기 권한은 내용 조회만 가능하고, 쓰기 권한은 수정·삭제까지 가능하며, 실행 권한은 프로그램 실행이나 디렉터리 진입을 허용한다.
- 권한 표기: r, w, x와 권한 없음(-)을 조합해 rw-r--r--처럼 9개의 문자로 표시하며, 앞에서부터 소유자, 그룹, 기타 사용자의 권한을 의미한다.
- 해석 예시: rw-r--r--는 소유자는 읽기·쓰기, 그룹과 기타 사용자는 읽기만 가능하다는 뜻이다.

**기호를 이용한 권한 변경**
- chmod 명령: 파일 소유자와 관리자(root)는 접근 권한을 변경할 수 있고, 일반 사용자도 자신이 소유한 파일의 권한은 조정할 수 있다.
- 기호 모드 구성: 사용자 범주(u, g, o, a), 연산자(+는 부여, -는 제거, =는 재설정), 권한 문자(r, w, x)를 조합해 표현한다.
- 대표 예: 소유자의 쓰기 권한 제거(u-w), 그룹에 쓰기·실행 권한 부여(g+wx), 기타 사용자에 실행 권한 추가(o+x) 등이다.
- 여러 권한 동시 변경: u+w,g-w처럼 쉼표로 구분해 한 번에 여러 조건을 지정할 수 있으며, 쉼표 뒤에는 공백을 넣지 않는다.
- 실습 내용: 그룹·기타 사용자 실행 권한을 추가·제거하거나, 소유자의 쓰기 권한은 주고 그룹의 쓰기 권한은 빼는 등의 조합을 연습한다.

**숫자를 이용한 권한 변경**
- 숫자 모드 개념: 각 권한(r, w, x)의 유무를 2진수 비트(1 또는 0)로 보고 이를 8진수(0~7) 숫자로 환산한다.
- rwx의 숫자 환산: 읽기 4, 쓰기 2, 실행 1로 합산해 하나의 숫자를 만들며, 예를 들어 r-x는 4+1=5가 된다.
- 자주 쓰는 값: 7(rwx), 6(rw-), 5(r-x), 4(r--), 0(---) 등이 많이 사용되고 1, 2, 3은 상대적으로 사용 빈도가 낮다.
- 세 자리 숫자 표기: 첫째 자리는 소유자, 둘째는 그룹, 셋째는 기타 사용자의 권한을 나타내며, 예를 들어 644는 rw-r--r--를 의미한다.
- 예시 변경: 644에서 소유자 쓰기 권한을 제거하면 444가 되고, 그룹에 쓰기·실행 권한을 더해 r--rwxr--로 만들면 474가 되는 식이다.

**기본 접근 권한 설정 (umask)**
- 기본 권한 개념: 새로운 파일이나 디렉터리를 생성할 때 리눅스는 미리 정해진 기본값에 따라 접근 권한을 자동으로 부여한다.
- 기본값 예: 일반 파일은 보통 소유자는 읽기·쓰기, 그룹과 기타 사용자는 읽기만 가능하며, 디렉터리는 소유자에게 읽기·쓰기·실행, 그룹과 기타 사용자에게 읽기·실행 권한이 주어진다.
- umask 확인: 인자 없이 umask를 실행하면 현재 마스크 값을, -S 옵션으로 실행하면 문자 형태로 된 의미를 확인할 수 있다.
- 마스크 값 의미: 마스크는 “부여하지 않을 권한”을 지정하는 값으로, 해당 비트가 1이면 그 권한은 생성 시 제거된다.
- 영향 예시: umask를 변경하면 새로 생성되는 파일의 권한이 600(rw-------)처럼 보다 제한적으로 설정될 수 있다.

**umask 동작 방식**
- 비트 연산 관점: 마스크 비트가 1인 위치의 권한은 요청 여부와 관계없이 0(부여 안 됨)이 되고, 0인 위치는 요청된 권한이 그대로 적용된다.
- 이해하기 쉬운 계산법: “최대 권한에서 마스크 값을 뺀다”는 식으로 파일과 디렉터리의 기본 권한을 유추할 수 있다.
- 다양한 마스크 값: 배포판과 버전에 따라 기본 마스크가 다르며, 사용자는 자신의 보안 요구에 맞게 값을 조정해 활용할 수 있다.
- 파일·디렉터리 영향 차이: 어떤 마스크 값은 파일에는 적절하지만 디렉터리에는 불편할 수 있으므로 둘 다 테스트해 보는 것이 좋다.
- 실습: 현재 기본 권한을 확인하고, 소유자·그룹은 읽기·쓰기, 기타 사용자는 읽기만 가능하도록 마스크를 조정한 뒤 새 파일을 만들어 결과를 검증한다.

</details>
