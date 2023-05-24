# laba07
Устанавливаем докер
```
sudo apt update && sudo apt install -y curl
curl -fsSL https://get.docker.com/ | sudo sh
```
создаем cpp файл hello_world
```
#include <iostream> 
 
int main() { 
std::cout << "Hello world" << std::endl; 
}
```

создаем CMakeLists.txt

```
cmake_minimum_required(VERSION 3.2) 
 
project (project_hw) 
 
add_executable(hello_world_app 
    hello_world.cpp 
) 
 
install(TARGETS hello_world_app hello_world_app RUNTIME DESTINATION /bin)
```

создаем докерфайл
```
cd laba07
FROM ubuntu:18.04 

RUN apt update 
RUN apt install -yy gcc g++ cmake
 
RUN mkdir hello_world 
COPY . hello_world/ 
WORKDIR hello_world 
RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install 
RUN cmake --build _build 
RUN cmake --build _build --target install
 
ENTRYPOINT ./_build/hello_world_app 
```
```
sudo docker build -t hello_world .
```
![изображение](https://github.com/Wenir04/laba07/assets/113133600/aa073635-a46b-4f31-972f-9ff6fb0cf9a4)

Возникает ошибка с permission 
```
sudo groupadd docker
sudo usermod -aG docker ${USER}
su - ${USER}
```
теперь можем запускать докер
```
docker run hello_world

```
![изображение](https://github.com/Wenir04/laba07/assets/113133600/45b574a1-f61b-4c91-8390-6fa81c133fdb)
