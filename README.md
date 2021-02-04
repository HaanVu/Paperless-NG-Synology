# Paperless-NG-Synology

## Hướng dẫn cài đặt Paperless-ng (https://github.com/jonaswinkler/paperless-ng) trên Synology NAS

# Giới thiệu:
Paperless là 1 web-app container chạy trên nền tảng docker, thường đc cài đặt trên các sever.


## Tính năng bảo gồm:


- Scan OCR văn bản PDF và chuyển sang dạng text searchable PDF
- Lưu trữ văn bản và index văn bản trên database
- Paperless-ng (0.9.11)là 1 bản fork của Paperless với nhiều tính năng và cho phép truy cập mà ko cần qua VPN
- Đây là hướng dẫn cài Paperless-ng (0.9.11) trên Synology NAS
- Và gồm cách thức set-up scanner cho Paperless

    __Lưu ý__: Hướng dẫn chỉ cho phiên bản Paperless-ng 


__Điều kiện:__
- Synology NAS và DSM 5.2+
- RAM 2 GB

# Các bước cài đặt:

## Thu thập các files cần thiết
- Log in vào Synology NAS

- Truy cập vào Package Center 

     <img width="87" alt="Screen Shot 2021-02-04 at 10 27 33 AM" src="https://user-images.githubusercontent.com/78508001/106938261-9b071f80-66d3-11eb-9be8-cbb16f6a0dad.png">


- Download và cài đặt Docker, lưu ý không cài đặt Paperless-ng container trên docker store

    <img width="94" alt="Screen Shot 2021-02-04 at 10 29 20 AM" src="https://user-images.githubusercontent.com/78508001/106938440-da357080-66d3-11eb-9611-c6c034e964e7.png">

- Truy cập vào (https://github.com/jonaswinkler/paperless-ng/releases/tag/ng-0.9.11)

- Download paperless-ng-0.9.11-dockerfiles.tar.xz

- __Unpack__ và lưu 2 files: docker-compose.postgres.yml và docker-compose.env

- __Rename__ docker-compose.postgres.yml vừa down thành: docker-compose.yml

