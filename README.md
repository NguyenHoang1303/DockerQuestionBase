
### 1. Docker là gì?
- Docker là một nền tảng để cung cấp cách để building, deploying và running ứng dụng dễ dàng hơn bằng cách sử dụng các containers (trên nền tảng ảo hóa). Ban đầu viết bằng Python, hiện tại đã chuyển sang Golang.
- Hiểu đơn giản là việc đóng gói tất cả ứng dụng của bạn, tất cả những thứ cần thiết thành containers. 
### 2. Containers là gì?
- Các containers cho phép lập trình viên đóng gói một ứng dụng với tất cả các phần cần thiết, chẳng hạn như thư viện và các phụ thuộc khác, và gói tất cả ra dưới dạng một package.
### 3. Images là gì?
- Docker image là một ảnh của một môi trường phát triển (có thể hiểu là snapshot).
- Nói ngắn gọn là chúng ta có thể gói các cài đặt môi trường (OS, package, phần mềm của chúng ta đã viết, …) lại thành 1 cục duy nhất, đó chính là docker image. Khi đã có docker image, ta có thể khởi tạo các docker container từ docker image.
### 4. Dockerfile là gì?
- là 1 file hướng dẫn build ra các images. Ví dụ:
    ```
    FROM openjdk:8-jdk-alpine
    COPY docker2.jar /
    ENTRYPOINT ["java", "-jar", "docker2.jar"]
    ```
        

 + FROM: môi trường chạy.
 + COPY : copy file docker2.jar từ máy thật vào trong image có đường dẫn / .
 + ENTRYPOINT: khá giống CMD đều dùng để chạy khi khởi tạo container, nhưng ENTRYPOINT không thể ghi đè từ dòng lệnh khi khi khởi tại container.
### 5. File docker-compose.yml để làm gì?
- docker-compose.yml dùng để chạy các Dockerfile. Ví dụ:
    ```
    version: "3"
    services:
      mysqldb_db:
        image: mysql:5.7
        environment:
          - MYSQL_USER=root
          - MYSQL_ROOT_PASSWORD=12345
          - MYSQL_DATABASE=docker1_db
        ports:
          - 3307:3306
    
        volumes:
          - mysqldb:/var/lib/mysql
      docker1-app:
        depends_on:
          - mysqldb
        build: doker1-compose
        ports:
          - 8050:8080
        environment:
          SPRING_APPLICATION_JSON: '{
                "spring.datasource.url"  : "jdbc:mysql://mysqldb:3306/docker1_db?useSSL=false",
                "spring.datasource.username" : "root",
                "spring.datasource.password" : "12345",
                "spring.jpa.properties.hibernate.dialect" : "org.hibernate.dialect.MySQL5InnoDBDialect",
                "spring.jpa.hibernate.ddl-auto" : "update"
              }'
    volumes:
      mysqldb:
    ```
- Một số từ khóa trong docker-compoese.yml
	+ version: chỉ ra phiên bản docker-compose đã sử dụng.
    + services: thiết lập các services(containers) muốn cài đặt và chạy.
    + image: chỉ ra image được sử dụng trong lúc tạo ra container.
    + build: dùng để tạo container.
    + ports: thiết lập ports chạy tại máy host và trong container.
    + enviroment:  thiết lập biến môi trường ( thường sử dụng trong lúc config các thông số của db).
    + volumes: dùng để mount hai thư mục trên host và container với nhau.
### 6. Docker system prune thực hiện công việc gì?
- This will remove:
    + all stopped containers
    + all networks not used by at least one container
    + all dangling images
    + all build cache
### 7. Docker compose up thực hiện điều gì?
- khởi tạo và chạy các container. Có thể thêm các option là -d và –force-recreate:
    + -d: thì các container chạy dưới dạng background.
    + --force-recreate : tái tạo lại các container.
- docker compose down thì xóa hết những gì được tạo từ lệnh up.
### 8. Sự khác nhau giữa docker run và docker exec?
- run: chạy 1 images để build 1 container.
- exec: thực thi các câu lệnh bên trong container đang hoạt động.
### 9. Một số lệnh thao tác với docker Image thường dùng?
- docker images : show danh sách các image đã cài đặt.
- docker rmi <id/Name> : xóa 1 image theo id hoặc name.
- docker rmi -f <id/name> : xóa 1 image kể cả khi đang chạy.
### 10. Một số lệnh thao tác với docker Container thường dùng?
- docker ps : show danh sách các container đang chạy.
- docker ps -a : show danh sách các container đang chạy và đã tắt
- docker inspect { id_container } : xem chi tiết của container được tạo ra.
- docker logs { id_container } : xem lịch sử container.
-  docker rm <id/name> : xóa 1 container.
- docker rm -f <id/name> : xóa 1 container kể cả khi nó đang chạy.
- docker rm $(docker ps -a -q) :  xóa tất cả container.
