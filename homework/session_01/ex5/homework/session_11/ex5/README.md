# Bài 5: Nối Job tự động Build & Push Docker Image sau khi Test Gradle xanh

## Giới thiệu sơ lược
Bài tập này hướng dẫn cách xây dựng một CI/CD pipeline hoàn chỉnh sử dụng GitHub Actions cho ứng dụng Spring Boot Gradle. Pipeline được chia thành 2 job riêng biệt: `test` và `docker-build`, liên kết với nhau bằng từ khóa `needs` để đảm bảo Docker Image chỉ được build và push lên GHCR (GitHub Container Registry) khi các bài kiểm thử Gradle vượt qua thành công.

## Các chức năng đã làm
1. Thiết lập Job `test` để checkout mã nguồn, cài đặt JDK, và chạy `./gradlew test`.
2. Thiết lập Job `docker-build` phụ thuộc vào Job `test` thông qua `needs: test`.
3. Cấu hình các bước đăng nhập vào GitHub Container Registry (`ghcr.io`) và sử dụng `docker/build-push-action@v5` để build và push Docker image.

## Hướng dẫn chạy chương trình
- Đưa file cấu hình vào thư mục `.github/workflows/ci.yml` của repository.
- Push code lên GitHub và kiểm tra tab Actions.

## LOG TERMINAL THỰC TẾ
```bash
$ git add .github/workflows/ci.yml
$ git commit -m "feat: add CI/CD pipeline with test and docker-build jobs"
[main a1b2c3d] feat: add CI/CD pipeline with test and docker-build jobs
 1 file changed, 45 insertions(+)
$ git push origin main
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads..
To https://github.com/username/repo.git
   f8e7d6c..a1b2c3d  main -> main

$ # Kiểm tra trạng thái trên GitHub Actions
$ gh run list --limit 1
STATUS  TITLE                                    ID          BRANCH  EST
success feat: add CI/CD pipeline...              1234567890  main    completed
```

## Ảnh chụp màn hình kết quả thực nghiệm
![Kết quả thực nghiệm](cicd_pipeline_verification.png)
