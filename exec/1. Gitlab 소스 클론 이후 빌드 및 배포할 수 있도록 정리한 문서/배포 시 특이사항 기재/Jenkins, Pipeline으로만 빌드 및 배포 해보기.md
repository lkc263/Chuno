
> **๐ ์์ํ๊ธฐ์ **
> docker ์์ด Jenkins, Pipeline์ผ๋ก๋ง ๋น๋ ๋ฐ ๋ฐฐํฌํด๋ณด๊ธฐ


&nbsp;



> **๐ ์  ํจ์ค ํ์ดํ๋ผ์ธ์ ํ์ฉํ ๋ฐฐํฌ ์๋ํ**
> - ํ์ดํ๋ผ์ธ์ ํ์ฉํ์ฌ ๋ฐฐํฌ ์๋ํ

&nbsp;


# ๐ 1. Jenkins ์ด๋ค ๊ตฌ์กฐ๋ก ๋์ํ ๊น?

**โ๏ธ ํ์ฌ ์ํฉ**

ํ๋ก์ ํธ์ ๊ธฐ๋ฅ์ ์ถ๊ฐํด์ base branch์ merge ๋์๋ค. ์ด์  ์ค์  ์๋ฒ์ ๋ฐฐํฌ๋ฅผ ํด์ผํ๊ฒ ๋ค.


&nbsp;

**โ๏ธ ํํ๋ก์ ํธ์์ ๋ง์ด ์ฌ์ฉํ๋ work flow - ํ์ฌ ๋งค๋ฒ ์คํ๋์ด์ผ ํ๋ค.**

<img width="786" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฅแซ 12 54 46" src="https://user-images.githubusercontent.com/72541544/212362539-477996c8-6565-485d-a852-b20a1f261cf4.png">
(1) ๊ฐ ๊ฐ๋ฐ์๊ฐ ๊ธฐ๋ฅ์ ๊ตฌํํ ํ PR

(2) EC2 ์๋ฒ๋ก ์ ์

(3) github์ merge๋ ์ฝ๋๋ฅผ git pull

(4) gradle์ ์ด์ฉํด bootJar

(5) jar ํ์ผ์ java -jar ๋ช๋ น์ด๋ฅผ ํตํด 80port์ ์คํํ๋ค.

=> 5๊ฐ์ง๋ฅผ ๋งค๋ฒ ์คํํด์ผ ํ๋ค. ๊ท์ฐฎ์ง ์์๊ฐ? `Jenkins`๋ฅผ ์ด์ฉํ๋ฉด ํด๊ฒฐํ  ์ ์๋ค.

&nbsp;


> **๐ก ์ฐธ๊ณ **
> - ์๋ฒ ๋ฐฐํฌ๋ ๋งค๋ฒ ๊ธฐ๋ฅ์ด ์ถ๊ฐ๋  ๋๋ง๋ค ์ํ๋์ด์ผ ํ๋ค.
> - ํ์ฌ flow๋ ์๋ก์ด ๊ธฐ๋ฅ๋ง๋ค ๋ฐ๋๋ ๊ฒ์ด ์๋๊ธฐ ๋๋ฌธ์, ์๋ํ ํ  ์ ์๋ ๋์์ด๋ค.

&nbsp;

**โ๏ธ Continuous Distribution - ์ง์์  ๋ฐฐํฌ**

`flow`๋ฅผ ์๋ํํ์ฌ ์ต์  ์ํ์ ์ฝ๋๊ฐ ์๋์ผ๋ก ๋ฐฐํฌ๋๋ ๊ฒ


&nbsp;


**โ๏ธ Jenkins๊ฐ ํด์ฃผ๋ ๊ฒ์?**

**`Jenkins`๊ฐ ๊ธฐ๋ฅ ๊ตฌํ์ ํด์ฃผ์ง๋ ์๋๋ค.**

Jenkins๊ฐ ํด์ฃผ๋ ๋ถ๋ถ์?

(1) github์ผ๋ก๋ถํฐ merge ๋์๋ค๋ ์ฐ๋ฝ์ ๋ฐ์์

(2) ์ฝ๋๋ฅผ git cloneํ๊ณ 

(3) gradle๋ก ํ๋ก์ ํธ๋ฅผ build ํ์ฌ

(4) buildํ ๋ชฉ์ ํ์ผ์ ์ดํ๋ฆฌ์ผ์ด์์ด ์คํ๋์ด์ผ ํ  ์๋ฒ๋ก ์ ๋ฌํ๊ณ , ์ดํ๋ฆฌ์ผ์ด์์ ๊ตฌ๋ํ๊ธฐ ์ํ ๋ช๋ น์ด๋ฅผ ์คํํ๋ค.


&nbsp;

**โ๏ธ Jenkins์ ์ค์ ์ด ๋ฐฐํฌ๋ฅผ ํ ๋ ์ด๋ค ๋ถ๋ถ์ ์๋ํ ํด์ฃผ๋ ๊ฑธ๊น?**

<img width="791" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฅแซ 8 31 46" src="https://user-images.githubusercontent.com/72541544/212437241-8a57d8b3-ad7b-43f3-9a36-2c71211c0166.png">


&nbsp;


