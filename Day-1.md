# <b> AWS WEB-APPLICATION </b>


## <b> 실습1. VPC 구축 및 웹 서버 시작 </b>

* * *

### <b> 개요 </b>
- 본 실습 섹션에서는 Amazon Virtual Private Cloud(VPC)를 사용하여 자체 VPC를 생성
- AWS VPC에 구성 요소를 추가하여 사용자 정의된 네트워크를 구성
- AWS EC2 인스턴스에 대한 보안 그룹을 생성
- 웹 서버를 실행하고 이를 VPC에서 시작하도록 EC2 인스턴스를 구성 및 사용자 정의

### <b> 목표 </b>
본 실습을 마친 후 다음을 할 수 있게 됩니다.
- VPC 생성
- 서브넷 생성
- 보안 그룹 생성
- VPC에서 EC2 인스턴스 시작 

### <b> 사전 조건 </b>
본 실습을 위해서는 다음이 필요합니다.
- Microsoft Windows, Mac OS X 또는 Linux(Ubuntu,SuSE, Red Hat)가 실행되며 Wi-Fi가 되는 컴퓨터 사용
- Chrome, Firefox 또는 IE9 이상 버전과 같은 인터넷 브라우저 (IE9 이전 버전은 지원 안됨)

### <b> 기간 </b>
본 실습에는 약 45분 정도가 소요됩니다.

### <b> Task 1 : VPC 생성 </b>
- 개요
    - 이 섹션에서는 VPC를 생성합니다.
- 시나리오

본 실습에서는 다음과 같은 인프라를 구축하게 됩니다.

![image](/images/Day1-Task-WEB.png)

#### <b> Task 1.1 : VPC 생성 </b>
이 작업에서는 하나의 가용 영역에서 2개의 서브넷으로 구성된 VPC를 생성합니다.
- 1.1.1 <b>AWS Management Console</b>의 <b>Services</b> 메뉴에서 <b>[VPC]</b>를 클릭합니다.
- 1.1.2 <b>[Start VPC Wizard]</b>를 클릭합니다.
- 1.1.3 탐색 창에서 <b>[VPC with Public and Private Subnets]</b>를 클릭합니다.
- 1.1.4 <b>Select</b>를 클릭합니다.
    - 다음 정보를 입력합니다.
    - <b> [IP CIDR block] : 10.0.0.0/16 </b>
    - <b> [VPC name] : My Lab VPC </b>
    - <b> [Public Subnet] : 10.0.1.0/24 </b>
    - <b> [Availability Zone] : 가용 영역 2a 선택 </b>
    - <b> [Public Subnet Name] : Public_Subnet1 </b>
    - <b> [Private Subent] : 10.0.3.0/24 </b>
    - <b> [Availability Zone] : 가용 영역 2a 선택 </b>
    - <b> [Private Subnet Name] : Private_Subnet3 </b>
- 1.1.5 <b>[Specify the details of your NAT gateway]</b>에서 화면 오른쪽의 <b>[Use a NAT instance instead]</b>를 클릭합니다.
- 1.1.6 <b>[Instance type]</b>에 나열된 첫 번재 인스턴스 유형을 선택합니다. (예 : t2.micro)
- 1.1.7 <b>[Key pair name]</b>에서 AWSLABS 키 페어를 선택합니다.
- 1.1.8 <b>[Create VPC]</b>를 클릭합니다.
- 1.1.9 VPC가 생성되면, VPC가 성공적으로 생성되었다는 메시지가 표시된 페이지가 보입니다. <b>[OK]</b>를 클릭합니다.

#### <b> Task 1.2 : 추가 서브넷 생성 </b>
본 작업에서는 다른 가용 영역에 서브넷 2개를 추가로 생성하고 기존 라우팅 테이블을 통해 서브넷을 연결합니다.
- 1.2.1 탐색 창에서 `[Subnets]`를 클릭합니다. 
- 1.2.2 `[Create Subnet]`을 클릭합니다.
- 1.2.3 <b>[Create Subnet]</b> 대화 상자에서 다음 세부 정보를 입력합니다.
    - <b>[Name tag]</b> : Public Subnet2
    - <b>[VPC]</b> : My Lab VPC 클릭
    - <b>]Availability Zone]</b> : 가용 영역 2c 선택
    - <b>CIDR block</b> : 10.0.2.0/24
- 1.2.4 <b>[Yes, Create]</b>를 클릭합니다.
- 1.2.5 <b>[Create Subnet]</b>을 클릭합니다.
- 1.2.6 <b>[Create Subent]</b> 대화 상자에서 다음 세부 정보를 입력합니다. 
    - <b>[Name tag]</b> : Private Subnet4
    - <b>[VPC]</b> : My Lab VPC 클릭
    - <b>]Availability Zone]</b> : 가용 영역 2c 선택
    - <b>[CIDR block]</b> : 10.0.4.0/24
