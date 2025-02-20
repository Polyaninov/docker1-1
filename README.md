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
