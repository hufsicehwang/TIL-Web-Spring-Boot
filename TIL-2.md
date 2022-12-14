# ๐ฆTIL-2๐ฆ
## Spring Boot ์ ํ์ ์ธ package ๊ตฌ์กฐ
- Controller
- DTO
- Service
- Repository
- Domain (Entity)
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FC7HSi%2FbtrtYU5BG4N%2FuaTJCaFk9ikMg4JkalvU71%2Fimg.png"></img>

## 1. Domain
- DB ํ์ด๋ธ๊ณผ ์ง์  ๋งตํ๋๋ ํด๋์ค๋ก์ JPA ์ฌ์ฉ ์ ์ด๋ธํ์ด์์ ์ด์ฉํ์ฌ ํ์ด๋ธ, ํ๋, ๋ฑ์ ์ค์ ํ๋ค.
- domain๊ณผ client๋ฅผ ์ง์  ์ฐ๊ฒฐํ์ง ์๊ณ  DTO๋ฅผ ์ด์ฉํด์ ๋ถ๋ฆฌํ๋ค.
  -  Client ์ชฝ๊ณผ ์ฐ๊ฒฐ๋ ๋ถ๋ถ์ ์ฆ์ ๋ณ๊ฒฝ์ฌํญ์ด ์์ ์ ์๋๋ฐ Domain๊ณผ ์ฐ๊ฒฐ๋์ด ์์ฃผ ๋ณ๊ฒฝ๋๊ฒ ๋๋ค๋ฉด ์ฌ๋ฌ ํด๋์ค์ ์ํฅ์ ๋ฏธ์น๊ธฐ ๋๋ฌธ์ ๋ถ๋ฆฌํ๋ค.
  -  View ๋จ๊ณผ DB ๋จ์ ํ์คํ๊ฒ ๋ถ๋ฆฌํ์ฌ ๊ด๋ฆฌํ๋ค.
```java
  package hello.hellospring.domain;
import javax.persistence.Entity;

@Entity
public class Member {
    private String title;
    private String text;

    }
    public String getTitle() {
        return title;
    }
    public void setTitle(String title) {
        this.title = title;
    }

    public String getText() {
        return text;
    }
    public void setText(String text) {
        this.text = text;
    }
}
```
> ๊ธฐ๋ณธ์ ์ธ ์ด๋ธํ์ด์ : @Entity
> > DB table์ ํฌํจ๋๋ attribute๋ค์ ๊ฐ์ง๋ค.
> > > setter์ getter๋ฅผ ์ค์ ํ๋ค. (`ALT`+`insert`ํค๋ก ์๋ ์์ฑ ๊ฐ๋ฅ)

## 2. DTO
- Data Transfer Object๋ก "๋ฐ์ดํฐ ์ ์ก ๊ฐ์ฒด"์ด๋ค.
- Domain์ DB ํ์ด๋ธ์ ๋ํ ์ ๋ณด๋ฅผ ๊ฐ์ง๊ณ  ์๋ ํด๋์ค์ด๊ณ , DTO๋ ํด๋น ํ์ด๋ธ์์ ์ค์ ๋ก CRUD๋ฅผ ํ  ํ๋๋ฅผ ์ ์ํด๋ ๊ฒ ์ด๋ค.
```java
package hello.hellospring.domain;

public class MemberForm {
    private String title;
    private String message;

    public String getTitle() {
        return title;
    }
    public void setTitle(String title) {
        this.title = title;
    }

    public String getMessage() {
        return message;
    }
    public void setMessage(String message) {
        this.message = message;
    }
}

```
> ๊ธฐ๋ณธ์ ์ธ ์ด๋ธํ์ด์ : ์์
> > ์ก๊ฒ ์๊ฐํด client ์ธก์์ ์๋ ฅ ๋ฐ์ POST ์์ฒญ ์ฌ ๋ฐ์ดํฐ์ ํด๋นํ๋ค.
> > > setter์ getter๋ฅผ ์ค์ ํ๋ค. (`ALT`+`insert`ํค๋ก ์๋ ์์ฑ ๊ฐ๋ฅ)
