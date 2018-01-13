# Hướng dẫn đóng gói ASP.net MVC Core vào Docker Image
## Muốn thử ngay mã nguồn
```sh
git clone https://github.com/TechMaster/DockerizeASPnetMVCCore
cd DockerizeASPnetMVCCore
docker build -t himvc .
docker run --name himvc -d -p 80:5000 himvc:latest
curl http://localhost
```
## Bước 1: Tạo project
```sh
dotnet new mvc -n himvc
dotnet restore
dotnet run
```

## Bước 2: Sử dụng chỉnh sửa nội dụng ứng dụng
Hãy chú ý đến 3 thư mục sau:
- Views: nếu sửa trang web sẽ cập nhật theo
- Controllers: nếu sửa phải biên dịch - chạy lại
- Models: tạm thời không động đến
## Bước 3: Viết Dockerfile
Phần này rất giống với bài trước [https://github.com/TechMaster/DockerizeDotNetCoreConsoleApp](https://github.com/TechMaster/DockerizeDotNetCoreConsoleApp)

Ở phần tạo Docker image với ASP.net Core runtime
```
EXPOSE 5000/tcp                     # Mở cổng 5000 trong docker container
ENV ASPNETCORE_URLS http://*:5000   # Khai báo biến môi trường để web server phục vụ ở cổng 5000
ENTRYPOINT ["dotnet", "himvc.dll"]
```
## Bước 4: .dockerignore
Hãy loại bỏ những thư mục, file sau đây trong phase 1 biên dịch ứng dụng trong Docker image ASP.net Core SDK
```
obj/
bin/
.vscode/
out/
ReadMe.md
Dockerfile
Dockerfile.globalization
```

## Bước 5: Giờ thì chiến thôi
```
docker build -t himvc .
docker run --name himvc -d -p 80:5000 himvc:latest
curl http://localhost
```
Nhớ đẩy code lên github để lưu lại, đừng để trong ổ cứng làm chi.