- 1.2.7 <b>[Yes, Create]</b>를 클릭합니다.
- 1.2.8 <b>[Public_Subnet2]</b>를 선택하고, 모든 다른 서브넷이 선택 해제되었는지 확인한 다음, 아래쪽 창에 있는 <b>[Route Table]</b>을 클릭합니다. 아래로 스크롤하여 <b>[Destination] 0.0.0.0/0</b>의 <b>[Target]</b>에 접두사 <b>[IGW]</b>가 포함되어 있는지 확인합니다. 포함되어 있지 않은 경우, <b>[Edit]</b>를 클릭하고 <b>Change to:</b> 목록에 있는 다른 라우팅 테이블을 클릭하여 <b>[Destination] 0.0.0.0/0</b>의 <b>[Target]</b>이 접두사 <b>[IGW]</b>를 포함하도록 변경합니다. <b>[Save]</b>를 클릭합니다.
- 1.2.9 <b>[Private_Subnet2]</b>를 선택하고, 모든 다른 서브넷이 선택 해제되었는지 확인한 다음, 아래쪽 창에 있는 <b>[Route Table]</b>을 클릭합니다. 아래로 스크롤하여 <b>[Destination] 0.0.0.0/0</b>의 <b>[Target]</b>에 접두사 <b>eni</b>가 포함되어 있는지 확인합니다. 포함되어 있지 않은경우, <b>[Edit]</b>를 클릭하고 <b>Change to:</b> 목록에 있는 다른 라우팅 테이블을 클릭하여 <b>[Destination] 0.0.0.0/0</b>의 <b>[Target]</b>이 접두사 eni를 포함하도록 변경합니다. <b>[Save]</b>를 클릭합니다.

#### <b> Task 1.3 : VPC 보안 그룹 생성 </b>
웹 및 SSH 트래픽에 대한 액세스 권한을 부여하는 VPC 보안 그룹을 생성합니다.
- 1.3.1 탐색 창에서 <b>[Security Group]</b>를 클릭합니다.
- 1.3.2 <b>[Create Security Group]</b>을 클릭합니다.
- 1.3.3 <b>[Create Security Group]</b> 대화 상자에서 다음 정보를 입력합니다.
    - <b>[Name tag]</b> : WebSecurityGroup
    - <b>[Group name]</b> : WebSecurityGroup
    - <b>[Description]</b> : Enable HTTP access
    - <b>[VPC]</b> : 작업 1.1에서 생성한 VPC를 클릭(My Lab VPC)
- 1.3.4 <b>[Yes, Create]</b>를 클릭합니다.
- 1.3.5 <b>[WebSecurityGroup]</b>을 선택합ㄴ디ㅏ.
- 1.3.6 <b>[Inbound Rules]</b> 탭을 클릭합니다.
- 1.3.7 <b>[Edit]</b>를 클릭합니다.
- 1.3.8 <b>[Type]</b>에서 <b>HTTP(80)</b>를 클릭합니다.
- 1.3.9 <b>[Source]</b> 상자를 클릭하고 <b>0.0.0.0/0</b>를 입력합니다.
- 1.3.10 <b>[Add another rule]</b>을 클릭합니다.
- 1.3.11 <b>[Type]</b>에서 <b>SSH(22)</b>를 클릭합니다.
- 1.3.12 <b>[Source]</b> 상자를 클릭하고 <b>0.0.0.0/0</b>을 입력합니다. 
- 1.3.13 <b>[Save]</b>를 클릭합니다. 

### <b> Task 2 : Web Server 시작 </b>
- 개요
    - VPC를 생성한 후, 생성한 VPC에서 EC2 인스턴스를 시작하고, 웹 서버의 역할을 하도록 부트스트랩합니다.

#### <b> Task 2.1 : 첫 번째 웹 서버 인스턴스 시작 </b>
본 작업에서는 VPC에서 EC2 인스턴스를 시작하는 과정을 살펴봅니다. 이 인스턴스는 웹 서버의 역할을 합니다.
- 2.1.1 <b>[Services]</b> 메뉴에서 <b>[EC2]</b>를 클릭합니다.
- 2.1.2 <b>[Launch Instance]</b>를 클릭합니다.
- 2.1.3 <b>[Amazon Linux AMI]</b> 행에서 <b>[Select]</b>를 클릭합니다.
- 2.1.4 <b>[Step2 : Choose an Instance Type]</b> 페이지에서 <b>[t2.micro]</b>가 선택되었는지 확인하고 <b>[Next : Configure Instance Details]</b>를 클릭합니다.
- 2.1.5 <b>[Step3 : Configure Instance Details]</b> 페이지에서 다음 정보를 입력하고 나머지 값은 모두 기본값으로 둡니다.
    - <b>[Network]</b> : 작업 1.1에서 생성한 VPC를 클릭(My Lab VPC)
    - <b>[Subnet]</b> : 작업 1.2에서 생성한 <b>Public_Subnet2 (10.0.2.0/24)</b>를 클릭
    - <b>[Auto-assign PublicIP]</b> : Enable을 클릭
- 2.1.6 아래로 스크롤하여 <b>[Advanced Details</b>] 섹션을 확장합니다.
- 2.1.7 명령 참조 파일에서 다음 사용자 데이터를 복사하여 <b>[User data]</b> 상자에 붙여 넣고, <b>[As text]</b>가 선택되었는지 확인합니다.

