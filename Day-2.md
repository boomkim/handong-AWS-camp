# Build a Serverless Web Application

- 2일차 블라블라

## 0. Overview

![image](/images/Day2-0.png)

- 생성 후 24시간이 지난 AWS 계정
리전 선택: 서울로 할겁니다
언어 선택: 영어로 할겁니다

에디터, 브라우저 
퀴즈 규칙


주의사항
모든 컴포넌트를 수동으로 구성합니다
명칭은 대소문자 구분

## 1. Host a Static Website

![image](/images/Day2-1.png)

사용하는 서비스 아이콘
객체간 상관관계
30분

### 1-1. Select a Region
- `[AWS Management Console]` ▷ 우측 상단 Region 부분에 `Asia Pacific (Seoul)` 선택

### 1-2. Create an S3 Bucket

이번 단계에서는 무슨 용도의 S3 버킷을 생성합니다

* `[AWS Management Console]` ▷ `[Find Services]` 검색창에 `S3` 입력
* `[Create bucket]`선택

  - Bucket name: `wildryde-firstname-lastname` # 그대로 적지 말고 이름부분을 반드시 변경!
  - Region: `Asia Pacific (Seoul)`
  - 확인 후 `[Create]`

### 1-3. Upload Content

이번 단계는 위에서 만든 S3 버킷에 무슨 용도의 컨텐츠를 업로드 합니다

* `[AWS Management Console]` ▷ `[S3]`

  - `1-2` 단계에서 만든 S3 버킷 선택
  - 현재 화면이 `Overview` 탭 위치에 있는지 확인
  
* 이 [링크](https://github.com/awslabs/aws-serverless-workshops/archive/master.zip) 파일을 로컬 PC로 다운로드
  
  - 적당한 위치에 압축 해제
  - 탐색기에서 `/WebApplication/1_StaticWebHosting/website` 하위 경로의 모든 파일 선택
  - 단, 이때 선택 대상에서 website 경로는 불포함
  - 위 S3 버킷의 `Overview` (웹브라우저) 화면 위로 `Drag and Drop`
  - 확인 후 `[Upload]`

### 1-4. Add a Bucket Policy to Allow Public Reads

### 1-5. Enable Website Hosting

### 1-6. Validate Your Implementation

giddy up 클릭시 에러처리까지 해놨네 ㅋㅋ

## 2. Manage Users

![image](/images/Day2-2.png)

30분

### 2-1. Create an Amazon Cognito User Pool

cognito에서 user 객체 확인 / 상태값 변경 확인

### 2-2. Add an App to Your User Pool

### 2-3. Update the config.js File in Your Website Bucket

### 2-4. Test Your Implementation


## 3. Bulid a Serverless Backend

![image](/images/Day2-3.png)

30분

### 3-1. Create an Amazon DynamoDB Table

### 3-2. Create an IAM Role for Your Lambda function

### 3-3. Create a Lambda Function for Handling Requests

node.js 6.10 deprecated
	8.10 런타임에서 도나?
	테스트상에는 문제없는듯
  
### 3-4. Test Your Implementation

## 4. Deploy a RESTful API

![image](/images/Day2-4.png)

15분


### 4-1. Create a New REST API

### 4-2. Create a Cognito User Pools Authorizer

### 4-3. Create a New Resource and Method

### 4-4. Deploy Your API

### 4-5. Update the Website Config

### 4-6. Validate Your Implementation

cloudwatch logs 확인
dynamodb item 확인


## 5. Terminate Resources

![image](/images/Day2-5.png)

10분

### 5-1. Delete Your Amazon S3 Bucket

### 5-2. Delete Your Amazon Cognito User Pool

### 5-3. Delete Your Serverless Backend

### 5-4. Delete Your REST API

### 5-5. Delete Your CloudWatch Log
