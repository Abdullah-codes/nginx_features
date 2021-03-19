# nginx.conf congrigation for rate limiting

1) download nginx.conf file replace that file with your deafult nginx file from /etc/niginx/

2)download demo file wich has  (index.html thumb.png and style.css)

2)now from downloaded file(nginx.conf) replace root as per  location where you stored demo file, so nginx can serve those files from that location 
for example I stored it in /home/user/sites/demo

3)save new confrigation 

4)check sytanx is ok with  ``` sudo nginx -t ``` command 

## Rate limiting confrigation-----------
						

* now to check rate limiting we will use siege 

2) open terminal and run (siege -v -r 2 -c 5  http://localhost/thumb.png) you will see 10 hits in blue color it means all the req we sent came back with response 200 ok it means all req were succsefull.

3) we will now apply rate limiting . open nginx config file and uncomment the limit_req_zone wich is in http contex , and now uncomment limit_req from location /  block.  it means we have limited the requets for (1 requests per second)  

4) save the confrigation check  for syntax and now reload nginx with ``` systemctl reload nginx ``` command.

5) now we will again check for rate limiting by using siege command. run this command in terminal (siege -v -r 2 -c 5  http://localhost/thumb.png) now you can see only one req is in blue and others are in red it means only 1 req was accepted by nginx server per second and others were rejected.
thats how we aplly rate limiting.
