- - - - -
Giải thích ý nghĩa từng dòng trong dockerfile
- - - - -

## Start your image with a node base image
FROM node:18-alpine
- Chỉ ra là cái dockerimage được xây dựng dựa trên cái docker image nào

## The /app directory should act as the main application directory
WORKDIR /app
- Chỉ ra rằng chúng ta sẽ làm việc ở bên trong những thư mục nào

## Copy the app package and package-lock.json file
COPY package*.json ./
- Copy những file từ trong máy của chúng ta vào trong docker image

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
-Thường dùng Docker chạy các ứng dụng web. Nó sẽ mở 1 cái cổng ở trong docker container, kết nối cổng này với 1 cổng trên máy của chúng ta để khi nào lauch 1 cái web trong docker contaiter thì chúng ta có thể truy cập web đó trên máy của chúng ta 

## Start the app using serve command
CMD [ "serve", "-s", "build" ]
- Muốn chạy những câu lệnh gì khi chạy docker container. VD: serve -s build
- Nếu viết nhiều câu lệnh này nó cũng sẽ chỉ nhận và thực thi câu lệnh cuối cùng thôi

