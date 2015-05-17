# Development flow with LAMP in docker

- [install docker](https://docs.docker.com/installation/)

  ```bash
  wget -qO- https://get.docker.com/ | sh
  ```

- [install docker-compose](https://docs.docker.com/compose/install/)
- place your code in ***./app*** folder
- build docker image

  ```bash
  docker-compose build
  ```
  
- run docker container
 
  ```bash
  docker-compose up -d
  ```

- open ```http://127.0.0.1``` 
