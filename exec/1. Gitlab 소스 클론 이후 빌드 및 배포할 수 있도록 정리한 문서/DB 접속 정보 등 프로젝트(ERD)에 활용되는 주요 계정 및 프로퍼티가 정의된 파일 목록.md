
  

# ๐ 1. mysql

mysql ๊ฐ์๊ฒฝ์ฐ docker image๋ฅผ ์ด์ฉํ  ๊ฒ์ด๋ค.

์ฐธ๊ณ  ์๋ฃ : [์  ํจ์ค์ ๋์ปค๋ฅผ ์ด์ฉํ CICD ๋ฐฐํฌ๋ฐฉ๋ฒ](https://dev-taerin.tistory.com/35)



```

# mysql ์ด๋ฏธ์ง ๋ถ๋ฌ์ค๊ธฐ

sudo docker pull mysql

# ๋์ปค ์ด๋ฏธ์ง ํ์ธ

sudo docker images

# ๋์ปค ์ด๋ฆ์ --name ๋ค์ ๋ฃ๊ณ , password๋ root ํจ์ค์๋(์ฌ์ฉ์ ์ง์ )

sudo docker run -d -p 3305:3306 -e MYSQL_ROOT_PASSWORD=ssafy --restart=unless-stopped -v /home/ubuntu/db:/var/lib/mysql --name D208_mysql mysql

# ๋์ปค ์ปจํ์ด๋ bash ์ ์

sudo docker exec -it d208_mysql bash

# mysql ์ ์

mysql -u root -p

# ํจ์ค์๋ ์๋ ฅ

ssafy

```


&nbsp;

`username` : root  
`password` : ssafy
  

![Untitled](https://user-images.githubusercontent.com/72541544/219372036-37eab172-df58-4ab5-a560-8be1404c2b21.png)


&nbsp;

`springboot - application.yml`

  
```yml
server:
  port: 8080
  servlet:
    context-path: /
    encoding:
      charset: UTF-8
      enabled: true
      force: true
#  address: localhost
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://i8d208.p.ssafy.io:3305/chuno?useSSL=false&autoReconnect=true&useUnicode=true&characterEncoding=utf-8&serverTimezone=UTC
    hikari:
      username: root
      password: ssafy
  jpa:
    database: mysql
    hibernate:
      ddl-auto: create
#    database-platform: org.hibernate.dialect.MySQL5InnoDBDialect
    properties:
      hibernate:
        show_sql: true
        format_sql: true
  servlet:
    multipart:
      location: C:\res_file\chuno
logging:
  level:
    root: info
    org.hibernate.type: trace
```


&nbsp;


**โ๏ธ sql default**

```sql
insert into users
(reg_dt, catch_count, chaser_play_count, chaser_win_count, email, exp, is_deleted, is_manager, level, money, nickname, paper_count, path, save_name, runner_play_count, runner_win_count, phone)
values
(now(), 0, 11, 7, "ljc9393@nate.com", 0, 0, 0, 1, 0, "ํฐ๊ฐ๋", 0, "", "", 30, 15, "01051411025"),
(now(), 0, 11, 7, "opi6@hanmail.net", 0, 0, 0, 1, 0, "์ธ์๋ํฐ์", 0, "", "", 30, 15, "01026896940"),
(now(), 0, 11, 7, "lce511@naver.com", 0, 0, 0, 1, 85900, "์ฑ์์งฑ๋", 0, "", "", 30, 15, "01084054759"),
(now(), 0, 11, 7, "souk0712@naver.com", 0, 0, 0, 1, 80000, "๋ชจ์นด", 0, "", "", 30, 15, "01082860799"),
(now(), 0, 11, 7, "asdf@naver.com", 0, 0, 0, 1, 0, "์๋ฌด", 0, "", "", 13, 15, "01515498451"),
(now(), 0, 11, 7, "qwer@naver.com", 0, 0, 0, 1, 524, "์ด๋ฆ", 0, "", "", 51, 15, "01059519858"),
(now(), 0, 11, 7, "zxcv@naver.com", 0, 0, 0, 1, 5000, "์ง๊ธฐ", 0, "", "", 30, 15, "01098751351"),
(now(), 0, 11, 7, "grg@naver.com", 0, 0, 0, 1, 800, "๊ท์ฐฎ์์ฃฝ๊ฒ ์", 0, "", "", 30, 15, "01849878512"),
(now(), 0, 11, 7, "tnth@naver.com", 0, 0, 0, 1, 7000, "๋๋ด๋ญํ์ง", 0, "", "", 30, 15, "01012168849"),
(now(), 0, 11, 7, "tnth2@naver.com", 0, 0, 0, 1, 7000, "๋๋ด๋ญํ์ง2", 0, "", "", 30, 15, "01012168849"),
(now(), 0, 11, 7, "tnth3@naver.com", 0, 0, 0, 1, 7000, "๋๋ด๋ญํ์ง3", 0, "", "", 30, 15, "01012168849"),
(now(), 0, 11, 7, "tnth4@naver.com", 0, 0, 0, 1, 7000, "๋๋ด๋ญํ์ง4", 0, "", "", 30, 15, "01012168849"),
(now(), 0, 11, 7, "tnth5@naver.com", 0, 0, 0, 1, 7000, "๋๋ด๋ญํ์ง5", 0, "", "", 30, 15, "01012168849"),
(now(), 0, 11, 7, "tnth6@naver.com", 0, 0, 0, 1, 7000, "๋๋ด๋ญํ์ง6", 0, "", "", 30, 15, "01012168849"),
(now(), 0, 11, 7, "tnth7@naver.com", 0, 0, 0, 1, 7000, "๋๋ด๋ญํ์ง7", 0, "", "", 30, 15, "01012168849"),
(now(), 0, 11, 7, "tnth8@naver.com", 0, 0, 0, 1, 7000, "๋๋ด๋ญํ์ง8", 0, "", "", 30, 15, "01012168849");

INSERT INTO items
(description, img_path, name, price, for_runner)
VALUES
    ("์์ ์ ์์น๋ฅผ ๋๋ฌ๋ด์ง ์๊ณ  ๊ฐ์ฅ ๊ฐ๊น์ด ์ถ๋ธ๊พผ์ ์์น๋ฅผ ํ์ธํ  ์ ์๋ค.", "item/item1.png", "์ฒ๋ฆฌ์", 1500, 1),
    ("์ถ๋ธ๊พผ์ด ์์ ์ ์ก์ ์ ์๋ ๋ฒ์๋ฅผ ์ถ์ํ๋ค.", "item/item2.png", "์์ฅ", 2000, 1),
    ("์ง์ง ๋ธ๋น๋ฌธ์์ ์์น๋ฅผ ํ์ธํ  ์ ์๋ค.", "item/item3.png", "ํ์คํ\n์ ๋ณดํต", 1000, 1),
    ("๋จน๋ฌผ์ ๋ฟ๋ ค ๋ด ํ๋ฉด์ ๊ฐ๋ฆด ์ ์๋ค.", "item/item4.png", "๋จน๋ฌผํ", 1300, 1),
    ("30์ด๊ฐ ๋ธ๋น์ ์์น๋ฅผ ์ง๋์ ํ์ํ  ์ ์๋ค.", "item/item5.png", "์กฐ๋ชํ", 1500, 0),
    ("์์ ์ด ๋ธ๋น๋ฅผ ์ก์ ์ ์๋ ๋ฒ์๋ฅผ ํ๋ํ  ์ ์๋ค.", "item/item6.png", "๊ธด\n์ค๋์ค", 2000, 0),
    ("๋ธ๋น ๋ฌธ์์ ์์น๋ฅผ ์ํํ  ์ ์๋ค.", "item/item7.png", "๊ฑฐ์ง\n์ ๋ณดํต", 1000, 0),
    ("์ฐ๊ธฐ๋ฅผ ํผ์ ๋ด ํ๋ฉด์ ๊ฐ๋ฆด ์ ์๋ค.", "item/item8.png", "์ฐ๋งํ", 1300, 0);


/*- ์ฒ๋ฆฌ์ : ์์ ์ ์์น๋ฅผ ๋๋ฌ๋ด์ง ์๊ณ  ๊ฐ์ฅ ๊ฐ๊น์ด ์ถ๋ธ๊พผ์ ์์น๋ฅผ ํ์ธํ  ์ ์๋ค.
- ์์ฅ : ์ถ๋ธ๊พผ์ด ์์ ์ ์ก์ ์ ์๋ ๋ฒ์๋ฅผ ์ถ์ํ๋ค.
- ํ์คํ ์ ๋ณดํต : ์ง์ง ๋ธ๋น๋ฌธ์์ ์์น๋ฅผ ํ์ธํ  ์ ์๋ค.
- ๋จน๋ฌผํ : ๋จน๋ฌผ์ ๋ฟ๋ ค ๋ด ํ๋ฉด์ ๊ฐ๋ฆด ์ ์๋ค.
2. ์ถ๋ธ๊พผ์ฉ
    - ์กฐ๋ชํ : n์ด๊ฐ ๋ธ๋น์ ์์น๋ฅผ ์ง๋์ ํ์ํ  ์ ์๋ค.
        - ์ ์ฒด ๋ธ๋น ์์น ์ ๊น ํ์
    - ๊ธด ์ค๋์ค : ์์ ์ด ๋ธ๋น๋ฅผ ์ก์ ์ ์๋ ๋ฒ์๋ฅผ ํ๋ํ  ์ ์๋ค.
    - ๊ฑฐ์ง ์ ๋ณดํต : ๋ธ๋น ๋ฌธ์์ ์์น๋ฅผ ์ํํ  ์ ์๋ค.
    - ~~ํ์์๋น : ๋ธ๋น ํ๋ฉด์ ๊ฐ์ง ์ถ๋ธ๊พผ ์์น ๋์ฐ๊ธฐ~~
    - ์ฐ๋งํ: ์ฐ๊ธฐ๋ฅผ ํผ์ ๋ด ํ๋ฉด์ ๊ฐ๋ฆด ์ ์๋ค.*/

```


&nbsp;

&nbsp;
