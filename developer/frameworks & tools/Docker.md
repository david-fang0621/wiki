## Docker의 개념

_Docker는 응용프로그람을 개발하고 배포하며 실행하기 위한_

- Build an image
  ```php
  docker build -t [image name] .
  ```
- Run container
  ```php
  docker run -dp 127.0.0.1:3000:3000 [image name]
  ```
- List containers
  ```php
  docker ps

  # Stop the container
  docker stop [the-container-id]

  # Remove the container
  docker rm [the-container-id]
  ```
- Push the image to Docker Hub
  ```php
  docker push docker/[image name]
  ```