```sql
#!/bin/bash -ex
yum -y update
yum -y install httpd php mysql php-mysql
chkconfig httpd on
/etc/init.d/httpd start
if [ ! -f /var/www/html/lab2-app.tar.gz ]; then
cd /var/www/html
wget https://us-west-2-aws-staging.s3.amazonaws.com/awsu-ilt/AWS-100-ESS/v4.0/lab-2-configure-website-datastore/scripts/lab2-app.tar.gz
tar xvfz lab2-app.tar.gz
chown apache:root /var/www/html/lab2-app/rds.conf.php
fi
```
- 2.1.8 <b>[Next]</b> : Add Storage를 클릭합니다. 
- 2.1.9 <b>[Next]</b> : Add Tags를 클릭합니다. 
- 2.1.10 <b>[Step 5]</b> : Add Tags 페이지에서 다음 정보를 입력합니다.
    - <b>[Key]</b> : Name
    - <b>[Value]</b> : Web Server 1
- 2.1.11 <b>[Next]</b> : Configure Security Group을 클릭합니다.
- 2.1.12 <b>[Step 6]</b> : Configure Security Group 페이지에서 Select an existing security group을 클릭한 후, 작업 1.3에서 생성한 보안 그룹을 선택합니다. 
- 2.1.13 <b>[Reveiw and Launch]</b>를 클릭합니다.
- 2.1.14 인스턴스 정보를 확인한 후 <b>[Launch]</b>를 클릭합니다.
- 2.1.15 <b>[Choose an existing key pair]</b>를 클릭하고, <b>[AWSLABS]</b> 키 페어를 클릭하고, 승인 확인란을 선택한 후, [Launch Instance]를 클릭합니다.
- 2.1.16 아래로 스크롤하여 <b>[View Instance]</b>를 클릭합니다.
- 2.1.17 2개의 인스턴스(<b>Web Server1</b>과 VPC 마법사에서 시작한 NAT 인스턴스)가 보일 것입니다.
- 2.1.18 <b>[Web Server 1]</b>의 <b>[Status Checks]</b> 열에 2/2 cheks passed가 표시될 때까지 기다립니다. 3~5분 정도 걸립니다. 오른쪽 위에 있는 새로 고침 아이콘을 사용하여 업데이트를 확인합니다.
- 2.1.19 <b>[Web Server 1]</b>을 선택하고 <b>[Public DNS]</b> 값을 복사합니다.
- 2.1.20 새 웹 브라우저 창이나 탭에 Public DNS 값을 붙여 넣고 <b>[Enter]</b>를 누릅니다. <b>[Amazon Linux AMI Test Page</b>]가 보일 것입니다.

실습1. 완료 <br>

축하합니다! 성공적으로 VPC를 생성하고 생성한 VPC에서 EC2 인스턴스를 시작했습니다.


* * *

## <b> 실습2. 웹 사이트를 위한 관계형 데이터 스토어 구성 </b>

* * *

### <b> 개요 </b>
- 이 실습은 이전 실습을 기반으로 합니다.
- Amazon Relational Database Service(RDS) DB 인스턴스를 시작하는 과정을 살펴봅니다.
- 관계형 데이터베이스 관리 시스템(RDBMS) 요구사항에 맞게 Amazon RDS를 사용하도록 앞에서 생성한 웹 서버를 구성합니다.
- 본 실습은 AWS 관리형 데이터베이스 인스턴스를 활용하여 관계형 데이터베이스 요구 사항을 해결하는 개념을 강화하도록 설계되었습니다.

### <b> 목표 </b>
본 실습을 마친 후 다음을 할 수 있게 됩니다.
- 고가용성을 갖춘 Amazon RDS DB 인스턴스를 시작
- 웹 서버로부터의 연결을 허용하도록 DB 인스턴스를 구성
- 웹 애플리케이션을 열고 데이터베이스와 상호 작용

### <b> 기간 </b>
본 실습에는 약 45분 정도가 소요됩니다.

### <b> Task 1 : Amazon RDS DB 인스턴스 시작 </b>
- 개요
    - 이 작업에서는 MySQL이 지원되는 Amazon RDS DB 인스턴스를 시작합니다.
- 시나리오

다음 인프라에서 시작합니다.

![image](/images/Day1-Task-WEB.png)

다음 인프라를 구축합니다.

![image](/images/Day1-Task-RDS.png)

#### <b> Task 1.1 : RDS DB 인스턴스에 대한 VPC 보안 그룹 생성 </b>
이 작업에서는 웹 서버가 RDS DB 인스턴스에 액세스하도록 허용하는 VPC 보안 그룹을 생성합니다.
- 1.1.1 <b>[AWS Management Console의 Services]</b> 메뉴에서 <b>[VPC]</b>를 클릭합니다.
- 1.1.2 탐색 창에서 <b>[Security Groups]</b>를 클릭합니다.
- 1.1.3 <b>[Create Security Group]</b>을 클릭합니다.
- 1.1.4 <b>[Create Security Group]</b> 대화 상자에서 다음 세부 정보를 입력합니다.
    - <b>[Name tag]</b> : DBSecurityGroup
    - <b>[Group name]</b> : DBSeurityGroup
    - <b>[Description]</b> : DB Instance Security Group
    - <b>[VPC]</b> : My LAB VPC 클릭
