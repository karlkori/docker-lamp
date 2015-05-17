# Development flow with LAMP in docker
After running docker container, you will can edit your app in ./app folder, all changes will be immediately sync with container and app will be available at ```http://127.0.0.1```

  - ./app - your application code
  - ./mysql - all your mysql databases
  - ./logs - all Apache logs

### Install

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