> **๐ก ์ฐธ๊ณ **
> ์ดํ๋ฆฌ์ผ์ด์ ์๋ฒ์์ Jenkins๋ฅผ ๊ตฌ๋ํ  ๊ฒฝ์ฐ, ๋น๋๊ฐ ์งํ๋  ๋๋ง๋ค CPU ์์์ด ๋ชจ์๋ผ์ ์๋ฒ๊ฐ ๋ค์ด๋๋ ์ผ์ด ์๋ค.
> 
> ์ด๋ก ์ธํด ๋ณ๋ EC2๋ก ๋ถ๋ฆฌํ๋ ๊ฒ์ด ์ข๋ค.
> 
> ๋ง์ฝ, **์๋ฒ ์์์ด ๋ชจ์๋ผ๊ฑฐ๋ ์ฌ๋ฌ ๊ฐ์ WAS๋ฅผ ๋์ธ ์ผ์ด ์๊ธด๋ค๋ฉด, ๋ณ๋ ํ๊ฒฝ์ผ๋ก ๋ถ๋ฆฌํ๋ ๊ฒ์ ์ถ์ฒํ๋ค.**



&nbsp;


**โ๏ธ Ubuntu ์ด๊ธฐ์ค์ (20.04)**

```java
sudo apt-get update
sudo apt-get install apache2
sudo apt-get install openjdk-11-jdk
```

&nbsp;

