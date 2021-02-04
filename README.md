# Paperless-NG-Synology

## Hướng dẫn cài đặt Paperless-ng 0.9.11 (https://github.com/jonaswinkler/paperless-ng) trên Synology NAS

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

- Download: __paperless-ng-0.9.11-dockerfiles.tar.xz__

- __Unpack__ và lưu 2 files: docker-compose.postgres.yml và docker-compose.env

- __Rename__ docker-compose.postgres.yml vừa down thành: docker-compose.yml

# Thiết lập trên Synology
- Log in vào Synology
- Tạo 1 folder docker trong Volume1
- Bên trong docker folder tạo folder paperless-ng để chứa container
- Copy 2 files docker-compose.yml và docker-compose.env vào folder paperless-ng
- Bên trong folder paperless-ng lần lượt tạo thêm 4 folders tên: 

        data


        media


        export


        consume
- Cần cho phép thâm nhập vào Synology NAS qua SSH
- Vào Control Panel -> Terminal and SNMP, chọn Enable SSH service, tuỳ port, default là port 22 và nhấn Apply
# Thiết lập paperless-ng trên Synology
Các bước kế tiếp cần thao tác trên PC khác bất kì hệ OS.

Chỉnh đổi file docker-compose.yml, có thể open file bằng bất kì text reader nào để sửa (notepad/PC, TextEdit/MacOS, etc…)

### Chỉnh file docker-compose.yml theo các bước sau:
Thay line docker-compose.yml trong (copy/paste)

    - pgdata:/var/lib/postgresql/data
Thay bằng:

    - /volume1/docker/paperless-ng/database:/var/lib/postgresql/data

Tiếp thay 4 lines trong file docker-compose.yml

      - data:/usr/src/paperless/data
      - media:/usr/src/paperless/media
      - ./export:/usr/src/paperless/export
      - ./consume:/usr/src/paperless/consume

Thay 

      - /volume1/docker/paperless-ng/data:/usr/src/paperless/data
      - /volume1/docker/paperless-ng/media:/usr/src/paperless/media
      - /volume1/docker/paperless-ng/export:/usr/src/paperless/export
      - /volume1/docker/paperless-ng/consume:/usr/src/paperless/consume

    
