


# ๐ 1. ์ฒ์์ผ๋ก nginx ์ค์น ํ setting ํ  ๋

**โ๏ธ nginx๋ฅผ ๋ค์ด ๋ฐ๋๋ค.**

```shell
# ์ค์น
sudo apt-get install nginx

# ์ค์น ํ์ธ ๋ฐ ๋ฒ์  ํ์ธ
nginx -v
```


&nbsp;


**โ๏ธ letsencrypt ์ค์น๋ฅผ ์ํด ๋ค์๊ณผ ๊ฐ์ ์์๋ก ๋ช๋ น์ด๋ฅผ ์๋ ฅ**

```shell
sudo apt-get install letsencrypt

sudo systemctl stop nginx

sudo letsencrypt certonly --standalone -d www์ ์ธํ ๋๋ฉ์ธ ์ด๋ฆ
```


์ด๋ ๊ฒ ํ ํ, "Congratulations!"๋ก ์์ํ๋ ๋ฌธ๊ตฌ๊ฐ ๋ณด์ด๋ฉด, ์ธ์ฆ์ ๋ฐ๊ธ์ด ์๋ฃ๋ ๊ฒ์ด๋ค.


์ดํ

`/etc/nginx/sites-available`๋ก ์ด๋ํ ํ, ์ ์ ํ ์ด๋ฆ์ ํ์ผ์ ์์ฑํ์ฌ ๋ค์๊ณผ ๊ฐ์ด ์์ฑํ๋ค.

`sudo vi proxy-setting.conf`

```shell
server {
        listen 80 default_server;
        listen [::]:80 default_server;

        server_name i8d208.p.ssafy.io;

        location /{
                proxy_pass http://localhost:3000;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "upgrade";
        }

        location /api {
                proxy_pass http://localhost:8000/api;
        }

}
server {
        listen 443 ssl;
        listen [::]:443 ssl;

        server_name i8d208.p.ssafy.io;

        location /{
                proxy_pass http://localhost:3000;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "upgrade";
        }

        location /api {
                proxy_pass http://localhost:8000/api;
        }

        ssl_certificate /etc/letsencrypt/live/i8d208.p.ssafy.io/fullchain.pem; # managed by Certbot
        ssl_certificate_key /etc/letsencrypt/live/i8d208.p.ssafy.io/privkey.pem; # managed by Certbot
        # include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
        # ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
}
```



&nbsp;


> **โ๏ธ ์ฌ๊ธฐ์ ๋ฌธ์ ์ **
> 
> ๊ธฐ์กด nginx๊ฐ 80๋ฒ port๋ก ์คํ๋๋ค.
> 
> <img width="1198" alt="แแณแแณแแตแซแแฃแบ 2023-02-04 แแฉแแฅแซ 9 50 40" src="https://user-images.githubusercontent.com/72541544/216736266-d317d61e-0bb2-4960-a160-c5c5eef9f465.png">
> **๋๋ 3.36.87.75๋ฅผ ์๋ ฅํ์ ๋, ์ฐ๋ฆฌ mainํ๋ฉด์ด ๋์์ผ๋ฉด ์ข๊ฒ ๋ค!**
> 
> `/etc/nginx/sites-enabled` ๋ก ์ด๋ํ๋ค.
> 
> <img width="1138" alt="แแณแแณแแตแซแแฃแบ 2023-02-04 แแฉแแฅแซ 9 55 52" src="https://user-images.githubusercontent.com/72541544/216736433-933e3388-3163-4de8-9028-dc9a226b85dc.png">
> `default`, `proxy-setting`์ด ์๋๋ฐ (`proxy-setting`์ ์ดํ์ ์คํํ๋ฉด ๋ง๋ค์ด์ง๋ `.conf` ํ์ผ์ด๋ค.)
> 
> `default ํธ์ง๊ธฐ`๋ฅผ ์ด์ด์ `port`๋ฅผ ๋ณ๊ฒฝํด์ฃผ๊ณ  ์ฌ์คํํ๋ฉด ๋๋ค. (์ฌ์คํ์ 2๋ฒ ์ฐธ๊ณ ) - default ํ์ผ์ ํธ์งํ์ง ๋ง๊ณ  ์ญ์ ํด๋ ๋๋ ๊ฒ ๊ฐ๋ค. (80 -> 180)
> 
> <img width="397" alt="แแณแแณแแตแซแแฃแบ 2023-02-04 แแฉแแฅแซ 9 58 41" src="https://user-images.githubusercontent.com/72541544/216736751-999380d0-18b8-4e85-b0e4-762cb17055d7.png">



