# task5
1.  Created a `Dockerfile` in newly created directory with following content:
```console
FROM nginx
COPY index.html /var/lib/docker/volume/my_volume/nginx
```
2.  Create an `index.html` file in same directory with following content:
```console
  GNU nano 6.2                                                      index.html                                                               
<!doctype html>
<html lang="en">
<head>
<p>Hello, World!</p>
</head>
<body>
</html>
```
3.  Create a `docker-compose.yml` file in same directory with following content:
```yml
version: '3'
services:
  web:
   build: .
   ports:
   - "8080:80"
   volumes:
   - /var/lib/docker/volumes/my_volume/nginx:/usr/share/nginx/html

  db:
   image: mysql
   volumes:
   - /var/lib/docker/volumes/my_volume/mysql:/var/lib/mysql
   environment:
    MYSQL_ROOT_PASSWORD: mysql
    MYSQL_DATABASE: mysql
    MYSQL_USER: mysql
    MYSQL_PASSWORD: mysql
   ports:
   - "8081:3306"
   ```
4. Run the following command to UP the containers:
   ```console
   $ docker compose up -d
   ```
5. The running two containers are as shown:
   ![image](https://user-images.githubusercontent.com/126319802/228717894-541efa55-9d02-4ba4-bc40-a3f34ce046d2.png)
6.  Here is the output of `localhost:8080`
![image](https://user-images.githubusercontent.com/126319802/228718335-e746c2ee-ebd3-4cf0-9919-8ca444eb86e5.png)

7.  after making some changes in docker file and rebuilding image, below is the new message that is hown:
![image](https://user-images.githubusercontent.com/126319802/228720359-ab1c79a3-9816-4bd8-b215-75788ccd1ccd.png)
8.  For scalling, `docker-compose.yml` is edited as followed:
```yml
version: '3'
services:
  web:
   build: .
   volumes:
   - /var/lib/docker/volumes/my_volume/nginx:/usr/share/nginx/html

  db:
   image: mysql
   volumes:
   - /var/lib/docker/volumes/my_volume/mysql:/var/lib/mysql
   environment:
    MYSQL_ROOT_PASSWORD: mysql
    MYSQL_DATABASE: mysql
    MYSQL_USER: mysql
    MYSQL_PASSWORD: mysql
   ports:
   - "8081:3306"
   ```
9. Run the following command:
   ```console
   $ docker-compose up -d --scale web=5
   ```
10. the successfull output is:
![image](https://user-images.githubusercontent.com/126319802/228722322-e3181b3f-36fb-4ca6-b2e8-3b6cb5047df1.png)
11. To install `Grafana`, run following command:
```console
$ docker run -d -p 3000:3000 grafana/grafana-enterprise
 ```
12. browse `localhost:3000` and enter `admin` as both username and password. 
13. ![image](https://user-images.githubusercontent.com/126319802/228752592-655bf947-d094-4b19-a170-118d59cdc3fe.png)
