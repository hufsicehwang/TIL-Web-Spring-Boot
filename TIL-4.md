# ๐ฆTIL-4๐ฆ

# Service
- Repository์์ ์์ฑํ DAO๋ฅผ ์ด์ฉํด์ database์ data์ ์ ๊ทผํด์ ์ํ ํ  transacion์ ์์ฑ ํ๋ค.
```java
public class MemberService {
    private final MemberRepository memberRepository;
    public MemberService(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }

    @Transactional
    public int join(Member member) {

        memberRepository.save(member);
        return member.getId();
    }
    @Transactional
    public List<Member> findMembers() {

        return memberRepository.findAll();
    }
    @Transactional
    public Optional<Member> findOne(int memberId) {

        return memberRepository.findById(memberId);
    }
}
```
> `@transactional` ์ด๋ธํ์ด์์ ์ฌ์ฉํด์ ํด๋น ๋ฉ์๋๊ฐ transaction์ด ๋๋๋ก ๋ณด์ฅํด ์ค๋ค.
>>  Spring์ ํด๋น ๋ฉ์๋์ ๋ํ ํ๋ก์๋ฅผ ๋ง๋ ๋ค. ํ๋ก์ ํจํด์ ๋์์ธ ํจํด ์ค ํ๋๋ก, ์ด๋ค ์ฝ๋๋ฅผ ๊ฐ์ธ๋ฉด์ ์ถ๊ฐ์ ์ธ ์ฐ์ฐ์ ์ํํ๋๋ก ๊ฐ์ ํ๋ ๋ฐฉ๋ฒ์ด๋ค. 
>>>  ํธ๋์ญ์์ ๊ฒฝ์ฐ, ํธ๋์ญ์์ ์์๊ณผ ์ฐ์ฐ ์ข๋ฃ์์ ์ปค๋ฐ ๊ณผ์ ์ด ํ์ํ๋ฏ๋ก, ํ๋ก์๋ฅผ ์์ฑํด ํด๋น ๋ฉ์๋์ ์๋ค์ ํธ๋์ญ์์ ์์๊ณผ ๋์ ์ถ๊ฐํ๋ ๊ฒ์ด๋ค.

# Controller
- ์ฌ์ฉ์์ ์์ฌ์ํต ํ  ์ ์๋ point์ด๋ค.
- View์์ ์์ฒญ ๋ฐ์ ๊ฒ์ ์ด๋ค Service๋ก ๋งคํ ์ํฌ ๊ฒ ์ธ๊ฐ๋ฅผ ์ ํ๋ค.
- Service์์ ์ฒ๋ฆฌํ ๊ฒฐ๊ณผ๋ฅผ View๋ก ์๋ตํ์ฌ ๋ณด์ฌ ์ค๋ค.
  - API๋ฅผ ์์ฑํ๋ค. 
```java
@Controller
public class MemberController {

    private final MemberService memberService;

    @Autowired
    public MemberController(MemberService memberService) {
        this.memberService = memberService;
    }

    @GetMapping("/members/new")
    public String createForm() {

        return "members/createMemberForm";
    }

    @PostMapping("/members/new")
    public String create(MemberForm form) {
        Member member = new Member();
        member.setName(form.getName());
        member.setTeam(form.getTeam());
        member.setTitle(form.getTitle());
        member.setText(form.getMessage());
        member.setRegisterTime(LocalDateTime.now());

        memberService.join(member);

        return "redirect:/members";
    }

}
```
> `get`, `post`, `put`, `patch`, `delete`์ ๋ํด์ mapping ํ๋ค.
> > ํน์ ํ request์ ๋ํด์ ์ฌ๋ฐ๋ฅธ Service๋ฅผ ์ ํํ๋ค.

## @Autowired
- ์คํ๋ง DI(Dependency Injection)์์ ์ฌ์ฉ๋๋ ์ด๋ธํ์ด์
- ์คํ๋ง์์ ๋น ์ธ์คํด์ค๊ฐ ์์ฑ๋ ์ดํ @Autowired๋ฅผ ์ค์ ํ ๋ฉ์๋๊ฐ ์๋์ผ๋ก ํธ์ถ๋๊ณ , ์ธ์คํด์ค๊ฐ ์๋์ผ๋ก ์ฃผ์
- ํด๋น ๋ณ์ ๋ฐ ๋ฉ์๋์ ์คํ๋ง์ด ๊ด๋ฆฌํ๋ Bean์ ์๋์ผ๋ก ๋งคํํด์ฃผ๋ ๊ฐ๋

### DI(Dependency Injection)๋
- DI(์์กด์ฑ ์ข์, Dependency Injection)๋, ํด๋์ค๊ฐ์ ์์กด๊ด๊ณ๋ฅผ ์คํ๋ง ์ปจํ์ด๋๊ฐ ์๋์ผ๋ก ์ฐ๊ฒฐํด์ฃผ๋ ๊ฒ

### DI๊ฐ ํ์ํ ์ด์ 
![image](https://user-images.githubusercontent.com/67450413/184641438-917ae46f-fc52-47dc-a244-11dd39a51256.png)
- SW๋ฅผ ์ฌ์ฉํ๋ ๊ณ ๊ฐ์ Factory ํด๋์ค๋ง์ ํธ์ถํด์ผํ๋ฉฐ, ๊ทธ๊ฒ์ด ConsoleFactory์ธ์ง UserFactory์ธ์ง ๋ชฐ๋ผ์ผ ํจ
- ๊ณ ๊ฐ๋ง๋ค ์ ์ฉ Factory๋ฅผ ์์ฑํ  ๊ฒฝ์ฐ ์ฝ๋ ์์ฐ์ฑ์ด ๋จ์ด์ง๋ฉฐ, ๊ณ ๊ฐ์ด ๋ชฐ๋ผ๋ ๋๋ ์ฝ๋๊ฐ ๋ธ์ถ ๋จ
- ๋๋ฌธ์ ์คํ๋ง์ Factory๊ฐ ConsoleFactory์ธ์ง UserFactory์ธ์ง๋ฅผ ํ๋ ์์ํฌ๊ฐ ์๋์ผ๋ก ๊ฐ์ฒด๊ฐ ์์กด์ฑ์ ์ฃผ์