- 1.1.5 <b>[Yes, Create]</b>를 클릭합니다.
- 1.1.6 방금 생성한 <b>[DBSecurityGroup]</b>을 선택하고, 다른 모든 보안 그룹이 선택 해제되어 있는지 확인합니다. 
- 1.1.7	[Inbound Rules] 탭을 선택하고 <b>[Edit]</b>를 클릭합니다.
- 1.1.8	다음 세부 정보로 인바운드 규칙을 생성합니다.
    - <b>[Type]</b> : MySQUAurora (3306)
    - <b>[Protocol]</b> : TCP(6)
    - <b>[Source]</b> : WebSecurityGroup
- 1.1.9	<b>[Save]</b>를 클릭합니다.

#### <b> Task 1.2 : Amazon RDS 인스턴스용 프라이빗 서브넷 생성 </b>
이 작업에서는 하나의 가용 영역에서 2개의 서브넷으로 구성된 VPC를 생성합니다.
- 1.2.1	탐색 창에서 <b>[Subnet]</b>를 클릭합니다.
- 1.2.2	<b>[Public_Subnet1]</b>을 선택하고, 모든 다른 서브넷을 선택 해제한 다음, 아래쪽 창에 있는 <b>[Summary]</b> 탭으로 스크롤합니다. 이 서브넷의 <b>[Availability Zone]</b>을 적어둡니다. (<b>가용 영역 2a)</b>
- 1.2.3	<b>[Public_Subnet2]</b>를 선택하고, 모든 다른 서브넷을 선택 해제한 다음, 아래쪽 창에 있는 <b>[Summary]</b> 탭으로 스크롤합니다. 이 서브넷의 <b>[Availability Zone]</b>을 적어둡니다. (<b>가용 영역 2c</b>)
- 1.2.4	<b>[Create Subnet]</b>을 클릭합니다.
- 1.2.5	<b>[Create Subnet]</b> 대화 상자에서 다음 세부 정보를 입력합니다.
    - <b>[Name tag]</b> : Private Subnet 5
    - <b>[VPC]</b> : My Lab VPC 선택
    - <b>[Availability Zone]</b> : 앞에서 퍼블릿 서브넷1용으로 적어둔 가용 영역을 클릭
    - <b>[CIDR block]</b> : 10.0.5.0/24
- 1.2.6	<b>[Yes, Create]</b>를 클릭합니다.
- 1.2.7	<b>[Create Subnet]</b>을 클릭합니다. 
- 1.2.8	<b>[Create Subnet]</b> 대화 상자에서 다음 세부 정보를 입력합니다.
    - <b>[Name tag]</b> : Private Subnet 6
    - <b>[VPC]</b> : My Lab VPC 클릭
    - <b>[Availability Zone]</b> : 앞에서 퍼블릭 서브넷 2용으로 적어둔 가용 영역을 클릭
    - <b>[CIDR block]</b> : 10.0.6.0/24
- 1.2.9	<b>[Yes, Create]</b>를 클릭합니다.
- 1.2.10 <b>[Private Subnet 5]</b>를 선택하고, 모든 다른 서브넷이 선택 해제되었는지 확인한 다음, 아래쪽 창에 있는 <b>[Route Table]</b>을 클릭합니다. 아래로 스크롤하여 <b>[Destination] 0.0.0.0/0</b>의 <b>[Target]</b>에 접두사 <b>[eni]</b>가 포함되어 있는지 확인합니다. 포함되어 있지 않거나 <b>[Destination] 0.0.0.0/0</b>이 없는 경우, <b>[Edit]</b>를 클릭하고 <b>Change to :</b> 목록에서 <b>[Private Route Table]</b>을 클릭하여 <b>[Destination] 0.0.0.0/0</b>의 <b>[Target]</b>이 접두사 <b>[eni]</b>를 포함하도록 변경합니다. <b>[Save]</b>를 클릭합니다.
- 1.2.11 <b>[Private Subnet 6]</b>에서 앞에서 수행한 단계를 반복합니다. 

#### <b> Task 1.3 : DB 서브넷 그룹 생성 </b>
이 작업에서는 DB 서브넷 그룹을 생성합니다. 각 DB 서브넷 그룹은 지정된 리전에서 두 개 이상의 가용 영역에 서브넷이 있어야 합니다.
- 1.3.1 <b>[Services]</b> 메뉴에서 <b>[RDS]</b>를 클릭합니다.
- 1.3.2 탐색 창에서 <b>[Subnet Groups]</b>를 클릭합니다.
- 1.3.3 <b>[Create DB Subnet Group]</b>을 클릭합니다.
- 1.3.4 <b>[Create DB Subnet Group]</b> 페이지에서 다음 세부 정보를 입력합니다.
    - <b>[Name]</b> : dbsubnetgroup
    - <b>[Description]</b> : Lab DB Subnet Group
    - <b>[VPC ID]</b> : My Lab VPC 클릭
- 1.3.5 <b>[Availability Zone]</b>의 경우, <b>[Private_Subnet5]</b>용으로 선택한 가용 영역을 클릭합니다.
- 1.3.6 <b>[Subnet ID]</b>의 경우, <b>10.0.5.0/24</b>를 클릭한 다음 <b>[Add]</b>를 클릭합니다.
- 1.3.7 <b>[Availability Zone]</b>의 경우, <b>[Private_Subnet6]</b>용으로 선택한 가용 영역을 클릭합니다.
- 1.3.8 <b>[Subnet ID]</b>의 경우, <b>10.0.6.0/24</b>를 클릭한 다음 <b>[Add]</b>를 클릭합니다.
- 1.3.9 <b>[Create]</b>를 클릭합니다.
- 1.3.10 새 서브넷 그룹이 보이지 않으면, 콘솔의 오른쪽 위 모서리에 있는 새로고침 아이콘을 클릭합니다.

