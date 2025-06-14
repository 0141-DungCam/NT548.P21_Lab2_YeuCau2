# NT548.P21_Lab2_YeuCau2
# Triển khai hạ tầng AWS & Tự động hóa CI/CD với CloudFormation và CodePipeline

Repository này chứa các file YAML dùng để:
- Triển khai hạ tầng AWS bằng AWS CloudFormation.
- Tự động hóa quy trình build và deploy ứng dụng với AWS CodePipeline.

## Yêu cầu

- Tài khoản AWS với quyền đủ để tạo/điều chỉnh các dịch vụ (CloudFormation, S3, IAM, CodePipeline, CodeBuild, v.v.)
- AWS CLI cài đặt trên máy tính cá nhân (tham khảo: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
- Quyền truy cập IAM phù hợp cho các thao tác tạo stack, khởi tạo pipeline.

## Hướng dẫn sử dụng

### 1. Cấu hình AWS CLI

Trước tiên, bạn cần cấu hình AWS CLI với Access Key và Secret Key:

```bash
aws configure
```

### 2. Triển khai hạ tầng bằng CloudFormation

Chạy lệnh sau để tạo stack từ file YAML (ví dụ: infra.yaml):

```bash
aws cloudformation create-stack \
  --stack-name TenStackCuaBan \
  --template-body file://infra.yaml \
  --capabilities CAPABILITY_NAMED_IAM
```

**Lưu ý:**  
- Thay đổi `infra.yaml` thành tên file template bạn muốn sử dụng.
- Thêm tham số `--parameters` nếu template yêu cầu các biến đầu vào.

Ví dụ:

```bash
aws cloudformation create-stack \
  --stack-name MyPipelineStack \
  --template-body file://codepipeline.yaml \
  --parameters ParameterKey=RepoName,ParameterValue=NT548.P21_Lab2_YeuCau2 \
  --capabilities CAPABILITY_NAMED_IAM
```

### 3. Quản lý stack

- Xem danh sách stack:
  ```bash
  aws cloudformation list-stacks
  ```
- Xóa stack:
  ```bash
  aws cloudformation delete-stack --stack-name TenStackCuaBan
  ```

### 4. Giám sát và chạy CodePipeline

Sau khi triển khai thành công, truy cập AWS Console để kiểm tra trạng thái CodePipeline hoặc sử dụng CLI:

```bash
aws codepipeline list-pipelines
aws codepipeline get-pipeline-execution --pipeline-name TenPipelineCuaBan --pipeline-execution-id <execution-id>
```

## Tham khảo

- [AWS CloudFormation Documentation](https://docs.aws.amazon.com/cloudformation/index.html)
- [AWS CodePipeline Documentation](https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome.html)
- [AWS CLI User Guide](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-welcome.html)