&nbsp;

**โ๏ธ ln -s ๋ช๋ น์ด ์คํํ๋ค.**

<img width="1134" alt="แแณแแณแแตแซแแฃแบ 2023-02-04 แแฉแแฅแซ 10 05 03" src="https://user-images.githubusercontent.com/72541544/216736945-fe330631-b9d6-4c3c-bbe4-98625ae9b946.png">


```shell
sudo ln -s /etc/nginx/sites-available/proxy-setting /etc/nginx/sites-enabled/proxy-setting
```



&nbsp;



**โ๏ธ ์ฑ๊ณต ์ฌ๋ถ ํ์ธ**


<img width="579" alt="แแณแแณแแตแซแแฃแบ 2023-02-04 แแฉแแฅแซ 10 06 09" src="https://user-images.githubusercontent.com/72541544/216737010-f7e2473e-197d-40a6-96d2-3986c6be53f5.png">


```shell
sudo nginx -t
```

`nginx test`๊ฐ ์ฑ๊ณตํ๋ค๋ ๊ฒ์ ์ ์ ์๋ค.


&nbsp;


**โ๏ธ nginx ์ฌ์์**

```shell
sudo systemctl restart nginx
```



์ด๋ ๊ฒ ์คํํ๋ฉด, http๋ก 3000ํฌํธ ์ ๊ทผ์, 443 ํฌํธ(https)๋ก ๋ฆฌ๋ค์ด๋ ํธ ๋๋ค. ๊ทธ๋ฆฌ๊ณ  ๋ฐฑ์๋ url์ /api/**๋ก ๋ถ๊ธฐ์ฒ๋ฆฌํ  ์ ์๋ค.ย 

- `https://๋๋ฉ์ธ์ฃผ์`ย ๋ก ์ ๊ทผํ๋ฉด ๋ฐฐํฌํ ์น ํ์ด์ง์ ์ ์ํ  ์ ์๊ฒ๋๋ค.
- `http://ip์ฃผ์`๋ก ์ ๊ทผํ๋ฉด ๋ฐฐํฌํ ์น ํ์ด์ง์ ์ ์ํ  ์ ์๋ค.

&nbsp;


&nbsp;


# ๐ 2. conf ํ์ผ ์์ ํ  ๋

ํ์ฌ ์ด์  `proxy-setting`์ ์์ ํ๊ณ  ์ถ์ ๋๊ฐ ์๋ค.

์์ ํ๊ณ  ์ถ์ ๋๋ ๋จผ์ 

**โ๏ธ nginx ์ข๋ฃ ํ, ์ค์ ํด์ผ ํ๋ค.**

`sudo systemctl stop nginx`์ ์๋ ฅํ์ฌ nginx์ ์ข๋ฃํ๋ค.

`sudo letsencrypt certonly --standalone -d www์ ์ธํ ๋๋ฉ์ธ ์ด๋ฆ` ์ ์๋ ฅํ์ฌ ์ค์ ํด์ค๋ค.


<img width="1048" alt="แแณแแณแแตแซแแฃแบ 2023-02-04 แแฉแแฅแซ 10 18 33" src="https://user-images.githubusercontent.com/72541544/216737698-463b4af8-94f4-4ffd-bc5a-954c1fa65360.png">

&nbsp;


**โ๏ธ /etc/nginx/sites-available**

`/etc/nginx/sites-available` ๋ก ์ด๋ํ์ฌ proxy-setting ํธ์ง๊ธฐ๋ฅผ ์ด์ด ์ด์ ๊ฐ์ด ์์ ํ๋ค.



```shell
server {
        listen 80 default_server;
        listen [::]:80 default_server;

        server_name i8d208.p.ssafy.io;

        location /{
                proxy_pass http://localhost:3000;
                proxy_set_header Upgrade $http_upgrade;
                proxy_set_header Connection "upgrade";
        }

        location /api {
                proxy_pass http://localhost:8000/api;
        }

}
```




<img width="520" alt="แแณแแณแแตแซแแฃแบ 2023-02-04 แแฉแแฅแซ 10 12 41" src="https://user-images.githubusercontent.com/72541544/216737363-9f853420-9e27-4621-afdb-1b17aa830e57.png">





&nbsp;

**โ๏ธ sites-enabled์์ ์ด์ ์ ๋ง๋ค์๋ proxy-setting์ ์ญ์ ํ๋ค.**


```shell
sudo rm proxy-setting
```
<img width="1024" alt="แแณแแณแแตแซแแฃแบ 2023-02-04 แแฉแแฅแซ 10 14 53" src="https://user-images.githubusercontent.com/72541544/216737499-c0deb904-5536-472a-be8e-dbeea8b601dd.png">

&nbsp;

**โ๏ธ ln -s ๋ช๋ น์ด ์คํํ๋ค. (๋ค์ sites-enabled์ proxy-setting์ ์ถ๊ฐ)**

<img width="1134" alt="แแณแแณแแตแซแแฃแบ 2023-02-04 แแฉแแฅแซ 10 05 03" src="https://user-images.githubusercontent.com/72541544/216736945-fe330631-b9d6-4c3c-bbe4-98625ae9b946.png">


```shell
sudo ln -s /etc/nginx/sites-available/proxy-setting /etc/nginx/sites-enabled/proxy-setting
```



&nbsp;



**โ๏ธ ์ฑ๊ณต ์ฌ๋ถ ํ์ธ**


<img width="579" alt="แแณแแณแแตแซแแฃแบ 2023-02-04 แแฉแแฅแซ 10 06 09" src="https://user-images.githubusercontent.com/72541544/216737010-f7e2473e-197d-40a6-96d2-3986c6be53f5.png">


```shell
sudo nginx -t
```

`nginx test`๊ฐ ์ฑ๊ณตํ๋ค๋ ๊ฒ์ ์ ์ ์๋ค.


&nbsp;


**โ๏ธ nginx ์ฌ์์**

```shell
sudo systemctl restart nginx
```



์ด๋ ๊ฒ ์คํํ๋ฉด, http๋ก 3000ํฌํธ ์ ๊ทผ์, 443 ํฌํธ(https)๋ก ๋ฆฌ๋ค์ด๋ ํธ ๋๋ค. ๊ทธ๋ฆฌ๊ณ  ๋ฐฑ์๋ url์ /api/**๋ก ๋ถ๊ธฐ์ฒ๋ฆฌํ  ์ ์๋ค.ย 


&nbsp;


**โ๏ธ ๊ฒฐ๊ณผ**

`client http` : `http://3.36.87.75/`
`server http` : `http://3.36.87.75/api/`

<img width="442" alt="แแณแแณแแตแซแแฃแบ 2023-02-04 แแฉแแฅแซ 10 28 01" src="https://user-images.githubusercontent.com/72541544/216738778-0a0d215f-6a0c-4fe3-8f8c-857ca789a570.png">



<img width="663" alt="แแณแแณแแตแซแแฃแบ 2023-02-04 แแฉแแฅแซ 10 27 57" src="https://user-images.githubusercontent.com/72541544/216738764-e2e7e4c5-9fc4-4d35-8c30-ec62ca5e1b86.png">


&nbsp;


`client https` : `https://i8d208.p.ssafy.io/`
`server https` : `https://i8d208.p.ssafy.io/api/`

<img width="567" alt="แแณแแณแแตแซแแฃแบ 2023-02-04 แแฉแแฅแซ 10 28 25" src="https://user-images.githubusercontent.com/72541544/216738790-87690f12-f34e-47e2-956f-e26ed076c72e.png">



<img width="477" alt="แแณแแณแแตแซแแฃแบ 2023-02-04 แแฉแแฅแซ 10 28 12" src="https://user-images.githubusercontent.com/72541544/216738785-6fb39d01-a5c4-45f8-94f6-09260c963044.png">



&nbsp;

&nbsp;

