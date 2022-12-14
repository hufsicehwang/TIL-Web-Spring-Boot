# ๐ฒTIL-3๐ฒ

## 1. Repository
- ๋ฐ์ดํฐ๋ฒ ์ด์ค์ ์ ๊ทผํ์ฌ CRUD์ ์ฐ์ฐ์ ํ  JPA์ ๋ํด์ ์์ฑํ๋ ๋ถ๋ถ์ด๋ค.
- ์ธํฐํ์ด์ค์ ์ถ์๋ถ์ implements ํ๋ ๊ตฌํ๋ถ๋ก ๋๋์ด์ ธ ์๋ค.
```java
public interface MemberRepository {
    Member save(Member member);
    Optional<Member> findById(int Id);
    List<Member> findAll();
}v
```
> __DataBase CRUD ์ฐ์ฐ ์์ฑ!__
> > optional์ ์ฌ์ฉํ๋ ์ด์ ๋ NPE(NullPointException)์ ํผํ๊ธฐ ์ํจ์ด๋ค. (ํน์  tupple์ ์ฐพ๋ Read ์ฐ์ฐ์ ์ฐพ์๋ณด๊ณ  ์์ผ๋ฉด NULL์ ๋ฐํํ๊ธฐ ๋๋ฌธ์ optional์ ์ฌ์ฉ)

```java

public class JpaMemberRepository implements MemberRepository {

    private final EntityManager em;
    public JpaMemberRepository(EntityManager em) {
        this.em = em;
    }

    @Override
    public Member save(Member member) {
        em.persist(member);
        return member;
    }

    @Override
    public Optional<Member> findById(int Id) {
        Member member = em.find(Member.class, Id);
        return Optional.ofNullable(member);
    }

    @Override
    public List<Member> findAll() {
        return em.createQuery("select m from Member m", Member.class)
                .getResultList();
    }
}

```
> `JPA` ์์ฑ์ ์ํด `EntityManager`๋ฅผ ์ฌ์ฉํ๋ค!!!
> > EntityManager ๋ด์ฅ ํจ์ `createQuery` : SQL ์์ฑ, `persist` : entity์ ์์์ฑ์ ๋ถ์ฌ, `find` : ์ฆ์๋ก๋ฉ ๋ฐฉ์์ผ๋ก `PK`๋ฅผ ํ์ฉํ์ฌ __ํ๋์ ๊ฐ์ฒด๋ฅผ ๋งคํ!!!__
> > > `์ง์ฐ๋ก๋ฉ` : JDBC ๊ฐ์ ๋๋ ์ธ ๊ฒ ๊ฐ์(๋๋ฆผ, ์ฝ๋๊น), `์ฆ์๋ก๋ฉ` : EntityManager์ ๋ด์ฅ ํจ์๋ฅผ ์ฌ์ฉํด์ ๊ฐ์ฒด๋ฅผ ๋น ๋ฅด๊ฒ ๋งคํ
