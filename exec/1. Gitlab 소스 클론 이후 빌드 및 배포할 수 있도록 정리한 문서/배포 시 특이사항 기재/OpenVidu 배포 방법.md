

# ๐ 1. OpenVidu on-premise ๋ฐฐํฌ


```shell
sudo su
```

- openvidu๋ฅผ ๋ฐฐํฌํ๊ธฐ : root ๊ถํ์ ์ป์ด์ผ ํ๋ค.

&nbsp;


```shell
cd /opt
```


- openvidu๋ฅผ ์ค์นํ๊ธฐ ์ํด ๊ถ์ฅ๋๋ ๊ฒฝ๋ก์ธ `/opt`๋ก ์ด๋


&nbsp;

```shell
curl <https://s3-eu-west-1.amazonaws.com/aws.openvidu.io/install_openvidu_latest.sh> | bash
```

- openvidu ์ค์น

&nbsp;


```shell
cd openvidu
```

- ์ค์น ํ openvidu๊ฐ ์ค์น๋ ๊ฒฝ๋ก๋ก ์ด๋



&nbsp;


```shell
$ nano .env

# OpenVidu configuration
# ----------------------
# ๋๋ฉ์ธ ๋๋ ํผ๋ธ๋ฆญIP ์ฃผ์
DOMAIN_OR_PUBLIC_IP=i5a608.p.ssafy.io

# ์คํ๋น๋ ์๋ฒ์ ํต์ ์ ์ํ ์ํฌ๋ฆฟ
OPENVIDU_SECRET=HOMEDONG

# Certificate type
CERTIFICATE_TYPE=letsencrypt

# ์ธ์ฆ์ ํ์์ด letsencrypt์ผ ๊ฒฝ์ฐ ์ด๋ฉ์ผ ์ค์ 
LETSENCRYPT_EMAIL=user@example.com

# HTTP port
HTTP_PORT=8442

# HTTPS port(ํด๋น ํฌํธ๋ฅผ ํตํด ์คํ๋น๋ ์๋ฒ์ ์ฐ๊ฒฐ)
HTTPS_PORT=8443
```


- ๋๋ฉ์ธ ๋๋ public IP์ openvidu์ ํต์ ์ ์ํ ํ๊ฒฝ์ค์ 


&nbsp;


```shell
$ ./openvidu start

Creating openvidu-docker-compose_coturn_1          ... done
Creating openvidu-docker-compose_app_1             ... done
Creating openvidu-docker-compose_kms_1             ... done
Creating openvidu-docker-compose_nginx_1           ... done
Creating openvidu-docker-compose_redis_1           ... done
Creating openvidu-docker-compose_openvidu-server_1 ... done

----------------------------------------------------

   OpenVidu Platform is ready!
   ---------------------------

   * OpenVidu Server: https://DOMAIN_OR_PUBLIC_IP/

   * OpenVidu Dashboard: https://DOMAIN_OR_PUBLIC_IP/dashboard/

----------------------------------------------------
```


- ์ค์  ํ ์คํ๋น๋ ์๋ฒ ์คํ(`ctrl + c`๋ฅผ ๋๋ฅด๋ฉด ๋ฐฑ๊ทธ๋ผ์ด๋๋ก ์คํ๋จ)


&nbsp;


&nbsp;


# ๐ 2. openvidu ๊ด๋ จ ์ฉ์ด ์ ๋ฆฌ



> **๐ก ์ฐธ๊ณ **
> 
> `openvidu` : Docker Compose๋ก ๊ด๋ฆฌ๋๋ ์ผ๋ จ์ Docker ์ปจํ์ด๋๋ก ๋ฐฐํฌ๋๋ค.
> - ์ค์น๋๋ ์๋น์ค(๊ดํธ ์์ openvidu ๋ด docker-compose๋ก ์ธํด ์คํ๋๋ docker container์ name์ด๋ค.)




&nbsp;

**โ๏ธ ์ฉ์ด**

- `OpenVidu Server(openvidu-server)` : OpenVidu ํ๋ซํผ์ ๋๋. ์๊ทธ๋๋ง์ ๋ด๋นํ๋ค. 
- `Kurento Media Server(kms)` : OpenVidu ํ๋ซํผ์ ํต์ฌ. ๋ฏธ๋์ด ์๋ฒ๋ฅผ ๋ด๋นํ๋ค. 
- `Coturn(coturn)` : ํน์  ํน์ ๋คํธ์ํฌ์์ ๋ธ๋ผ์ฐ์ ๋จ ๊ฐ ๋ฏธ๋์ด ํต์ ์ ํ์ฉํ๋๋ฐ ์ฌ์ฉ๋๋ ์๋ฒ. 
- `Nginx(nginx)` : SSL ์ธ์ฆ์๋ฅผ ๊ตฌ์ฑํ๊ณ  Openvidu ์๋ฒ์ ์์ฉ ํ๋ก๊ทธ๋จ์ด ๋ชจ๋ ํ์ค https ํฌํธ(443)์์ ์ ๊ณต๋๋๋ก ํ๋ ๋ฐ ์ฌ์ฉ๋๋ ์ญ๋ฐฉํฅ ํ๋ก์๋ฅผ ๋ด๋นํ๋ค. 
- `OpenVidu-Call`: OpenVidu์์ ๊ธฐ๋ณธ์ผ๋ก ์ ๊ณตํ๋ ์ดํ๋ฆฌ์ผ์ด์ ํ๋ก๊ทธ๋จ. ์ฐ๋ฆฌ๋ ์ฐ๋ฆฌ ์ดํ๋ฆฌ์ผ์ด์์ ์ ์ฉํ์ฌ ์ฌ์ฉํ  ๊ฒ์ด๋ฏ๋ก ๋นํ์ฑํ ์์ผฐ๋ค.



&nbsp;

&nbsp;