#### <b> Task 1.4 : RDS DB 인스턴스 생성 </b>
이 작업에서는 MySQL 지원 Amazon RDS DB 인스턴스를 구성 및 시작합니다.
- 1.4.1	<b>[Services]</b> 메뉴에서 <b>[RDS]</b>를 클릭합니다.
- 1.4.2	<b>[Get Started Now</b>]를 클릭합니다.
- 1.4.3	<b>[MySQL]</b>을 클릭하고 <b>[Select]</b>를 클릭합니다.
- 1.4.4	<b>[Production]</b> 아래의 <b>[MySQL]</b>을 클릭합니다.
- 1.4.5	<b>[Next Step]</b>을 클릭합니다.
- 1.4.6	<b>[Specify DB Details]</b> 페이지에서 다음 세부 정보를 입력합니다.
    - <b>[DB Instance Class]</b> : 목록에 있는 첫 번째 옵션을 클릭
    - <b>[Multi-AZ Deployment]</b> : Yes 클릭
    - <b>[DB Instance Identifier]</b> : labdbinstance
    - <b>[Master Username]</b> : labuser
    - <b>[Master Password]</b> : labpassword
    - <b>[Confirm Password]</b> : labpassword
- 1.4.7	<b>[Next Step]</b>을 클릭합니다.
- 1.4.8	<b>[Configure Advanced Settings]</b> 페이지에서 다음 정보를 입력하고 나머지 값은 모두 기본값으로 둡니다.
    - <b>[VPC]</b> : My Lab VPC
    - <b>[Subnet Group]</b> : dbsubnetgroup
    - <b>[Publicly Accessible]</b> : No
    - <b>[VPC Security Group(s)]</b> : DBSecurityGroup (VPC)
    - <b>[Database Name]</b> : sampledb
    - 다음으로 Monitoring 항목에서 Enable Enhanced Monitoring : No를 설정합니다.
- 1.4.9	<b>[Launch DB Instance]</b>를 클릭합니다.
- 1.4.10 <b>[View Your DB Instances]</b>를 클릭합니다.
- 1.4.11 <b>[labdbinstance]</b>를 선택하고, <b>[Endpoint]</b>가 available 또는 modifying으로 변할 때까지 기다립니다. 최대 10분 정도 걸릴 수 있습니다. 오른쪽 위에 있는 새로고침 아이콘을 사용하여 업데이트를 확인합니다. 
- 1.4.12 <b>[Endpoint]</b>를 복사하여 저장합니다. 3306을 복사하지 않도록 주의합니다. <b>[Endpoint]</b>는 "qr7g2qco3oeq5h.cze6p5rivinc.us-west-2.rds.amazon.com"과 비슷한 형태입니다.


### <b> Task 2 : 데이터베이스와 상호 작용 </b>
- 개요
    - 이 작업에서는 이전 실습에서 생성한 웹 서버에 배포된 PHP 웹 애플리케이션을 통해 데이터베이스와 상호 작용합니다.

#### <b> Task 2.1 : 데이터베이스 웹 애플리케이션에 액세스 </b>
웹 서버에서 실행되는 웹 애플리케이션을 엽니다.
- 2.1.1	<b>[Services]</b> 메뉴에서 <b>[EC2]</b>를 클릭합니다.
- 2.1.2	탐색 창에서 <b>[Instances]</b>를 클릭합니다.
- 2.1.3	<b>[Web Server1]</b>을 선택하고, 모든 다른 인스턴스가 선택 해제되었는지 확인한 후, 아래쪽 창에 있는 <b>[Description]</b> 탭까지 아래로 스크롤합니다.
- 2.1.4	<b>[Web Server1]</b>의 <b>[Public IP]</b>주소를 복사합니다. 
- 2.1.5	IP 주소를 새 브라우저 탭 또는 창에 붙여넣습니다. 웹 애플리케이션이 웹 서버의 인스턴스 메타데이터와 함께 표시됩ㄴ디ㅏ.
- 2.1.6	AWS 로고 오른쪽 옆에 있는 <b>[RDS]</b> 링크를 클릭합니다.
- 2.1.7	다음 정보를 입력합니다. 
    - <b>[Endpoint]</b> : 앞에서 복사한 엔드포인트를 붙여 넣습니다. 3306이 생략되어 있는지 확인합니다.
    - <b>[Database]</b> : sampledb
    - <b>[Username]</b> : labuser
    - <b>[Password]</b> : labpassword
