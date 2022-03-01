# DockerQuestionBase

### Docker là gì?
 	- Docker là công cụ giúp các nhà phát triển tạo và duy trì các ứng dụng của họ 1 cách dễ dàng và có tổ chức. Hiểu đơn giản là việc đóng gói tất cả ứng dụng của bạn, tất cả những thứ cần thiết thành containers. 
### Containers là gì?
	- là các công cụ mà Docker sử dụng để đóng gói và vận chuyển các ứng dụng của  nhà phát triển đến điểm nơi mà họ muốn sử dụng.
### Images là gì?
    - Images được sử dụng đẻ tạo nên các container trong Docker.
### Dockerfile là gì?
    -  là 1 file hướng dẫn build ra các images.
### docker system prune thực hiện công việc gì?
- This will remove:
    + all stopped containers
    + all networks not used by at least one container
    + all dangling images
    + all build cache
### docker compose up thực hiện điều gì?
- khởi tạo và chạy các container. Có thể thêm các option là -d và –force-recreate:
    + -d: thì các container chạy dưới dạng background.
    + --force-recreate : tái tạo lại các container.
- docker compose down thì xóa hết những gì được tạo từ lệnh up.
### Sự khác nhau giữa docker run và docker exec?
- run: chạy 1 images để build 1 container.
- exec: thực thi các câu lệnh bên trong container đang hoạt động.
### 1 số lệnh thao tác với docker Image thường dùng?
- docker images : show danh sách các image đã cài đặt.
- docker rmi <id/Name> : xóa 1 image theo id hoặc name.
- docker rmi -f <id/name> : xóa 1 image kể cả khi đang chạy.
### 1 số lệnh thao tác với docker Container thường dùng?
- docker ps : show danh sách các container đang chạy.
- docker ps -a : show danh sách các container đang chạy và đã tắt
- docker inspect { id_container } : xem chi tiết của container được tạo ra.
- docker logs { id_container } : xem lịch sử container.
-  docker rm <id/name> : xóa 1 container.
- docker rm -f <id/name> : xóa 1 container kể cả khi nó đang chạy.
- docker rm $(docker ps -a -q) :  xóa tất cả container.
