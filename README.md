- - - - -
# Giải thích ý nghĩa từng dòng trong dockerfile
- - - - -

## Start your image with a node base image
FROM node:18-alpine
- Chỉ ra là cái dockerimage được xây dựng dựa trên cái docker image nào

## The /app directory should act as the main application directory
WORKDIR /app
- Chỉ ra rằng chúng ta sẽ làm việc ở bên trong những thư mục nào
- Khởi tạo thư mục App
- Nếu có dòng này thì mặc định nhảy vào Docker container sẽ vào thư mục App

## Copy the app package and package-lock.json file
COPY package*.json ./
- Copy những file từ trong máy của chúng ta vào trong docker image
- Copy tất cả các file có đuôi .json vào trong thư mục App

## Copy local directories to the current local directory of our docker image (/app)
COPY ./src ./src
COPY ./public ./public
- VD: Copy thư mục src từ máy cá nhân vào trong thư mục src của docker image


## Install node packages, install serve, build the app, and remove dependencies at the end
RUN npm install \
    && npm install -g serve \
    && npm run build \
    && rm -fr node_modules
- Cài đặt những thư viện, packet gì vào trong docker image. "\" cái này là chạy trên nhiều dòng

EXPOSE 3000
- Thường dùng Docker chạy các ứng dụng web. Nó sẽ mở 1 cái cổng ở trong docker container, kết nối cổng này với 1 cổng trên máy của chúng ta để khi nào lauch 1 cái web trong docker contaiter thì chúng ta có thể truy cập web đó trên máy của chúng ta 

## Start the app using serve command
CMD [ "serve", "-s", "build" ]
- Muốn chạy những câu lệnh gì khi chạy docker container. VD: serve -s build
- Nếu viết nhiều câu lệnh này nó cũng sẽ chỉ nhận và thực thi câu lệnh cuối cùng thôi


- - - - -
Build docker image
- - - - -

## Build your first
docker build -t welcome-to-docker .
- paste vào trong thư mục mình cần build
![image](https://github.com/user-attachments/assets/22b677d4-279a-4cac-8654-b45c89c400b5)

## Run container từ Docker image ta vừa mới Build
- Image
![image](https://github.com/user-attachments/assets/95780b25-252b-431f-ae99-efa41bced69a)
- Click vào Docker image vừa được tạo
![image](https://github.com/user-attachments/assets/25244ee0-54fd-49e3-8b68-2485fa076062)
- Click Run
![image](https://github.com/user-attachments/assets/3e162b0e-55a3-4b2a-a4a6-e5d522e7dd03)
![image](https://github.com/user-attachments/assets/b9f1f4a6-ba70-4b10-b9bf-5a161993975a)
![image](https://github.com/user-attachments/assets/5371d942-d201-42dd-8155-92c7e47f457e)

- Click Run
![image](https://github.com/user-attachments/assets/b13427c9-f285-4b73-9550-4f5c9d36fc6d)
-- Đây chính là chỗ Mesh cổng 3000 ở bên trong Docker container với cổng 8080 trên máy của chúng ta
- Kết quả
![image](https://github.com/user-attachments/assets/827ccf96-076b-424d-a741-3d7cae5d9bac)