- 2.1.8	<b>[Submit]</b>을 클릭합니다. 연결 문자열이 표시된 후, 페이지가 리디렉션됩니다. 2개의 새로운 레코드가 주소 테이블에 추가되어 표시됩니다.
- 2.1.9	또 다른 담당자를 추가하려면 <b>[Add Contact]</b>을 클릭하고 <b>[Name]</b>, <b>[Phone]</b> 및 <b>[Email]</b>을 입력한 후, <b>[Submit]</b>를 클릭합니다.
- 2.1.10 담당자를 수정하려면, <b>[Edit]</b>를 클릭하고, 원하는 필드를 수정한 다음, Submit를 클릭합니다. 
- 2.1.11 레코드를 삭제하려면, <b>[Remove]</b>를 클릭합니다. 
- 2.1.12 이제 이 브라우저 탭이나 창을 닫아도 됩니다.


실습2. 완료 <br>

축하합니다! 웹 사이트를 위한 관계형 데이터 스토어 구성을 성공적으로 완료했습니다. <br>



* * *

## <b> 실습3. 인프라 관리 </b>

* * *

### <b> 개요 </b>

- 본 실습은 이전 실습을 기반으로 합니다.
- Elastic Load Balancing(ELB)과 Auto Scaling 서비스를 사용합니다.
- 인프라를 로드 밸런싱하고 자동 조정하는 과정을 살펴봅니다.

### <b> 목표 </b>

본 실습을 마친 후 다음을 할 수 있게 됩니다.

- 실행중인 인스턴스에서 Amazon 머신 이미지(AMI)를 생성
- ELB 로드 밸런서 추가
- Auto Scaling 시작 구성 생성
- Auto Scaling 그룹 생성
- 프라이빗 서브넷 내에서 새 인스턴스를 자동 조정
- Amazon CloudWatch 경보 생성
- 인프라의 성능 모니터링

### <b> 기간 </b>

본 실습에는 약 45분 정도가 소요됩니다.


### <b> Task 1 : Auto Scaling </b>

- 개요
    - 이 작업에서는 인프라를 생성하고 자동 조정합니다.
- 시나리오

다음 인프라에서 시작합니다.

![image](/images/Day1-Task-RDS.png)

다음 인프라를 구축합니다.

![image](/images/Day1-Task-ELB.png)


#### <b> Task 1.1 : VPC 생성 </b>

이 작업에서는 하나의 가용 영역에서 2개의 서브넷으로 구성된 VPC를 생성합니다.

- 1.1.1	AWS Management Console의 Services 메뉴에서 EC2를 클릭합니다.
- 1.1.2	탐색 창에서 Instances를 클릭합니다.
- 1.1.3	Web Server 1의 Status Checks 2/2 checks passed로 표시되어 있는지 확인합니다. 아닌 경우, 변경될 때까지 기다렸다가 다음 단계로 진행합니다. 오른쪽 위에 있는 새로고침 버튼을 사용하여 업데이트를 확인합니다.
- 1.1.4	Web Server 1을 오른쪽 마우스 클릭하고, Image를 클릭한 후, Create Image를 클릭합니다.
- 1.1.5	다음 정보를 입력하과, 나머지 값은 그대로 기본값으로 둡니다.
    - Image name: Web Server AMI
    - Image description: Lab 3 AMI for Web Server
- 1.1.6	Create Image를 클릭합니다.
- 1.1.7	확인 화면에 새로운 AMI용 AMI ID가 표시됩ㄴ디ㅏ.
- 1.1.8	Close를 클릭합니다.


#### <b> Task 1.2 : 로드 밸런서 추가 </b>

이 작업에서는 로드 밸런서를 생성하여 2개의 가용 영역에서 여러 EC2 인스턴스에 걸쳐 트래픽을 로드 밸런싱합니다. 

- 1.2.1	탐색 창에서 Load Balancer를 클릭합니다.
- 1.2.2 Create Load Balancer를 클릭한 후 다음 화면에서 Classic Load Balancer를 선택합니다.
- 1.2.3 다음 정보를 입력하고, 나머지 값은 그대로 기본값으로 둡니다.
    - Load Balancer name : Lab3ELB
    - Create LB inside : My Lab VPC 선택
    - Select Subnet : [+]를 클릭하여 Public Subnet 1 및 Public Subnet 2를 선택
- 1.2.4 Next : Assign Security Group를 클릭합니다.
- 1.2.5 default 보안 그룹을 선택 해제하고, 이름에 WebSecurityGroup이 포함되고 Enable HTTP access 라는 Description이 있는 보안 그룹을 선택합니다.
- 1.2.6 Next : Configure Security Settings를 클릭합니다.
- 1.2.7 본 실습에서는 보안 리스너는 구성하지 않으므로, Next : Configuretion Health Check를 클릭합니다.
- 1.2.8 다음 정보를 입력하고, 나머지 값은 그대로 기본값으로 둡니다.
    - Ping Path : /index.php (기본값과 다른 값입니다.)
    - Interval : 6
    - Healthy Threshold : 2를 선택
- 1.2.9 Next : Add EC2 Instance를 클릭합니다.
- 1.2.10 다음 작업에서 로드 밸런서에서 EC2 인스턴스를 추가합니다. Next : Add Tags를 클릭합니다.
- 1.2.11 Review and Create를 클릭합니다.
- 1.2.12 로드 밸런서의 구성을 확인하고 Create를 클릭합니다.
- 1.2.13 Close를 클릭합니다.
- 1.2.14 Lab3ELB를 선택하고, 아래쪽 창의 Description에서 로드 밸런서의 DNS Name을 적어둡니다. 이때 (A Record)는 생략합니다. 




