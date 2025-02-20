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


sudo docker run -d -p 27017:27017 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=admin -v ~/mongo_data:/data/db --name mongodb1  mongo

docker run -d --name mongo-express \
    -e ME_CONFIG_MONGODB_SERVER=mongo-container \
    -e ME_CONFIG_BASICAUTH_USERNAME=admin \
    -e ME_CONFIG_BASICAUTH_PASSWORD=password \
    -p 8081:8081 mongo-express


sudo docker run -d \
  --name my_postgres \
  -e POSTGRES_PASSWORD=passwd \
  -v ~/pg_data:/var/lib/postgresql/data \
  -p 5432:5432 \
  postgres:9

sudo docker exec -it my_postgres psql -U postgres
