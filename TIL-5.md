# ๐ฑTIL-5๐ฑ

## YAML์ด๋
- ๋ฐ์ดํฐ ํํ ์์์ ํ ์ข๋ฅ
- ์ฐ๋ฆฌ๊ฐ ์ผ๋ฐ์ ์ผ๋ก ์ฌ์ฉํ๋ JSON, XML ๋ณด๋ค๋ ๋์ฑ ์ธ๊ฐ์ด ๋ณด๊ณ  ์ดํดํ๊ธฐ ์ฌ์ด ํํ
- YAML, YLM์ด๋ผ๊ณ  ํ๊ธฐํ๋ฉฐ ๋ณดํต`์ผ๋ฏ`์ด๋ผ๊ณ  ๋ฐ์ ํ๋ค.

### YAML ํฌ๋ฉง
```yaml
#YAML
Servers:
  - name: Server1
    administrator: Kim
    created: 20050103132749
    status: active
  - name: Server2
    administrator: Lee
    created: 20210101000000
    status: active
```
### JSON ํฌ๋ฉง
```xml
#JSON
{
  Servers:[
    {
      name: Server1,
      administrator: Kim,
      created: 20050103132749,
      status: active
    },
    {
      name: Server2,
      administrator: Lee,
      created: 20210101000000,
      status: active
    }
  ]
}
```
### XML ํฌ๋ฉง
```xml
#XML
<servers>
  <entry>
    <name>server1</name>
    <administrator>kim</administrator>
    <created>20050103132749</created>
    <status>active</status>
  </entry>
  <entry>
    <name>server2</name>
    <administrator>Lee</administrator>
    <created>20210101000000</created>
    <status>active</status>
  
  </entry>
</servers>
```

## YAML ์ฌ์ฉ๋ฐฉ๋ฒ
- key-value๋ก ๋ฐ์ดํฐ ์ ์
- ๋ค์ฌ์ฐ๊ธฐ๋ ๊ธฐ๋ณธ์ ์ผ๋ก 2์นธ, 4์นธ ์ฌ์ฉ
- ์ฌ๋ฌ ๋ฐ์ดํฐ๋ฅผ ๋ฐฐ์ด์์๋ก ํํ์ ์์๋ถ๋ถ์ `-` ๊ธฐํธ ์ฝ์
- ์ฃผ์์ `#` ์ฌ์ฉ
- https://yaml.org/   ๊ณต์ reference

# YAML ์ฌ์ฉํ๊ธฐ
## 1.YAML๋ก file ๊ฒฝ๋ก ์ง์ ํ๊ธฐ
- `resource` directory ๋ด๋ถ์ application.yml์ ์์ฑํ๋ค.
```yaml
tools:
  log-path:
    base: C:\Users\User\Desktop\log
    dags1: C:\Users\User\Desktop\log\dags1
    dags2: C:\Users\User\Desktop\log\dags2
    dems1: C:\Users\User\Desktop\log\dems1\trace
    dems2: C:\Users\User\Desktop\log\dems2\trace
```

## 2.Component ์ง์ 
- `component` ํจํค์ง ์์ฑ ํ `ToolProperties.java` ์์ฑ
```java
@Component
@Getter
public class ToolProperties {
    @Value("${tools.log-path.base}")
    private String logBasePath;

    @Value("${tools.log-path.dags1}")
    private String dags1LogPath;

    @Value("${tools.log-path.dags2}")
    private String dags2LogPath;

    @Value("${tools.log-path.dems1}")
    private String dems1LogPath;

    @Value("${tools.log-path.dems2}")
    private String dems2LogPath;
}
```
> class ๋ณ์์ `@Value` ์ด๋ธํ์ด์์ ์ฌ์ฉํด์ ํ ๋น
> > `@Component` ์ด๋ธํ์ด์์ ์ฌ์ฉํด์ Bean Configuration ํ์ผ์ Bean์ ๋ฐ๋ก ๋ฑ๋กํ์ง ์๊ณ ๋ ๋น๋์ bean ๊ฐ์ฒด ์๋ ๋ฑ๋ก
> > > ์ถํ ์ฌ์ฉํ๊ณ ์ ํ๋ ๋ถ๋ถ์์ class ๋ณ์๋ฅผ ์ด์ฉํด getter method๋ก ์ฌ์ฉ
