## IAM(Identity and Access Management)

IAM = Identity and Access Management, Global service, 즉 aws 리소스에 대한 접근을 제어하는 서비스이다.

-   루트 사용자는 디폴트로 만들어지는것
-   유저는 너의 그룹안에만 있고, 그룹지어질 수도 있다.
-   한 사용자가 여러그룹에 속할 수도 있다.
-

IAM의 이유

-   aws 계정을 사용하도록 허용하기 위함.
-   IAM Policy를 통해 Json 문서를 지정할 수 있다.
-   AWS는 least privilege principle을 따른다. 즉 사용자가 꼭 필요로 하는 것 이상의 권한을 주지 않는 것이다.
-   IAM은 리전을 가지지 않는다. 즉 모든 리전에서 사용할 수 있다.

IAM(Identity and Access Management)의 구성 요소

Version: IAM 정책의 버전을 지정합니다.
ID: IAM 정책의 고유 식별자입니다.
Statement: 정책의 규칙을 정의하는 부분입니다.
Sid: 규칙의 식별자입니다.
Effect: 규칙의 적용 효과를 지정합니다. (Allow 또는 Deny)
Principal: 규칙이 적용되는 주체를 지정합니다. (사용자, 그룹, 역할 등)
Action: 규칙이 허용하는 작업을 지정합니다. (리소스에 대한 허용된 작업)
Resource: 규칙이 적용되는 리소스를 지정합니다. (예: S3 버킷, EC2 인스턴스 등)
Condition: 규칙이 적용되는 조건을 지정합니다. (예: 특정 IP 주소, 시간 등)
IAM은 AWS 리소스에 대한 접근을 제어하는 서비스로, 이러한 구성 요소를 사용하여 정책을 작성하고 관리할 수 있습니다.

시험에는 Effect, principal, action, resource에 대해 이해를 해야한다.

IAM - Password Policy
사용자의 이용침해를 막기 위해서 첫번쨰 방법은 비밀번호 정책의 정의.
왜냐하면 비밀번호가 강력할수록 계정의 보안이 철저해지기 떄문.
aws에서는 다양한 옵션을 이용해 비밀번호 정책의 생성이 가능

-   비밀번호의 최소길이
-   특정문자의 사용
-   비밀번호 변경을 허용 또는 금지
-   비밀번호 만료기간 설정
-   비밀번호 재사용 횟수 설정

시험대비를 위해 알아둬야할 두번째 요소
IAM - MFA(Multi-Factor Authentication)다요소 인증

-   AWS에서는 이 매커니즘을 필수적으로 사용하도록 권장. -적어도 루트 게정은 무슨 일이 있어도 반드시 보호해야함
-   MFA는 두가지 요소를 통해 인증을 수행 -비밀번호
-   MFA 장치를 통한 인증

MFA의 장점
단순히 비밀번호만 해킹당해도 물리적인 인증장치가 필요하기 때문에, 계정이 침해 당하기 어렵다.

MFA devices options in AWS

-   Virtual MFA device
-   Universal 2nd Factor (U2F) Security Key 예를 들어(Yubico사의 YubiKey)
-   Hardware Key Fob MFA Device 미국 정부의 aws govCloud를 사용하는 경우라면 필요

어떻게 하면 유저가 AWS에 액세스 할 수 있는가?

-   AWS Management Console(protected by password + MFA)
-   AWS Command Line interface (CLI): protected by access keys(CLI) : 컴퓨터에서 설정하는건데 액세스 키에 의해 보호된다. 액세스 키란 자격증명으로 터미널에서의 aws 액세스를 가능하게 해준다.
-   AWS Software Developer Kit (SDK) for code : protected by access keys

AWS Console 관리 콘솔을 통해서 이러한 access keys를 생성가능, Access key는 비밀번호와 같은 것, 동료와 공유하면 안된다.
Access Key = username
Secret Access Key = password

CLI는 무엇인가?
명령 커맨드를 사용하여 AWS 서비스들과 상호작용을 할 수 있도록 해주는 도구이다.

SDK는 무엇인가
소프트웨어 개발 키트로써, 특정 언어로 된 라이브러리의 집합 따라서 프로그래밍 언어에 따라 다름. SDK는 코딩을 통해 애플리케이션 내에 심어 두는 것 .
지원 언어로는 sdks, mobile sdks, IoT Device sdks,
주로 사용되는 것은 aws cli on aws sdk for python이라는 것이 있다.

cli의 access key로 로그인하는법

aws configure명령어 입력후, 액세스키 및 시크릿액세스키 입력

> aws iam list-users 로 권한을 확인

aws에 액세스 하기위해서는 액세스 키와 비밀 액세스 키를 구성하여 ClI를 사용할 수 있다는 것이다.

CloudShell

-   CloudShell은 AWS 클라우드에서 무료로 사용 가능한 터미널같은 개념이다.
-   특징
    AWS 고유의 API 호출을 반환해준다.
    API 호출을 할 리전을 지정할 수 있다.(기본값은 현재 로그인된 리전으로 나오게 된다.)
    Shell의 구성 설정이 가능하다. (글씨 크기를 설정하는등)
    파일들을 업로드, 혹은 다운로드도 가능

요약 CloudShell은 특정 리전에서만 사용가능하니, 리전을 선택을 잘해야하고, CloudShell 사용을 원치 않거나 선호하지 않는 경우에도 그냥 터미널을 사용해도 된다.

IAM Roles for Services

-   IAM Role은 사용자와 같지만 실제 사람들이 사용하도록 만들어 진 것이 아니고, AWS 서비스에 의해 사용되도록 만들어짐
-   예를들어 EC2라는 가상서버를 임대할 떄 그 EC2인스턴스에 권한을 부여해야 한다. 그래서 IAM Role을 만들어 하나의 개체로 만들어야 한다.
-   Common roles(EC2 Instance Roles, Lambda Function Roles, Roles for CloudFormation)
-   AWS에서는 여러가지 타입들에 대해 Role을 부여할 수 있는데 알아둬야할건 AWS 서비스에 대한 Role을 생성할 수 있다는 것에 대해 알아두면 된다.
