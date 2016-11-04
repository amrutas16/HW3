## HW3 - Queues, Caches and Proxies

### Setup
Install redis  
Start redis server by the command ```redis-server```  
Install dependencies by running ```npm install```  
Run ```sudo node main.js```  to start 

### Tasks  
- set/get: On visiting ```/set```, a key is set with a message. On visiting ```/get```, the message is displayed. This message expires in 10 sec.  
- recent: On visiting ```/recent```, the 5 most recently visted urls will be displayed. They are stored in a redis queue, and are fetched from there. I have used ltrim, lrange and lpush to store them. 
- upload: On visiting ```/upload```, an image is uploaded by running the command   
 ```curl -F "image=@./img/morning.jpg" localhost:3000/upload```  
 I have used lpush to store these images in a redis queue.  
- meow: On visiting ```/meow```, the most recent image will be displayed. I have used lpop to remove the image from the queue after it has been displayed.  
- spawn: On visiting ```/spawn```, a new app server is created. I have used a count for the port number on which the server will run. After a server is created, the count is incremented. I have used ```lpush``` to store the port numbers in the queue.  
- destroy: On visiting ```/destroy```, a random number between 1 and the number of new ports will be generated. This server will be destroyed, i.e, it will be removed from the queue. I have used ```lrem``` to remove it from the queue.  
- listservers: On visiting ```listservers```, the port numbers will be fetched from the redis queue and will be displayed on the webpage. I have used ```lrange``` for this purpose.  
- proxy server: A proxy server is created on port number 80. I have used the ```http-proxy``` library for this purpose. I have used two servers on port numbers 3000 and 3001. These are stored in a redis queue. Everytime ```http://localhost``` is visited, it will redirect to ```http://localhost:3000``` and ```http://localhost:3001``` alternately. I have used `rpoplpush` to toggle between the two.   

### Screencast
[Link](https://youtu.be/mb7rp4aHuc0)