#### <b> Task 1.3 : 시작 구성 및 Auto Scaling 그룹 생성 </b>

이 작업에서는 Auto Scaling 그룹에 대한 시작 구성을 생성합니다.

- 1.3.1	탐색 창에서 Launch Configurations를 클릭합니다.
- 1.3.2	Create Auto Scaling group과 Create launch configuration을 클릭합니다.
- 1.3.3	탐색 창에서 My AMIs를 클릭합니다.
- 1.3.4	앞에서 생성한 Web Server AMI를 선택하기 위해 Select를 클릭합니다.
- 1.3.5	t2.micro 선택을 수락하려면 Next: Configure details를 클릭합니다.
- 1.3.6	다음 정보를 입력하고, 나머지 값은 그대로 기본값으로 둡니다. 
    - Name : Lab3Config
    - Monitoring : Enable CloudWatch detailed monitoring 선택
- 1.3.7	Next : Add Storage를 클릭합니다.
- 1.3.8	Next : Configure Security Group을 클릭합니다.
- 1.3.9	Select an existing security group을 클릭하고, 이름에 WebSecurityGroup이 포함되고 Enable HTTP access라는 Description이 있는 보안 그룹을 선택합니다.
- 1.3.10 Review를 클릭합니다.
- 1.3.11 시작 구성의 세부 정보를 확인하고, Create launch configuration을 클릭합니다. 
- 1.3.12 Choose an existing key pair를 클릭하고, qwikLABS key pair를 선택하고, 승인 확인란을 선택한 후, Create launch configuration을 클릭합니다. 
- 1.3.13 Auto Scaling 그룹에 대한 다음 정보를 입력하고, 나머지 값은 그대로 기본값으로 둡니다.
    - Group name : Lab3ASGroup
    - Group size : 2개의 인스턴스로 시작
    - Network: My Lab VPC 선택
- 1.3.14 아래로 스크롤하여 Advanced Details를 확장하고 Receive traffic from one or more load balancers를 선택합니다. 
- 1.3.15 Classic Load Balancers 텍스트 상자를 클릭한 다음, Lab3ELB를 클릭합니다.
1.3.16 다음 정보를 입력하고, 나머지 값은 그대로 기본값으로 둡니다.
    - Health Check Type: ELB 선택
    - Monitoring: Enable CloudWatch detailed monitoring 선택
- 1.3.17 Next: Configure scaling policies를 클릭합니다.
- 1.3.18 Use scaling policies to adjust the capacity of this group을 선택합니다.
- 1.3.19 2개와 6개의 인스턴스 범위 내에서 조정할 수 있도록 Scale between 텍스트 상자를 수정합니다.
- 1.3.20 Increase Group Size에서 Execute policy when에 대해 Add New Alarm을 클릭합니다.
- 1.3.21 Send a notification to :가 선택되어 있는지 확인한 후, create topic을 클릭합니다. (이메일 알람을 생성하는 것은 선택 사항이며, 나머지 실습에서 [*]로 표시된 관련 단계를 건너뛰어도 좋습니다. 이메일 알림을 받지 않으려면, Send a notification to :을 선택 해제해야 합니다.)
- 1.3.22 다음 정보를 입력하고, 나머지 값은 그대로 기본값으로 둡니다. 
    - ‘Send a notification to : ASTopic
    - ‘With these recipients : 액세스 권한이 있는 이메일 주소를 입력
    - Whenever: Average of CPU Utilization
    - Is >= 65 Percent
    - For at least: 1 consecutive period(s) of 1 minute
    - Name of alarm: HighCPUUtilization
- 1.3.23 Create Alarm을 클릭합니다. 
- 1.3.24 Increase Group Size의 나머지 부분에 다음 정보를 입력합니다.
    - Take the action: Add 선택. 1 입력, instances 선택. 65 입력
    - Instances need : 각 단계 후 줁비에 60초
- 1.3.25 Decrease Group Size에서 Execute policy when에 대해 Add New Alarm을 클릭합니다. 
- 1.3.26 ‘Send a notification to:가 선택되어 있는지 확인하고, ASTopic (<your email address>)을 선택합니다. 이메일 알림을 받지 않으려면 이 항목을 선택 해제합니다.
- 1.3.27 다음 정보를 입력하고, 나머지 값은 그대로 기본값으로 둡니다.
    - Whenever: Average of CPU Utilization
    - Is <= 20 Percent
    - For at least: 1 consecutive period(s) of 1 minute
    - Name of alarm: LowCPUUtilization
- 1.3.28 Create Alarm을 클릭합니다.
- 1.3.29 Decrease Group Size의 나머지 부분에 다음 정보를 입력합니다.
    - Take the action: Remove 선택, 1 입력. instances 선택. 20 입력
- 1.3.30 Next: Configure Notifications를 클릭합니다.
- 1.3.31 Next: Configure Tags를 클릭합니다.
- 1.3.32 다음 정보를 입력하고, 나머지 값은 그대로 기본값으로 둡니다.
    - Key: Name
    - Value: Lab3Weblnstance
