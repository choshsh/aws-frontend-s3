# aws-frontend-s3

정적 호스팅을 위해 vue로 작성된 프로젝트를 빌드하고 아티팩트를 s3로 업로드하는 GitHub Action.

## Repo Secret 만들기

| 키 | 설명 |
| --- | --- |
| AWS_ACCESS_KEY_ID | IAM 액세스 키 |
| AWS_SECRET_ACCESS_KEY | IAM 액세스 비밀번호 |
| AWS_S3_NAME | S3 버킷 이름 |
| AWS_S3_REGION | S3 리전 |

## AWS IAM 설정

- `AmazonS3ReadOnlyAccess` 관리형 정책 추가
- 인라인 정책 추가
    
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "VisualEditor0",
                "Effect": "Allow",
                "Action": "s3:PutObject",
                "Resource": "arn:aws:s3:::<버킷 이름>/*"
            }
        ]
    }
    ```
    

## AWS S3 설정

- 퍼블릭 액세스 차단 비활성
- 버킷 정책 편집
    
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "GetObjectsInBucket",
                "Effect": "Allow",
                "Principal": "*",
                "Action": "s3:GetObject",
                "Resource": "arn:aws:s3:::<버킷 이름>/*"
            }
        ]
    }
    ```