# ๐ณTIL-1๐ณ

## 1. ํ๋ก์ ํธ ์์ฑ ๋ถํฐ ์คํ
1. IntelliJ ๋๋ Eclipse ์ค์น
2. JDK๋ 11 ๋ฒ์ ์ผ๋ก ์ค์นํ๋๊ฒ ์ค๋ฅ๋  ํ๋ฅ  ์ ์
3. https://start.spring.io/ ์์ ์คํ๋ง ํ๋ก์ ํธ ์์ฑ
    - Project: Gradle Project
    - Spring Boot: 2.3.x
    - Java: 11
    - __Dependencies: Spring Web, Thymeleaf__
4. IntelliJ๋ก Open
5. src ์ฐํด๋ฆญ -> mark directory as -> root source
6. (ํ๋ก์ ํธ๋ช)Aplication.java ๋ด๋ถ์ ๋ฉ์ธ ๋ฉ์๋ Run
7. `http://localhost:8080/`์์ ํ์ธ

## 2. MVC ๋ชจ๋ธ
![image](https://user-images.githubusercontent.com/67450413/181166692-6f9a976d-0e70-4785-ac21-9b4800ecaff7.png)
- Model : ๋ฐ์ดํฐํ์ด์ค์ ์ฐ๋ํ์ฌ ์ฌ์ฉ์๊ฐ ์๋ ฅํ ๋ฐ์ดํฐ๋ ์ฌ์ฉ์์๊ฒ ์ถ๋ ฅํ  ๋ฐ์ดํฐ๋ฅผ ๋ค๋ฃธ
  - domain, repository, service์ ํด๋น๋จ
- View : ๋ชจ๋ธ์ด ์ฒ๋ฆฌํ ๋ฐ์ดํฐ๋ ๊ทธ ์์ ๊ฒฐ๊ณผ๋ฅผ ๊ฐ์ง๊ณ  ์ฌ์ฉ์์๊ฒ ์ถ๋ ฅํ  ํ๋ฉด์ ๋ง๋ฌ
  - html๋ก ๊ตฌ์ฑ๋ thymeleaf(template engine)์ ํด๋น๋จ 
- Controller : client ์ธก์์ requestํ์๋ response ํด์ค ํจ์๋ฅผ mapping ํด์ค
  - controller.java์ ํด๋น๋จ

##  3. Spring Boot ๋ด๋ถ ์์
### gradle
> Ant์ Maven๊ณผ ๊ฐ์ ์ด์  ์ธ๋ ๋น๋ ๋๊ตฌ์ ๋จ์ ์ ๋ณด์ํ๊ณ  ์ฅ์ ์ ์ทจํฉํ์ฌ ๋ง๋  ์คํ์์ค `๋น๋ ๋๊ตฌ`
### /sql/ddl.sql
> ์ฐ๋๋ ๋ฐ์ดํฐ๋ฒ ์ด์ค์ ์คํํ  ์ ์๋ SQL Data Definition Language
### /src/main/resource/application.properties
> ๋ฐ์ดํฐ๋ฒ ์ด์ค ์ฐ๊ฒฐ ์ค์  ์ถ๊ฐ
>> ์คํ๋ง๋ถํธ 2.4๋ถํฐ๋ `spring.datasource.username`๋ฅผ ๊ผญ ์ถ๊ฐ ํด์ผํจ.
### /src/main/java/ํ๋ก์ ํธ/domain/Member.java
> ๋ชจ๋ธ ๊ณ์ธต์ธ domain์์ `Entity`์ ํด๋น 
### /src/main/java/ํ๋ก์ ํธ/domain/MemberForm.java
> ๋ชจ๋ธ ๊ณ์ธต์ธ domain์์ `DTO(Data Transfer Object)`์ ํด๋น
### /src/main/java/ํ๋ก์ ํธ/repository/MemberRepository.java
> DAO๋ฅผ ์์ฑํ  ์ถ์๋ถ๋ฅผ ์ ์ํ ์ธํฐํ์ด์ค
### /src/main/java/ํ๋ก์ ํธ/repository/JpaMemberRepository.java
> DAO๋ฅผ JPA๋ฅผ ํตํด์ ์์ฑ
### /src/main/java/ํ๋ก์ ํธ/service/MemberService.java
> __`Repository`์์ JPA๋ฅผ ์ด์ฉํด์ ์์ฑํ DAO์ transaction์ ์์ฑ__
### /src/main/java/ํ๋ก์ ํธ/MemberController.java
> POST, GET๊ณผ ๊ฐ์ Request์ ๋ํ Response ๋งตํ ํ ํ์ด์ง rendering, redirecting