- 1.3.33 Review를 클릭합니다.
- 1.3.34 Auto Scaling 그룹의 세부 정보를 확인한 다음, Create Auto Scaling group을 클릭합니다.
- 1.3.35 Auto Scaling 그룹이 생성되면 Close를 클릭합니다.
- 1.3.36 * Auto Scaling 그룹에 대한 알림 구독을 확인하는 이메일을 받게 됩니다. 이메일을 열고 Confirm subscription link를 클릭합니다.


#### <b> Task 1.4 : Auto Scaling이 작동하는지 확인하고 인스턴스를 로드 밸런서에 추가</b>

이 작업에서는 Auto Scaling이 올바르게 작동하고 있는지 확인합니다.

- 1.4.1	탐색 창에서 Instances를 클릭합니다.
- 1.4.2	4개의 인스턴스 (Web Server 1, NAT Server, 그리고 Lab3WebInstance라는 이름의 새로운 인스턴스 2개)가 보일 것입니다.
- 1.4.3	탐색 창에서 Load Balancer를 클릭합니다.
- 1.4.4	Lab3ELB를 선택하고, 아래로 스크롤하여 Instances 탭을 클릭합니다. 이 로드 밸런서 목록에 Lab3WebInstance가 나열된 것이 보일 것입니다.
- 1.4.5	Lab3ELB의 Instances 탭에서 이 인스턴스의 Status가 InService로 바뀔 때까지 기다립니다. 오른쪽 위에 있는 새로고침 버튼을 사용하여 업데이트를 확인합니다.
- 1.4.6	로드 밸런서가 인스턴스가 실행되고 있는 가용 영역의 Healthy? 필드 아래에 Yes를 표시합니다.

### <b> Task 2 : 인프라 모니터링 </b>

- 개요
    - 인스턴스가 최소 2개, 최대 6개인 Auto Scaling 그룹을 생성했습니다.
    - Auto Scaling 그룹을 한번에 인스턴스 하나씩 증가하거나 축소하는 AutoScaling 정책을 생성했습니다.
    - 그룹의 전체 평균 CPU 사용률이 >= 65%와 <= 20% 일 때 각각 해당 정책을 트리거하는 Amazon CloudWatch 경보를 생성했습니다.
    - 최소 크기는 2이고 부하가 전혀 없으므로 현재 2개의 인스턴스가 실행중입니다.
    - 생성한 CloudWatch 경보를 사용하여 이제 인프라를 모니터링할 수 있습니다.


#### <b> Task 2.1 : Auto Scaling 테스트 </b>

본 작업에서는 앞에서 구현한 Auto Scaling 구성을 테스트합니다. 

- 2.1.1	Services 메뉴에서 CloudWatch를 클릭합니다.
- 2.1.2	탐색 창에서 Alarms를 클릭합니다(ALARM 이 아님).
- 2.1.3	HighCPUUtilization과 LowCPUUtilization 이라는 2개의 경보가 보입니다. LowCPUUtilization은 State가 Alarm 이어야 하고, HighCPUUtilization은 State가 OK 여야 합니다. 이는 현재 그룹 CPU 사용률이 20% 미만이기 때문입니다. 그룹 크기가 현재 최소 크기인 (2)이므로, Auto Scaling은 어떠한 인스턴스도 제거하지 않습니다.
- 2.1.4	EMI 1.2.13에서 복사한 로드 밸런서의 DNS 이름을 새 브라우저 창 또는 탭에 복사합니다. 
- 2.1.5	AWS 로고 오른쪽 옆에 있는 LOAD TEST를 클릭합니다. 애플리케이션이 인스턴스에 대한 부하 테스트를 수행하고 5초 간격으로 자동 새로 고침합니다. [Current CPU load]가 100% 상승한 것을 볼 수 있습니다. Load Test 링크는 간단한 백그라운드 프로세스를 트리거합니다.
- 2.1.6	Services 메뉴에서 CloudWatch를 클릭합니다. 5분 이내에 Low CPU 경보 상태가 OK로 변경되고 High CPU 경보 상태가 ALARM으로 변경되는 것을 확인할 수 있습니다.
- 2.1.7	Services 메뉴에서 EC2를 클릭합니다.
- 2.1.8	탐색 창에서 Ai Instances를 클릭합니다.
- 2.1.9	이제 Lab3Weblnstance라는 이름의 인스턴스가 2개 이상 실행되는 것을 볼 수 있습니다.
- 2.1.10 단계 2.1.3에서 연 브라우저 탭 또는 창을 닫습니다.


#### <b> Task 2.2 : 첫 번째 웹 서버 인스턴스 시작 </b>

본 작업에서는 퍼블릭 서브넷2의 웹 서버 1을 종료합니다. Auto Scaling 그룹이 프라이빗 서브넷에서 인스턴스를 시작했으므로, 공개적으로 액세스 가능한 원래 웹 서버는 더 이상 필요없습니다. 

- 2.2.1	Services 메뉴에서 EC2를 클릭합니다.
- 2.2.2	탐색 창에서 Instances를 클릭합니다. 
- 2.2.3	Web Server 1을 마우스 오른쪽 버튼으로 클릭하고 Instance State 와 Terminate를 각각클릭합니다.




실습3. 완료 <br>

축하합니다! Auto Scaling과 Elastic Load Balancer을 사용하여 인프라를 관리하는 작업을 성공적으로 완료했습니다. 




















# Thank you