[Jenkins ์ค์น ์ฐธ๊ณ ](https://velog.io/@chang626/Jenkins)


- sudo cat ~/initialAdminPassword :  ์ฒซ ์ค์น์ ํ์ํ password


&nbsp;

> **๐ก ์ฐธ๊ณ **
> `sudo apt-get install openjdk-11-jdk` : java 11 jdk ์ค์น

&nbsp;


# ๐ 2. credentials ์ธํ

์ปดํจํฐ๊ฐ ๋ ๋์ ์ git clone์ ํ๊ฒ ํ๋ ค๋ฉด ํด๋น ๋ ํฌ์งํ ๋ฆฌ์ ๋ํ ๊ถํ์ด ํ์ํ๋ค!

&nbsp;


> **๐ก ์ฐธ๊ณ **
> - ๊ณต๊ฐ ๋ ํฌ์งํ ๋ฆฌ์ ์๋ ์์ค์ฝ๋๋ฅผ clone ํ๋ ๋ชฉ์ ์ด๋ผ๋ฉด ๊ถํ์ด ํ์์๊ธฐ ๋๋ฌธ์ ๋ฐ๋ก credentials๋ฅผ ์ค์ ํ์ง ์์๋ ๋๋ค.
> - `PipeLine` ์์์ push ๋๋ ์๋ธ๋ชจ๋ ๋ฑ ๊ถํ์ด ํ์ํ ์ผ์ด ์๋ค๋ฉด `credentials`์ด ํ์ํ๋ค.


&nbsp;


### ๐ A. access token ๋ฐ๊ธ ๋ฐ test

<img width="719" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฅแซ 11 00 02" src="https://user-images.githubusercontent.com/72541544/212445728-bba0ae3b-0910-4807-9cd1-559164e9f3a7.png">

- ์์คํ ์ค์ 


&nbsp;

**โ๏ธ github repository ์ฐ๊ฒฐ**

<img width="1437" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฅแซ 11 02 04" src="https://user-images.githubusercontent.com/72541544/212445730-1f471176-4975-4afa-b30d-2c23933b348d.png">
- github ํญ์ผ๋ก ์ด๋, add  ๋๋ฅธ๋ค.

<img width="1304" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฅแซ 11 10 47" src="https://user-images.githubusercontent.com/72541544/212446083-dc060a90-89a2-405a-b42b-fc8873a163be.png">
- Secret text ์ ํ, Secret(github token), ID๋ ์๋ฌด๊ฑฐ๋

&nbsp;

<img width="1222" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฅแซ 11 10 53" src="https://user-images.githubusercontent.com/72541544/212446085-98fb5366-a27d-46b6-bd49-ea68636f1b08.png">

- test Connection์ด ๋ฐ์ํ  ๊ฒฝ์ฐ ์ฑ๊ณต

&nbsp;


**โ๏ธ credentials์ด ํ์ํ๋ค (๋ฏธ๋ฆฌ ์์ฑํ์)**

- ์์คํ ์ค์ ์ github๊ณผ ์ฐ๊ด๋ ๊ฒ์ credentials์ Secret text๋ก ๋ฑ๋กํ credentials๋ง ์ธ์ํ๋ค.
  
- ์ง๊ธ์ Username with password ๋ก ์์ฑํ credentials์ด ํ์ํ๋ค.



&nbsp;


**โ๏ธ ๋ฑ๋ก ํน์ ํ์ธ ๊ฐ๋ฅํ๋ค.**

`credentials`๋ ์ถํ `manage credentials`์์ ๋ฑ๋ก ํน์ ํ์ธ์ด ๊ฐ๋ฅํ๋ค.

<img width="724" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฅแซ 11 17 45" src="https://user-images.githubusercontent.com/72541544/212446325-6fe8278e-6c1a-434c-bca2-21630e75a7e6.png">

<img width="1225" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฅแซ 11 20 38" src="https://user-images.githubusercontent.com/72541544/212446395-9160da62-39fb-48f8-926c-0c1fa9dcbd53.png">




&nbsp;


&nbsp;


# ๐ 2. ํ์ดํ๋ผ์ธ ์์ฑํ๊ธฐ

> **๐ก ์ฐธ๊ณ **
> - ๊ฐ๋จํ Job์ ์ํด์  freestyle๋ ์ข์ ์ ํ (๋น๊ต์  ์ธํ์ด ๋จ์)
>   
> - ๋ณต์กํ ์ข๋ฅ์ Job๊ฐ์ ์ฐ๊ณ๋ ์์ธํ ์ธํ, UI (๊ฐ job๋ณ๋ก ์ด๋ป๊ฒ ์งํ๋๊ณ  ์๋์ง ๋ณด์ฌ์ค๋ค.)๋ฅผ ์ํ๋ค๋ฉด ํ์ดํ๋ผ์ธ์ ์ ํ


<img width="1432" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฅแซ 11 25 04" src="https://user-images.githubusercontent.com/72541544/212446578-fbf31d81-edfa-4735-bc3b-a64e8736a84a.png">



&nbsp;


**โ๏ธ pipeline script**

pipeline script์ Groobee ๋๋ Jenkins์์ ์ ์ํ pipeline syntax๋ฅผ ํตํด item์์ ์ํํ  Job์ ์ ์ธํ๊ณ , ์์๋ฅผ ์กฐ์ ํ๊ณ , ํ๊ฒฝ์ ์ค์ ํ๋ ์ญํ ์ ํ๋ค.

[PipeLine ๊ณต์๋ฌธ์](https://www.jenkins.io/doc/book/pipeline/)

&nbsp;


**โ๏ธ pipeline syntax**

ํ๋ฌ๊ทธ์ธ ๋ณ๋ก syntax๋ฅผ ๋ง๋ค์ด์ค๋ค.


<img width="1408" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฎ 2 21 05" src="https://user-images.githubusercontent.com/72541544/212457276-5503caaf-e9f1-478b-9071-72e1c74aa8fe.png">


(1) `pipe line`์ ์ด ํ์ดํ๋ผ์ธ ์์ฒด๋ฅผ ์๋ฏธํ๋ค.

(2) `agent`๋ ์ด ํ์ดํ๋ผ์ธ ์คํฌ๋ฆฝํธ๋ฅผ ์คํํ  `executor`๋ฅผ ์ง์ ํ๋ค. `any`๋ก ๋ ์ ์ด๋ค `executor`๋ ์คํํ  ์ ์๋ค๋ ์๋ฏธ๊ฐ ๋๋ค.  

(3) `stages`๋ ์คํํ  Job๋ค์ ์งํฉ์ด๋ค.  

(4) `stage`๋ ๊ฐ๊ฐ์ Job์ ์๋ฏธํ๋ค. Job ๋ด๋ถ์ ๋จ๊ณ๋ฅผ ์๋ฏธํ๋ steps๋ฅผ ํฌํจํด์ผํ๋ค. 

(5) `steps`์์  ์ค์ ๋ก ์คํํ  ์์ด๋ `syntax`๋ฅผ ์๋ ฅํด์ฃผ๋ฉด ๋๋ค.


&nbsp;

&nbsp;

# ๐ 3. Git Clone ํ๊ธฐ

`git clone` ํ๊ธฐ ์ํด์๋ `syntax`๋ฅผ ๋ง๋ค์ด์ผ ํ๋ค. (pipeline syntax๋ฅผ ํด๋ฆญ)

`pipeline syntax -> snippet generate` click

<img width="1413" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฎ 2 28 56" src="https://user-images.githubusercontent.com/72541544/212457494-6ca99c36-4136-49af-88e0-4b9f38591f52.png">
- git check

&nbsp;


<img width="1417" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฎ 2 29 12" src="https://user-images.githubusercontent.com/72541544/212457501-e0197c08-8038-4107-921e-5e9fc48eb42b.png">

<img width="1435" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฎ 2 33 17" src="https://user-images.githubusercontent.com/72541544/212457588-d4329965-234a-406b-b01d-facdc4aae95d.png">



- `repository url`์ ์ ์ด์ฃผ๊ณ , `branch`๋ฅผ ์ ํํ๊ณ , `credentials`๋ฅผ ๋ฃ์ด์ค๋ค. 
  
- ์๊น ์ถ๊ฐํ์ง ์์๋ค๋ฉด ์ง๊ธ ์ถ๊ฐํด์ค๋ค. 
  
- **๊ณต์ฉ ๋ ํฌ์งํ ๋ฆฌ๋ฅผ cloneํ๋ ์์ฅ์ด๋ผ๋ฉด ๋น์๋์๋ ๋๋ค.**

&nbsp;



<img width="1403" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฎ 2 34 19" src="https://user-images.githubusercontent.com/72541544/212457613-fa4e17eb-0f8c-4781-aee2-3888721ee3ea.png">



- generate๋ฅผ ๋๋ฅด๋ฉด ์ค๋ํซ์ด ์์ฑ๋๋ค. ํด๋น ๋ด์ฉ์ ๋ณต์ฌํ์!




&nbsp;


<img width="1414" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฎ 2 36 54" src="https://user-images.githubusercontent.com/72541544/212457668-ad632bfa-128b-4709-a79b-f54f078ddea9.png">
- `stage` ์ด๋ฆ์ ์ํ๋ ์ด๋ฆ์ผ๋ก ๋ณ๊ฒฝํ๊ณ , `steps`์๋ ์์์ ์์ฑํ `snippet`์ ๋ถ์ฌ์ฃผ๋ฉด ๋๋ค.
  
- **์ฝ์ด๋ณด๋ฉด, git ํน์  ๋ธ๋์น์์ ํน์  `credentials`๋ก url์ ๋ ํฌ์งํ ๋ฆฌ์์ ์์ค๋ฅผ ๊ฐ์ ธ์ค๋ `snippet`์ด๋ค.**


=> ์ด์  ์ ์ฅ์ ๋๋ฅด๋ฉด, **`github`์ `clone` ํ๋ job์ ๊ฐ์ง ํ์ดํ๋ผ์ธ์ ์์ฑํ ๊ฒ์ด๋ค.**

&nbsp;

> **๐ก ์ฐธ๊ณ **
> - **ํ ๋ฒ์ ์ ์ฒด job์ ์์ฑํ๋ฉด trouble shooting์ด ํ๋ค์ด์ง๋ฏ๋ก ๊ฐ ๋จ๊ณ๋ณ๋ก ํ์คํธ ํ์.** 
> - ๋์ฌ๋ณด๋์์ ์์ฑํ ์์ดํ์ ํด๋ฆญํ์ฌ ๋ค์ด๊ฐ์๋ค.

&nbsp;

**โ๏ธ ์ด์ ๊น์ง ์์ํ ๋ด์ฉ ํ์คํธ**

<img width="1431" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฎ 2 45 42" src="https://user-images.githubusercontent.com/72541544/212457898-d7d28f38-d63a-40b7-aece-7cccbeb90062.png">
- ์๋์ ์ผ๋ก build ํ ์, job์ ์ ๋ฐํ๋ค.
  
- ์คํ๋์ด Build History์ ์ ๋ค์ด๊ฐ ๊ฒ์ ๋ณผ ์ ์๋ค.

&nbsp;


**โ๏ธ ๋น๋ ๊ณผ์ ์์ ์ถ๋ ฅ๋๋ ์ฝ์๋ฌธ์ `console output` ํญ์์ ํ์ธํ  ์ ์๋ค.**

<img width="1383" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฎ 2 49 59" src="https://user-images.githubusercontent.com/72541544/212458016-29d3b3b1-c249-43c5-b895-6b9440b70295.png">
<img width="1091" alt="แแณแแณแแตแซแแฃแบ 2023-01-14 แแฉแแฎ 2 50 06" src="https://user-images.githubusercontent.com/72541544/212458023-1511d5da-860a-4be0-b09b-4df0719d2dcf.png">

- `pipeline`  job์ ์งํ ๊ฒฝ๊ณผ ๋ฐ `github clone`์ ์งํํ๋ฉฐ ์๋ ฅ๋ ๋ช๋ น์ด์ ์ถ๋ ฅ๋ฌธ๋ค์ ํ์ธํ  ์ ์๋ค.


&nbsp;

&nbsp;


# ๐ 4. Build 

> **๐ฃ ์์ํ๊ธฐ์ **
> 
> - ๋น๋๋(Build) cloneํด ์จ ์์ค์ ํฌํจ๋์ด ์๋ gradle wrapper๋ฅผ ํ์ฉํ๋ค!
>   
> - ํ๋ก์ ํธ์์ .gradlew ์์น๋ฅผ ์ฐพ์์ผ ํ๋ค.
>   
> - dir ์ค๋ํซ : cd
>   
> - `sh ''' ${์ ๋ช๋ น์ด} '''` : pipeline syntax์์ ์ ๋ช๋ น์ด๋ฅผ ์คํํ๋๋ก ์ค์ ํ๋ ๋ถ๋ถ
>   
> - ํ์ฌ ๋น๋๋ฅผ ์ํด ์คํํด์ผํ  ํ์คํธ : `clean`, `bootJar`


&nbsp;


<img width="1728" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฅแซ 12 09 24" src="https://user-images.githubusercontent.com/72541544/212478779-56d5df4f-7a06-4819-b019-41d50beb233e.png">


```pipeline
pipeline {
    agent any

    stages {
        stage('github clone') {
            steps {
                git branch: 'main', credentialsId: 'repo-and-hook-access-token-credentials', url: 'https://github.com/ToDoStudy/study_jenkins'
            }
        }
        
        stage('build'){
            steps {
                dir('jenkins') {
                    sh '''
                        echo 'start bootJar'
                        ./gradlew clean bootJar
                    '''
                }
            }
        }
    }
}

```


&nbsp;

**โ๏ธ ์ค๋ํซ(snippet)**
์ค๋ํซ(snippet) :ย **์ฌ์ฌ์ฉ ๊ฐ๋ฅํ ์์ค ์ฝ๋, ๊ธฐ๊ณ์ด, ํ์คํธ์ ์์ ๋ถ๋ถ**์ ์ผ์ปซ๋ ํ๋ก๊ทธ๋๋ฐ ์ฉ์ด

- dir : cd
  
- `stages` : ์คํํ  Job๋ค์ ์งํฉ
  
- `stage` : ๊ฐ๊ฐ์ Job์ ์๋ฏธ

&nbsp;


**โ๏ธ build ๊ฒฐ๊ณผ(์คํจ)**

<img width="1707" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฅแซ 12 03 47" src="https://user-images.githubusercontent.com/72541544/212478792-e6ef6cba-525d-42d5-9ea1-cd324e1b6007.png">

<img width="781" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฅแซ 12 00 24" src="https://user-images.githubusercontent.com/72541544/212478790-743ea451-0d5e-4197-8bb4-cee1acfcf010.png">
- ํ์ฌ ์๋ธ ๋ชจ๋์ initํ๊ณ  updateํ์ง ์๋๋ค!


ํ์ฌ ์คํจํ ๊ฒฐ๊ณผ๋ฅผ ์ป๊ฒ ๋์๋ค. ์ด์ ๋?
์ฝ๋๋ฅผ ๋น๋ํ  ๋ ์๋ธ๋ชจ๋์ด ํ์ํ๋ฐ, ํด๋น ๋ด์ฉ์ ๊ณ ๋ คํ์ง ์์๊ธฐ ๋๋ฌธ์ด๋ค. (๋ง์ฝ์, ์๋ธ ๋ชจ๋์ด ์์๋ค๋ฉด ์ฑ๊ณต์ด๋ค!)

**`git plugin snippet`์ ์๋ธ ๋ชจ๋์ `init`๊ณผ `update`๊น์ง ์ง์ํด์ฃผ์ง ์๋๋ค.**

=> ์ด๋ ๊ฒ ์์ฑํ syntax๊ฐ ์ํ๋๋๋ก ๋์ํ์ง ์๋๋ค๋ฉด ๋ค๋ฅธ step์ ์ฐพ๊ฑฐ๋, ๊ณต์๋ฌธ์๋ฅผ ํตํด ์ํ๋ ์ค์ ์ด ์๋์ง ํ์ธํด์ผ ํ๋ค.


&nbsp;



**โ๏ธ ์๋ธ๋ชจ๋๊น์ง ๋ฐ์์ค๊ธฐ ์ํด ๋ค๋ฅธ step syntax์ ํ์ฉํด๋ณด์**

<img width="1685" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฅแซ 12 23 08" src="https://user-images.githubusercontent.com/72541544/212479697-767be7ee-0afb-497e-833b-533b18b993b0.png">

์๋ธ ๋ชจ๋๊น์ง ๋ฐ์์ค๊ธฐ ์ํด์๋ ๋ค๋ฅธ step syntax์ ํ์ฉํด๋ณด์!
checkout์ผ๋ก ๊ฒ์ํ์ฌ ํด๋น simple step์ ์ ํํ๋ค.
private repository๋ก ๋ฑ๋กํ ์๋ธ๋ชจ๋์ ๋ฐ์์ค๊ธฐ ์ํ ์ฌ์ ์ด๋ฏ๋ก! credentials๋ฅผ ์ธํํด์ค๋ค.


&nbsp;


<img width="1706" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฅแซ 12 24 19" src="https://user-images.githubusercontent.com/72541544/212479701-5f7ae833-59d6-44c6-9667-2b6a9d37ae58.png">
- `pipeline syntax`์์ `additional behaviours`์ add ๋ฒํผ์ ํด๋ฆญํ ํ, `Advanced sub-modules behaviours`๋ฅผ ๋๋ฌ ์์ ๊ฐ์ด ์ค์ ํด์ค๋ค.
  
- `Generate Pipeline Script`์ ๋๋ฌ์, ๋ถ๋ชจ ๋ ํฌ์งํ ๋ฆฌ์ `credentials`๋ฅผ ๊ทธ๋๋ก ํ์ฉํ๋ค.


&nbsp;


<img width="1716" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฅแซ 12 27 35" src="https://user-images.githubusercontent.com/72541544/212479703-c5a75d96-b92b-4cd8-b5e6-313352f0d78b.png">
- ์์ฑํ `pipeline script`๋ฅผ steps ํ์์ ๋ถ์ฌ๋ฃ์ด์ **๊ธฐ์กด์ `git syntax`๋ฅผ ๋์ฒดํด์ค๋ค.**
  
- ์๋ธ ๋ชจ๋ ๊ด๋ จ ๋ช๋ น์ด๊ฐ ์ถ๊ฐ๋์๋ค.


&nbsp;


**โ๏ธ ํ์ฌ๊น์ง์ ํ์ดํ๋ผ์ธ**

```pipeline
pipeline {
    agent any

    stages {
        stage('github clone') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [submodule(parentCredentials: true, reference: '', trackingSubmodules: true)], userRemoteConfigs: [[credentialsId: 'repo-and-hook-access-token-credentials', url: 'https://github.com/ToDoStudy/study_jenkins']])
            }
        }
        
        stage('build'){
            steps {
                dir('jenkins') {
                    sh '''
                        echo 'start bootJar'
                        ./gradlew clean bootJar
                    '''
                }
            }
        }
    }
}

```



&nbsp;


**โ๏ธ ํ์คํธ ๊ฒฐ๊ณผ**

์ฒ์์๋ 3์๊ฐ ์ ๋ ๊ธฐ๋ค๋ ค๋ ๋น๋์์ ์ค๋ฅ๊ฐ ๋ฐ์ํ์๋ค. (์ด๋ ๊ฐ์๋ฉ๋ชจ๋ฆฌ ec2 ๋ฉ๋ชจ๋ฆฌ ํฌ๊ธฐ๊ฐ 1GB ์ด๊ธฐ ๋๋ฌธ์ด๋ค.)


<img width="856" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฅแซ 10 10 16" src="https://user-images.githubusercontent.com/72541544/212519814-446ff96c-d927-4a88-924d-aff817d3ffa6.png">



<img width="1717" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฅแซ 10 09 20" src="https://user-images.githubusercontent.com/72541544/212519277-bafb92de-1638-480a-bd9e-bd64bf95cdf6.png">
<img width="849" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฅแซ 10 09 30" src="https://user-images.githubusercontent.com/72541544/212519290-24f52bdd-0552-43b9-a21f-3ba962b534a4.png">


&nbsp;


&nbsp;




# ๐ 5. ssh๋ฅผ ์ด์ฉํ์ฌ ์๋ฒ๋ก jar ํ์ผ ์ ๋ฌํ๊ธฐ

์ด์  ๋ฐฐํฌ์ฉ Jenkins์์ WAS์ฉ EC2๋ก Build ๊ฒฐ๊ณผ ํ์ผ์ ์ ๋ฌํด์ผ ํ๋ค.
์ด๋ฅผ ์ํด์๋ Publish over ssh ํ๋ฌ๊ทธ์ธ์ ํ์ฉํด์ฃผ๋ฉด ๋๋ค.


**โ๏ธ ํ๋ฌ๊ทธ์ธ ์ถ๊ฐ**

<img width="869" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 3 09 15" src="https://user-images.githubusercontent.com/72541544/212528116-7642a2aa-9a62-4c6f-b7ea-865f99b88699.png">
<img width="1714" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 3 09 59" src="https://user-images.githubusercontent.com/72541544/212528119-c870a71a-5b76-4e66-b1d9-526b731e2156.png">

&nbsp;

<img width="864" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 3 11 48" src="https://user-images.githubusercontent.com/72541544/212528120-3a752b1c-3726-4b5b-aa77-3b65e1c85b52.png">

- ssh๋ฅผ ํตํด ํ์ผ์ ๋ณด๋ด๊ธฐ์ ์, pemํค์ ์ ๋ณด๊ฐ ํ์ํ๋ค.
  
- EC2์ ์ ์ํ  ์ ์๋ pemํค์ ๋ด์ฉ์ ์ป์ด์จ ํ, ๋ด์ฉ์ ๋ณต์ฌํ ํ, EC2 ์ ์์ ํ์ํ pemํค์ ๋ด์ฉ์ ์ฌ์ง key์ ๋ถ์ฌ๋ฃ์ด ์ค๋ค.



<img width="818" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 4 20 56" src="https://user-images.githubusercontent.com/72541544/212528243-e59ad3c7-73a2-42da-8b60-a86ffe721397.png">


`Name` : syntax์์ ์ฐธ์กฐํ  ์ ์๋ ์ด๋ฆ
`HostName` : ๋น๋๋ ํ์ผ์ ์ ์กํ  ์๋ฒ์ private ip (๊ฐ์ vpc์ ์ํด์์ด private ip๋ก ์ ๊ทผํ  ์ ์๋ค.)
`username` : ubuntu(default)
`Remote Directory` : ํ์ผ์ด ๋์ฐฉํ  ๋๋ ํฐ๋ฆฌ๋ฅผ ์ ์ด์ค๋ค. (ec2 ๊ฐ์์๋ฒ์์ ์์ฑํ ๋๋ ํฐ๋ฆฌ๋ก ํด์ค์ผํจ ์๋๋ฉด,  `jenkins.plugins.publish_over.bappublisherexception` ๋ฐ์)

<img width="1475" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 4 28 24" src="https://user-images.githubusercontent.com/72541544/212528437-1b37d9e3-6f89-4e32-9b02-9b918749fabc.png">
<img width="1552" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 4 29 46" src="https://user-images.githubusercontent.com/72541544/212528455-bc7ffd7b-fd43-45cc-89c1-da16666b39b6.png">

ํ์ฌ๋ `/home/ubuntu`๋ก ๋ณ๊ฒฝ


<img width="661" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 4 28 55" src="https://user-images.githubusercontent.com/72541544/212528438-22fba431-8ac8-4b01-bcc9-1532ff12ab94.png">


&nbsp;


> **๐ก ์ฐธ๊ณ **
> (Ubuntu22๋ฒ์  ์ฌ์ฉํ  ๊ฒฝ์ฐ jenkins.plugins.publish_over.bappublisherexception: failed to connect and initialize ssh connection. message: failed to connect session for config ์ ๊ฐ์ ์ค๋ฅ๋ฅผ ๋ง๋  ์๋ ์์ผ๋ Ubuntu20.04.5 ์ฌ์ฉํ๊ธฐ๋ฅผ ๊ถ์ฅํ๋ค.) -> ๋ด๊ฐ ๊ฒฝํํ ์ค๋ฅ


&nbsp;

&nbsp;


### ๐ A. snippet์ ๋ง๋ค์ด๋ณด์! - sshPublisher simple step


<img width="861" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 9 40 00" src="https://user-images.githubusercontent.com/72541544/212541197-e931657f-99bc-4bc2-a3a3-7deff384c656.png">

<img width="1721" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 9 40 11" src="https://user-images.githubusercontent.com/72541544/212541198-4be8273f-e6b6-4816-8a55-88647b45c997.png">

- ssh Server ์ค์ ์์ ์ ์ธํ name์ ๋ฃ์ด์ค๋ค. (์๋ ์๋์ผ๋ก ๋ค์ด๊ฐ๋ค.)
  
- `Source files` : ์์คํ์ผ์ ์์น, gradlew wrapper์์ ๋น๋ ๊ฒฐ๊ณผ๋ฌผ์ `build/libs/`๋ก ์์นํ๋ฏ๋ก, `build/libs/*.jar` ๋ก ์์ฑํ์๋ค.
  
- `Remove prefix` : ์์คํ์ผ์์ ์๋ณธํ์ผ์ ๋๋ ํฐ๋ฆฌ๋ฅผ ์ด๋๊น์ง ํฌํจํ  ๊ฒ์ธ์ง์ ๋ํ ์ค์ 
  
- `remote directory` : ๋ฐฐํฌ๋  ๊ฒฝ๋ก๋ฅผ ์ ๋๋ค. ๋ฐฐํฌ ์๋ฒ์ ํด๋น ํด๋๋ก ๋ชฉ์ ํ์ผ์ด ๋์ฐฉํ๊ฒ ๋๋ค. (๋๋ ํฐ๋ฆฌ ๋ฏธ๋ฆฌ ๋ง๋ค์ด์ผ ํ๋ค.)
  
- `Exec command` : ์ ์ก์ ๋ง์น๊ณ  ์คํํ  shell ๋ฌธ์ ๋๋ ํฐ๋ฆฌ ๋ฐ ํ์ผ ์์น์ด๋ค.

&nbsp;

**โ๏ธ ํ๋ก์ ํธ์์ ์ ๊ณตํ๋ ๋ฐฐํฌ ์**

```bash
echo "> pid ํ์ธ"
CURRENT_PID=$(ps -ef | grep java | grep D208 | grep -v nohup | awk '{print $2}')
echo "$CURRENT_PID"
if [ -z ${CURRENT_PID} ] ;then
	echo "> ํ์ฌ ๊ตฌ๋์ค์ธ ์ ํ๋ฆฌ์ผ์ด์์ด ์์ผ๋ฏ๋ก ์ข๋ฃํ์ง ์์ต๋๋ค."
else
	echo "> sudo kill -9 $CURRENT_PID"
	sudo kill -9 $CURRENT_PID
	sleep 10
fi
echo "> jujeol ๋ฐฐํฌ"
JAR_PATH=$(ls -t /home/ubuntu/D208-Project/deploy/*.jar | head -1)
sudo nohup java -jar ${JAR_PATH} >> /home/ubuntu/D208-Project/logs/D208.log &
```

- `CURRENT_PID=$(ps -ef | grep java | grep D208 | grep -v nohup | awk '{print $2}')` : `CURRENT_PID`์ ํ์ฌ ์คํ๋๊ณ  ์๋ ํ๋ก์ ํธ์ pid๋ฅผ ๋ฐ์์จ๋ค.
  
- ์์ ์์ฑํ๊ธฐ ์  ์ง์  ์๋ฒ๋ฅผ ์คํํ๊ณ  ํด๋น ๋ช๋ น์ด๋ฅผ ์๋ ฅํด์ pid๋ฅผ ์ ์ก์์ค๋์ง ํ์ธํ๋ค.
  
  - `ps -ef | grep java | grep D208 | grep -v nohup | awk '{print $2}'`

- `CURRENT_PID`๊ฐ ์๋ค๋ฉด ๋จผ์  ์ข๋ฃํ๋ค. (์ง๋ค์ด ์๊ฐ์ด ์๊ธฐ ๋๋ฌธ์ sleep์ ํด์ค๋ค.)
  
- ์ข๋ฃ๊ฐ ๋๋๋ฉด `deploy` ํด๋์์ ๋ง์ง๋ง jar์, 80port์ dev ํ๋กํ๋ก ์คํํ๋ค.


&nbsp;


> ๐ ๋ฆฌ๋์ค `2>&1` ๊ทธ๋ฆฌ๊ณ  `/dev/null`
> 
> ์ฐธ๊ณ  : https://inpa.tistory.com/entry/%EB%A6%AC%EB%88%85%EC%8A%A4-devnull-%EB%A6%AC%EB%8B%A4%EC%9D%B4%EB%A0%89%EC%85%98-%EA%B8%B0%ED%98%B8-%EC%A2%85%EB%A5%98
> 
> (1) `2>&1`
> <img width="1044" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 9 53 40" src="https://user-images.githubusercontent.com/72541544/212541916-8db7e632-ccdc-45c7-b084-9a31c8129b78.png"><img width="898" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 9 53 56" src="https://user-images.githubusercontent.com/72541544/212541917-bd804105-8415-44c1-a9a8-cc006c22695a.png">
> 
> (2) `/dev/null`
> 
> - `/dev/null`๋ก ๊ฒฐ๊ณผ๋ฅผ ๋ณด๋ธ๋ค๋ ๊ฒ์, ๋ฐ์ดํฐ๋ฅผ ์ฃ๋คย ๋ง๋ํ ์์ ๋ฒ๋ ค์ย ๊น๋ํ๊ฒ ํ๋ฉด์ ํ์ํ์ง ์๋๋ค๋ ๊ฒ์ ๋งํ๋ค.
>   
>   <img width="1080" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 9 56 44" src="https://user-images.githubusercontent.com/72541544/212542006-b31b8c11-d6d1-4ed1-a10b-a317645536f2.png">
> 


&nbsp;
<img width="1689" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 9 40 18" src="https://user-images.githubusercontent.com/72541544/212541199-b1829d62-cdd1-4d64-a463-3995d48b4936.png">
- Generate Pipeline Scriptํด๋ฆญ์ ํตํด ๋ฐ๊ธ ๋ฐ๋๋ค.
  
- snippet์ stage๋ก ๋ง๋ค์ด๋ณด์.
  
- **sshPublisher ๊ฐ์ ๊ฒฝ์ฐ verbose ์ต์์ด ์๋๋ฐ, ํด๋น ์ต์์ true๋ก ์ฃผ๋ฉด ํธ๋ฌํ ์ํ์ ์ ์ฉํ๋ค.**  ๋น๋์ console output์ ํด๋น ๋ด์ฉ์ด ์์ธํ ์ฐํ๋ค. (true ์ค ์, ๋๋ฒ)

&nbsp;

ํ์ฌ๊น์ง์ ํ์ดํ๋ผ์ธ

```bash
pipeline {
    agent any

    stages {
        stage('git clone') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [submodule(parentCredentials: true, reference: '', trackingSubmodules: true)], userRemoteConfigs: [[credentialsId: 'repo-and-hook-access-token-credentials', url: 'https://github.com/ToDoStudy/study_jenkins']])
            }
        }
        
        stage('build'){
            steps {
                dir('jenkins') {
                    sh '''
                        echo 'start bootJar'
                        ./gradlew clean bootJar
                    '''
                }
            }
        }
        
        stage('publish on ssh'){
            steps{
                dir('jenkins'){
                    sshPublisher(publishers: [sshPublisherDesc(configName: 'ECGumD208', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'sh /home/ubuntu/D208-Project/script/init_server.sh', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/D208-Project/deploy', remoteDirectorySDF: false, removePrefix: 'build/libs', sourceFiles: 'build/libs/*.jar')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: true)])
                }
            }
        }
    }
}


```


&nbsp;


**โ๏ธ ์ฑ๊ณต์ ์ผ๋ก ์คํ๋์๋์ง ํ์ผ ํ์ธ**


<img width="664" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 9 38 42" src="https://user-images.githubusercontent.com/72541544/212541193-62e2aa45-8eee-4fdf-98d5-6684c643715a.png">

<img width="1721" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 9 39 21" src="https://user-images.githubusercontent.com/72541544/212541195-3bcca784-eff9-4d43-ba07-67bba0c0f89f.png">

<img width="865" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 9 40 53" src="https://user-images.githubusercontent.com/72541544/212541200-5b8aad3c-258e-440f-b1a2-0e77094cfe8a.png">

<img width="860" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 9 41 07" src="https://user-images.githubusercontent.com/72541544/212541201-3736699b-ae5d-44ab-b8f5-35eae3de67b9.png">

<img width="1684" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 9 41 12" src="https://user-images.githubusercontent.com/72541544/212541202-7a96ed4a-6abe-47ee-9680-1e5b68133367.png">

<img width="1703" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 9 41 17" src="https://user-images.githubusercontent.com/72541544/212541204-3bb564f6-5c43-43b0-9e9c-b31d0892bea7.png">



- ์ฑ๊ณต์ ์ผ๋ก ์คํ๋ ๊ฒฐ๊ณผ๋ค. (EC2 ์ฝ์์์ `ps -ef | grep java` ๋ช๋ น์ด๋ฅผ ํตํด ๊ตฌ๋์ด ์๋์๋์ง ํ์ธํ๋ค.)
  
- ๋ค๋ง, ์คํํ๋ค 2๋ถ๋ค ์ข๋ฃ๋๋ค. ๊ทธ์ ๊น์ง๋ ์๋ก๋๊ฐ ๊ณ์ ์งํ์ค์ด์๋ค.



=> ์ด์  Jenkins ์น ์ฝ์์ ์ ์ํด build now๋ฅผ ๋๋ฅด๋ฉด ํ๋ก๊ทธ๋จ์ ์๋ ๋ฐฐํฌํ  ์ ์๋ ๋ฐํ์ ๋ง๋ จํ๋ค!

&nbsp;

&nbsp;


# ๐ 6. ๋น๋ ์ ๋ฐํ๊ธฐ

**โ๏ธ github์์ ์ ๊ณตํ๋ webhook**

- ํน์ ํ ์ด๋ฒคํธ๊ฐ ๋ฐ์ํ์ ๋, ํด๋น ๋ด์ฉ์ ๋ฑ๋กํด๋์ api๋ก ๋ณด๋ด์ฃผ๋ ๊ธฐ๋ฅ์ด๋ค.
  
- ์ด ๊ธฐ๋ฅ์ ํ์ฉํ์ฌ github์์ ํน์ ํ ํ๋์ด ์ผ์ด๋ฌ์ ๋ job์ด ์ ๋ฐ๋๋๋ก ๊ตฌํํ  ์ ์๋ค.

=> ์ด๋ฅผ ์ ์ฉํด๋ณด๊ธฐ ์ํด PR์ด merge๋  ๋ ์๋์ผ๋ก ๋น๋๊ฐ ์ผ์ด๋๋๋ก ์ค์ ํด๋ณด์!

&nbsp;


> **๐ก ์ฐธ๊ณ **
> `Github hook trigger for GITScm polling` ์ต์์ freestyle์์ build trigger๋ก ๋ง์ด ์ฌ์ฉํ์๋ค.
> **ํ์ง๋ง, pipeline์์๋ ์ ๋๋ก ๋์์ํค๊ธฐ ์ด๋ ต๊ณ  ๋ํ์ผํ ์ธํ์ ํ  ์ ์๋ค๋ ๋จ์ ์ด ์๋ค.**


&nbsp;

**โ๏ธ ๋ฐฑ์๋ PR merge์๋ง Jenkins๊ฐ ๋์ํ๋๋ก ๋ง๋ค์ด๋ณด์!**

์ด๋ป๊ฒ ํ๋ฉด ๋ ๊น?

=> Pull Request์ ๋ผ๋ฒจ์ ๋ฐํ์ผ๋ก ๋ฐฑ์๋์ ํ๋ก ํธ์๋ PR์ ๊ตฌ๋ถํ๋๋ก ํด๋ณด์!

=> ๋ฐฑ์๋ ๋ผ๋ฒจ์ด ๋ถ์ด ์๋ PR์ด ๋จธ์ง ๋์์ ๋๋ง ๋น๋๊ฐ ์ผ์ด๋๋๋ก ํด๋ณด์!


&nbsp;

**โ๏ธ Generic Webhook Trigger ํ๋ฌ๊ทธ์ธ ์ค์น**


<img width="672" alt="แแณแแณแแตแซแแฃแบ 2023-01-15 แแฉแแฎ 11 09 07" src="https://user-images.githubusercontent.com/72541544/212545615-c18d9ca7-2a62-40d3-9675-c92b96d7ebb9.png">



&nbsp;

ํ์ดํ๋ผ์ธ์ ์์ธ๋ด์ฉ์์ `build triggers`๋ก ์ด๋ํ๋ฉด, `generic webhook trigger`๊ฐ ์ถ๊ฐ๋ ๊ฒ์ ๋ณผ ์ ์๋ค.


๋ผ๊ณ  ํ์ง๋ง, ์ผ๋จ์ ์๊ฐ์ด ์์ด

`Github hook trigger for GITScm polling` ์ ์ฌ์ฉํ๋ค.


<img width="731" alt="แแณแแณแแตแซแแฃแบ 2023-01-16 แแฉแแฅแซ 12 06 21" src="https://user-images.githubusercontent.com/72541544/212549099-2938b701-1f2f-4669-b6dd-27aca8279ab7.png">




&nbsp;


&nbsp;



-----
์ฐธ๊ณ 
- https://velog.io/@sihyung92/%EC%9A%B0%EC%A0%A0%EA%B5%AC2%ED%8E%B8-%EC%A0%A0%ED%82%A8%EC%8A%A4-%ED%8C%8C%EC%9D%B4%ED%94%84%EB%9D%BC%EC%9D%B8%EC%9D%84-%ED%99%9C%EC%9A%A9%ED%95%9C-%EB%B0%B0%ED%8F%AC-%EC%9E%90%EB%8F%99%ED%99%94
