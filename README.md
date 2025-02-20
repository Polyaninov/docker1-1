1. Запустить контейнер nginx:
создать и перенести в контейнер папку app (смонтировать в /usr/share/nginx/html)
в папке app создать файл index.html с таким содержимым
<Html>    
<Head>  
<title>  
Example of make a text B,I,U  
</title>  
</Head>  
<Body>   
<b> [This text is Bold......] </b>  
<I> [This text is Italic......] </I>  
<U> [This text is Underline......] </U>   
</Body>  
</Html> 
перенаправить порт 80 из контейнера на порт 8090 хоста
при выполнении curl на ip:port должна отдаваться страница из п2


sudo docker run -d -p 8090:80 -v ~/app:/usr/share/nginx/html --name mynginx nginx
curl 127.0.0.1:8090

devops@devops-Vir:~$ sudo docker inspect 6b51d63afb5c | grep -E '\b(IPAddress|Image|Volumes)\b'
        "Image": "sha256:97662d24417b316f60607afbca9f226a2ba58f09d642f27b8e197a89859ddc8e",
            "Image": "nginx",
            "Volumes": null,
            "IPAddress": "172.17.0.2",
                    "IPAddress": "172.17.0.2",



devops@devops-Vir:~$ sudo docker inspect 6b51d63afb5c | grep Image
        "Image": "sha256:97662d24417b316f60607afbca9f226a2ba58f09d642f27b8e197a89859ddc8e",
            "Image": "nginx",


2. Запустить контейнер с mongodb:
задать переменную ME_CONFIG_MONGODB_ADMINUSERNAME со значением admin
задать переменную ME_CONFIG_MONGODB_ADMINPASSWORD со значением adminpassword
создать директорию mongo_data и смонитировать ее внутрь контейнера в /data/db
вывесить дефолтный порт монги на хост

sudo docker run -d -p 27017:27017 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=admin -v ~/mongo_data:/data/db --name mongodb1  mongo

docker run -d --name mongo-express \
    -e ME_CONFIG_MONGODB_SERVER=mongo-container \
    -e ME_CONFIG_BASICAUTH_USERNAME=admin \
    -e ME_CONFIG_BASICAUTH_PASSWORD=password \
    -p 8081:8081 mongo-express

devops@devops-Vir:~$ sudo docker inspect 65684ba7d41b | grep -E '\b(IPAddress|Image|Volumes)\b'
        "Image": "sha256:6fe2220a3a52775d0ddfc59d6ca8140c80e5169c5c374f048b8a76f2f11820e7",
            "Image": "mongo",
            "Volumes": {
            "IPAddress": "172.17.0.3",
                    "IPAddress": "172.17.0.3",

    

3. Запустить контейнер с postgres 9:
задать переменную POSTGRES_PASSWORD со значением passwd
создать директорию pg_data и прокинуть ее в контейнер по пути /var/lib/postgresql/data

sudo docker run -d \
  --name my_postgres \
  -e POSTGRES_PASSWORD=passwd \
  -v ~/pg_data:/var/lib/postgresql/data \
  -p 5432:5432 \
  postgres:9

sudo docker exec -it my_postgres psql -U postgres

devops@devops-Vir:~$ sudo docker inspect e87876b388cb | grep -E '\b(IPAddress|Image|Volumes)\b'
        "Image": "sha256:027ccf656dc121a26b53cac03415d4326a75bf2751f177210d47793754e8b316",
            "Image": "postgres:9",
            "Volumes": {
            "IPAddress": "172.17.0.4",
                    "IPAddress": "172.17.0.4",


