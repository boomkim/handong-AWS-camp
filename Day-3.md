# 한동대 AWS Camp Day-3 

## Big Data 


## AI/ML - Sagemaker: 번역 ML 모델 학습 

### 1. S3 버킷 생성

* AWS 콘솔 Sign in -> S3 콘솔 접속 
* AWS S3 버킷 생성 `sagemaker-{userid}`

### 2. Notebook instance 생성 

* Sagemaker 콘솔 접속 
* 좌측 `Notebook Instance` -> `Create notebook instance` 클릭 
* instance 이름: `{username}-workshop` 
* 인스턴스 타입: `ml.m4.xlarge`
* IAM Role: `Create a new role` 
* (팝업창에서) Specific S3 Buckets: `sagemaker-{userid}` (위에서 생성한 버킷) 입력 후 `Create role`
* 다시 Create Notebook instance 페이지로 돌아온 뒤 `Create notebook instance` 를 클릭합니다.

### 3. Notebook Instance 접근 

* 서버 상태가 `InService` 로 바뀔 때까지 기다립니다. 보통 5 분정도의 시간이 소요 됩니다.
* `InService` 가 된 후 Open을 클릭하면 Notebook으로 접속할 수 있습니다. 

### 4. 실습용 코드 다운로드 

* 터미널 실행 (우측에 `New` -> `Terminal`)
* 터미널에서 깃 클론 
```bash
cd SageMaker/
git clone https://github.com/boomkim/handong-AWS-camp.git
```

