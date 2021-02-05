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

    
__Save lại__, có thể tuỳ ý thay đổi path theo ý muốn cho phù hợp, đây chỉ là hướng dẫn cho folder docker/paperless-ng được tạo trong volume1 của NAS

## Compile paperless-ng
- Log in vào Synology
- Truy cập SSH với user root or admin vào Synology NAS (Putty or Terminal...) theo setting đã chọn ở bước trên


    ssh root@xxx.xxx.xx.xx
- Di chuyển tới folder paperless-ng (volume1/docker/paperpless-ng)
- Nhập lệnh để compile container paperles-ng

        docker-compose up -d

- Đợi tạo container hoàn thành healthy và không lỗi
- Tiếp nhận lệnh sau để tạo account superuser cho paperless-ng app

        docker-compose run --rm webserver createsuperuser
- Tạo admin account tuỳ ý

## Hướng dẫn sử dụng paperless-ng
- Paperless-ng container sẽ tự động chạy khi NAS bật
- Truy cập vào port của paperless để xác nhận, theo default port là 7300
- Vào browser truy cập tới port của paperless-ng trên Synology NASintit
        
        192.168.xx.xx:7300 
- Nhập username và password đã chọn


# Chúc mứng bạn đã bắt đầu sử dụng paperless-ng

 
 |


 |

 |

 |

 |

 |






# OPTIONAL 
## Scanner cho paperless-ng
Các bước sau dành cho ai muốn dùng máy scan dữ liệu về paperless-ng
__
Chỉ áp dụng cho máy __Scanner có hộ trợ transfer file qua FTP__

- Log in vào Synology NAS
- Chọn __Control Panel__

 <img width="300" alt="Screen" src="https://user-images.githubusercontent.com/78508001/107071942-4ed2e280-679a-11eb-801d-2b077e006433.png">

 - Vào __Shared Folder__ tạo Folder mới trong volume1, đặt tên bất kì, tạm đặt là FTP

 <img width="92" alt="Screen Shot 2021-02-05 at 10 25 52 AM" src="https://user-images.githubusercontent.com/78508001/107073706-8b074280-679c-11eb-9f20-1a7308eb0235.png">


- Choose __User__

 <img width="200" alt="Screen Shot 2021-02-05 at 10 11 28 AM" src="https://user-images.githubusercontent.com/78508001/107072087-85a8f880-679a-11eb-8f7b-a0bfd09f2e19.png">

 - Tạo account mới tên bất kì, trong bài sẽ tạm đặt là __FTP__ , password tuỳ chọn
 
- Chuyển sang phần __File Services__


 <img width="150" alt="Screen Shot 2021-02-05 at 10 14 25 AM" src="https://user-images.githubusercontent.com/78508001/107072413-edf7da00-679a-11eb-9c4f-5a995e532e01.png">

- Chọn Tab __FTP__, nhấn enable __FTP__ 

<img width="797" alt="Screen Shot 2021-02-05 at 10 15 40 AM" src="https://user-images.githubusercontent.com/78508001/107072586-1b448800-679b-11eb-895e-4f0419951293.png">

- Vẫn ở Tab __FTP__, kéo xuống dưới phần General
<img width="584" alt="Screen Shot 2021-02-05 at 10 17 15 AM" src="https://user-images.githubusercontent.com/78508001/107072778-534bcb00-679b-11eb-892a-c943459d1a97.png">

- Click __Advanced Setting__ sau đó cho phép __Change user root directories__

<img width="256" alt="Screen Shot 2021-02-05 at 10 22 21 AM" src="https://user-images.githubusercontent.com/78508001/107073297-09afb000-679c-11eb-855e-443da556c642.png">

|


|



- Sau đó click vào Select User

<img width="487" alt="Screen Shot 2021-02-05 at 10 31 08 AM" src="https://user-images.githubusercontent.com/78508001/107074217-44661800-679d-11eb-8e52-d29e5cd481d3.png">

- Phần usber or group, chọn drop down menu chọn user FTP vừa tạo
- Click Shared folder, chọn folder FTP vậy,

## Chỉ dẫn setup scanner

Một số scanner phù hợp đã có listed bên paperless-ng, có thể tham khảo trong phần documentation bên paperless-ng

Cài đặt scanner chuyển ftp tới Synology NAS. Do tuỳ scanner nên không có hình cụ thể. 

Địa chỉ dựa theo user đã tạo trong bài là

    FTP@xxx.xxx.xx.xx

Toàn bộ file scan sẽ đước chuyển về folder FTP đã tạo trong volume1

## Chuyển file về paperless-ng

Quay lại về giao diện Synology
Chọn Control Panel vào phần Task Scheduler

<img width="200" alt="Screen Shot 2021-02-05 at 10 37 59 AM" src="https://user-images.githubusercontent.com/78508001/107074887-38c72100-679e-11eb-91e8-9e528b9790d2.png">

Click vào Create

<img width="463" alt="Screen Shot 2021-02-05 at 10 39 27 AM" src="https://user-images.githubusercontent.com/78508001/107075046-6dd37380-679e-11eb-84eb-864ceffa067e.png">

Tạo task dưới quyền admin, tên bất kì, trong bài đặt là "Move to"

<img width="516" alt="Screen Shot 2021-02-05 at 10 40 36 AM" src="https://user-images.githubusercontent.com/78508001/107075163-98253100-679e-11eb-8a32-01f209612f91.png">

Chuyển sang tab Task Setting

<img width="511" alt="Screen Shot 2021-02-05 at 10 41 45 AM" src="https://user-images.githubusercontent.com/78508001/107075270-c0149480-679e-11eb-90e2-4067eb7a6ac7.png">

Trong __Run command__ copy đoạn script

    mv  /volume1/fpt/*  /volume1/docker/paperless-ng/consume

Về phần __Schedule__, cài đặt thời gian cho script, trong hướng run script sẽ chạy mỗi phút

<img width="520" alt="Screen Shot 2021-02-05 at 10 43 36 AM" src="https://user-images.githubusercontent.com/78508001/107075474-02d66c80-679f-11eb-83ee-27dde0facf3c.png">


Như vậy đã mỗi khi scanner gửi file vế FTP folder, toàn bộ file trong FTP sẽ được chuyển về paperless-ng/consume
paperless-ng sẽ xử lý tiếp

# Vậy là xong, thank you for reading!




