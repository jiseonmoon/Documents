# 1. 문자, 폰트

## 1-1. D2 Coding 글꼴

네이버 개발자센터에서 배포하는 코딩용 폰트이다. 개발자의 코딩을 위해 가독성 및 유사 문자간 변별력 뿐만 아니라 디자인적으로 한글과의 조화를 고려해 최적화시킨 글꼴이다.

- 코딩시 유사한 형태의 영문/숫자 뿐만 아니라 한글/특수문자 등에 대한 변별력과 가독성을 강화함
- 고정폭 글꼴로 제작이 되어 어떤 개발환경에서도 자간과 행간을 유지하도록 디자인됨

## 1-2. Eclipse 프로젝트 UTF-8 설정

1. Window > Preferences > General > Workspace에서 인코딩을 UTF-8으로 변경
2. HTML, CSS, JSP 파일에 대한 설정 역시 UTF-8을 사용하도록 설정

## 1-3. 문자인코딩

문자나 기호들의 집합을 컴퓨터에서 표현(부호화)하는 방법이다.

> 컴퓨터는 0과 1, 즉 2진수만 가지고 모든 데이터를 표현하기 때문에 문자를 표현할 숫자 코드가 필요하게 되었다. 이에 따라 각 컴퓨터마다 독자적인 문자 인코딩을 사용하기 시작했고, 미국 내에서 이를 통합하기 위해 ASCII 코드가 만들어져 사용되어 왔다. 대부분의 문자 코드 인코딩은 ASCII 코드 방식을 확장한 것이다.

## 1-4. 문자 집합(Character Set)과 인코딩(Encoding)

**문자 집합**

```
정보를 표현하기 위한 글자나 기호들의 집합을 정의한 것이다.
```

**인코딩**

```
이런 문자나 기호의 집합을 컴퓨터에서 저장하거나 통신에 사용할 목적으로 부호화 하는 것을 문자 인코딩(부호화)이라 하고 인코딩 된 문자 부호(Character code)를 다시 디코딩(복호화)하여 본래 문자나 기호로 표현할 수 있다.
```

- **조합형 한글** : 초, 중, 종성에 해당하는 문자를 각각 부호화하여 문자에 따라 부호를 조합하여 만드는 방식이다.
- **완성형 한글** : 한글을 그 구조와 관계 없이 코드를 배당하여 표현하는 방식이다.
  - KSC5601 : 완성형과 조합형의 모든 한글 문자의 표현이 가능한 한글 문자 부호 표준이다.
  - EUC-KR : EUC(확장 유닉스 코드)의 일종이며 한글 표현을 위한 문자 인코딩이다.
  - CP949 : 마이크로소프트에서 사용하는 한글 문자의 부호표이다.
- **유니코드** : 전세계의 모든 문자를 동일하게 표현하기 위한 산업표준이다.
  - UTF : 유니코드 형태의 문자를 변환하기 위한 공식이다. UTF-7, UTF-8, UTF-16BE, UTF-16LE등의 종류가 있다.



# 2. mysql, utf-8 설정

## 2-1. Database, table utf-8 설정

- Database 생성 시 설정

  ```mysql
  CREATE DATABASE 데이터베이스명 DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
  ```

- 이미 생성 된 DB의 설정

  ```mysql
  ALTER DATABASE 데이터베이스명 DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
  ```

- table 생성 시 설정

  ```mysql
  CREATE TABLE tableName (
    ...
  ) DEFAULT CHARACTER SET utf8 COLLATE utf8_general_cri;
  ```

- 이미 생성 된 table의 설정

  ```mysql
  ALTER TABLE 테이블명 DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
  ```

## 2-2. server, client utf-8 설정

C:\ProgramData\MySQL\MySQL Server 8.0\my.ini 파일을 수정 혹은 생성

```
[client]
default-character-set=utf8

[mysqld]
character-set-client-handshake = FALSE
init_connect="SET collation_connection = utf8_general_ci" init_connect="SET NAMES utf8"
character-set-server = utf8

[mysql]
default-character-set=utf8

[mysqldump]
default-character-set = utf8
```

## 2-3. connection string

```
db_url      = jdbc:mysql://HOST/DATABASE
db_driver   = com.mysql.jdbc.Driver
db_username = USERNAME
db_password = PASSWORD
```

## 2-4. user 생성과 DB, table 권한 

```mysql
CREATE USER '유저명'@'localhost' IDENTIFIED BY '비밀번호';

GRANT ALL PRIVILEGES ON 데이터베이스명.테이블명 TO '유저명'@'localhost';
```

## 2-5. innodb, myisam

**innodb**

```
Transaction-safe한 Storage Engine이다.
```

**myisam**

```
Single-append, Multi-read 인 경우에 적합한 Storage Engine이다.
```

**myisam vs innodb**

![myisam vs innodb](http://idchowto.com/wp-content/uploads/2015/12/db-storage-engine1.png)

## 2-6. sequence, auto increment

**sequence**

```
unique한 값을 생성해주는 oracle 객체이다. 시퀀스를 생성하면 기본키와 같이 순차적으로 증가하는 컬럼을 자동적으로 생성 할 수 있다. 보통 PRIMARY KEY 값을 생성하기 위해 사용 한다.
```

**auto increment**

```
mysql에서 새 레코드가 테이블에 삽입 될 때 unique한 번호가 자동으로 생성 되도록 하는 기능이다. 보통 PRIMARY KEY 값을 생성하기 위해 사용 한다.
```

## 2-7. Limit

SELECT문에서 반환할 행의 수를 제한하는 절이다.

```mysql
SELECT * FROM 테이블명 LIMIT 출력할 레코드의 시작 행 오프셋 값, 출력하고자 하는 레코드 개수;
```

## 2-8. lower_case_table_names

- 0 : 대소문자를 구별하는 OS 에서만 의미가 있고 Windows/Mac OS X 에는 적용되지 않는다. 테이블과 DB 생성 시 디스크에 저장되는 테이블과 데이타베이스의 이름을 대소문자를 구분해서 생성한다. 참조 시에도 대소문자를 구분해서 사용해야 한다.
- 1 : 테이블과 DB 이름을 소문자로 생성하며 참조시에는 소문자로 변경하여 처리한다. 기존에 대문자가 포함되어 생성한 테이블과 DB 는 문제가 될 수 있다.
- 2 : 대소문자를 구분하지 않는 파일 시스템을 가진 OS(Mac OS X) 에서만 동작한다. 테이블과 DB 생성 시 디스크에 저장되는 테이블과 데이타베이스의 이름을 대소문자를 구분해서 생성한다. 참조 시에는 소문자로 변경한다.

C:\ProgramData\MySQL\MySQL Server 8.0\my.ini 파일을 수정한다.

```
[mysqld]
lower_case_table_names = 1
```

## 2-9. explain

쿼리를 성능 분석하는 도구로 MySQL이 쿼리에서 시간을 보내는 위치와 그 이유를 보여준다. 쿼리를 계획하고, 계측하고, 실행 계획의 다양한 지점에서 소요되는 시간을 측정하고 행을 계산하는 동안 쿼리를 실행한다. 실행이 완료되면 쿼리 결과 대신 계획 및 측정 값을 출력한다.

## 2-10. mysql query cache

최근에 실행된 SELECT 명령문 텍스트를 클라이언트에 보내는 결과와 함께 저장하는 기능이다. 만약에 동일한 명령문이 나중에 전달되면, 서버는 그 명령문을 다시 분석 (parsing)하고 실행하는 대신에 쿼리 캐시에서 그 결과 값을 추출한다.

## 2-11. MYSQL GROUP BY 사용 시 주의점 

GROUP BY를 사용하는 경우, SELECT할 수 있는 컬럼은 GROUP BY에 나열된 컬럼과 집계 함수로 한정된다. sql_mode의 값을 “ONLY_FULL_GROUP_BY”로 변경하면 잘못된 GROUP BY를 사용하는 것을 방지할 수 있다.

```mysql
SET sql_mode = 'ONLY_FULL_GROUP_BY';
```



# 3. naming Convention - 이름 관습

## 3-1. java, spring

3-1-1. package

- 패키지 이름의 최상위 레벨은 항상 ASCII 문자에 포함되어 있는 소문자로 쓰고, 가장 높은 레벨의 도메인 이름 중 하나이어야 한다.
- 현재는 com, edu, gov, mil, net, org, 또는 1981년 ISO Standard 316에 명시된 영어 두 문자로 표현되는 나라 구별 코드가 사용된다.
- 패키지 이름의 나머지 부분은 조직 내부의 명명 규칙을 따르면 된다. 이러한 규칙을 따라 만들어진 이름은 디렉토리 구조에서 디렉토리 이름으로도 사용된다.

3-1-2. class, interface

- 모든 Java class는 영문 대소문자를 혼용할 수 있지만, 반드시 명사를 사용하고 시작 글자를 대문자로 지정하며 camel case에 준하여 작성한다.
- framework에서 정의하는 요소에 대한 구분으로 해당 java class의 성격을 나타내는 postfix가 포함되어 있어야 한다. (ex. postfix : Controller, Wrapper, Service, ServiceImpl, Cmd, DAO, VO, Test 등)

3-1-3. method

- 메소드의 이름은 대소문자를 혼용할 수 있지만 반드시 동사를 사용하며 소문자로 시작한다.

- 이후 용어의 첫 글자만 대문자를 사용하며 숫자 및 특수문자는 사용하지 않는다.

- **method에서 사용하는 동사**

  | 구분                                           | 유형           | 동사     | 비고                        |
  | ---------------------------------------------- | -------------- | -------- | --------------------------- |
  | business 처리 관련                             | 내용검증       | validate |                             |
  |                                                | 조건확인       | check    |                             |
  |                                                | 검색           | search   |                             |
  |                                                | 연계           | contact  |                             |
  |                                                | action         | action   |                             |
  |                                                | 파일관리-읽기  | read     |                             |
  |                                                | 파일관리-쓰기  | write    |                             |
  | data 처리 관련(Controller, Business, DAO 공통) | 등록           | insert   |                             |
  |                                                | 조회(단건)     | select   |                             |
  |                                                | 조회(멀티건)   | select   | postfix로 List를 사용       |
  |                                                | 수정           | update   |                             |
  |                                                | 삭제           | delete   |                             |
  |                                                | 등록/수정      | merge    |                             |
  |                                                | 등록/수정/삭제 | multi    | 작업을 동시에 수행하는 경우 |
  | Value Object(model)                            | 값읽기         | get      |                             |
  |                                                | 값설정         | set      |                             |

3-1-4. 변수 및 상수

- 첫 글자는 소문자를 사용하며 이후 용어의 첫 글자만 대문자를 사용하며 숫자 및 특수문자는 사용하지 않는다.
- loop index에서 사용하는 변수는 i, j, k, l, x, y, z 등을 (관용적으로) 사용할 수 있다.
- 일반 변수는 _ 또는 $ 사용을 하지 않는다. 단, 데이터베이스의 속성명을 그대로 사용하는 경우에는 _ 사용을 허용
- 상수(Static Final 변수)는 용어사전을 사용하여 대문자로만 작성하며 단어 사이는 _를 사용하여 구분한다. 단, SUCCESS=1, FAIL=0으로 정의한다.

## 3-2. html, css, js

3-2-1. html

- html 파일의 이름은 첫 글자만 대문자로 한다.

3-2-2. css

- css 파일의 이름은 소문자로 시작한다.

3-2-3. jsp

- jsp 파일의 이름은 첫 글자만 대문자로 한다.

- postfix를 제외하고는 가능한 full name을 활용하도록 한다.

- **postfix 명명규칙**

  | Postfix명 | 설명 | 적용 예             |
  | --------- | ---- | ------------------- |
  | List      | 목록 | ChangeRequestList   |
  | Regist    | 등록 | ChangeRequestRegist |
  | Detail    | 상세 | ChangeRequestDetail |
  | Updt      | 수정 | ChangeRequestUpdt   |
  | Popup     | 팝업 | ChangeRequestPopup  |
  | Search    | 조회 | ChangeRequestSearch |

- 변수명은 소문자만 사용하며 단어 조합 시에는 _를 사용하여 구분한다.

- **각 컨트롤의 변수명에 대한 명명규칙**

  | 컨트롤   | Prefix명 | 적용 예                            |
  | -------- | -------- | ---------------------------------- |
  | 버튼     | btn      | 회원등록버튼 --> btnRegiUsr        |
  | 이미지   | img      | 검색버튼 --> imgSearch             |
  | Text     | txt      | 사용자이름 Input --> txtName       |
  | TextArea | txa      | 내용 Textarea --> txaContent       |
  | Select   | sel      | Select에서 옵션선택 --> selOption1 |
  | ListBox  | lst      | List에서 메뉴선택 --> lstMenu01    |
  | Radio    | rdo      | Radio에서 타입선택 --> rdoTypeA    |
  | CheckBox | chk      | 체크박스로 옵션선택 --> chkOption1 |

3-2-4. js

- js 파일의 이름은 첫 글자만 대문자로 한다.
- function 이름은 class에서의 메소드명과 동일한 방법으로 부여한다.
- 변수명은 소문자로 시작하고 새로운 단어의 시작은 대문자를 사용한다.



# 4. HTML, Javascript 등

## 4-1. jQuery

HTML 요소에 대한 DOM(문서객체모델)과 이벤트 주도형 자바스크립트 언어 사이의 상호작요을 매우 쉽게 수행할 수 있도록 만들어진 오픈 소스 형태의 자바스크립트 라이브러리이다.

head 태그 사이에 추가하여 설치한다.

```jsp
<script src="https://code.jquery.com/jquery-3.4.1.min.js"></script>
```

## 4-2. Bootstrap

부트스트랩(Bootstrap)은 웹사이트를 쉽게 만들 수 있게 도와주는 HTML, CSS, JS 프레임워크이다. jQuery를 필요로 한다.

부트스트랩 CDN(콘텐츠 전송 네트워크) 링크들을 사용한다.

```jsp
<!-- 합쳐지고 최소화된 최신 CSS -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/css/bootstrap.min.css">

<!-- 부가적인 테마 -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/css/bootstrap-theme.min.css">

<!-- 합쳐지고 최소화된 최신 자바스크립트 -->
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.2/js/bootstrap.min.js"></script>
```

## 4-3. Cache control

브라우저 캐싱 동작을 지시하는 HTTP 헤더이다. 요청과 응답 내의 캐싱 매커니즘을 위한 디렉티브를 정하기 위해 사용된다.

- no-cache : 캐시된 복사본을 사용자에게 보여주기 이전에, 재검증을 위한 요청을 원 서버로 보내도록 강제한다.

  **jsp no-cache 설정**

  ```jsp
  <%  
  response.setHeader("Cache-Control","no-store");  
  response.setHeader("Pragma","no-cache");  
  response.setDateHeader("Expires",0);  
  if (request.getProtocol().equals("HTTP/1.1"))
          response.setHeader("Cache-Control", "no-cache");
  %>
  ```

  **php no-cache 설정**

  ```php
  <?  
  header("Pragma: no-cache");  
  header("Cache-Control: no-cache,must-revalidate");  
  ?>
  ```

## 4-4. RESTFul/URL, URI 차이

**RESTFul**

```
웹 상의 자료를 HTTP위에서 SOAP이나 쿠키를 통한 세션 트랙킹 같은 별도의 전송 계층 없이 전송하기 위한 아주 간단한 인터페이스이다. 하나의 URI는 하나의 고유한 리소스를 대표하도록 설계된다는 개념에 전송방식을 결합해서 원하는 작업을 지정한다.
```

| URL             | URI                   |
| --------------- | --------------------- |
| Locator         | Identifier            |
| URI의 하위 개념 | URL과 URN의 상위 개념 |
| 자원의 위치     | 자원의 식별자         |

## 4-5. JSON/기본 개념/정의, 데이터 방식/Gson

**JSON**

```
데이터를 좀 더 쉽게 교환하고 저장하기 위하여 만들어진 텍스트 기반의 데이터 교환 표준이다. 자바스크립트의 객체 표기법에서 리터럴(literal)과 프로퍼티(property)를 표현하는 방법만 가져와서 사용한다.
```

> {
> "데이터이름":값,
> 	...
>
> "데이터이름":값
>
> }

**Gson**

```
JSON의 자바 오브젝트의 직렬화(자바 오브젝트 -> JSON), 역직렬화(JSON -> 자바 오브젝트)를 해주는 오픈 소스 자바 라이브러리이다.
```

pom.xml에 추가하여 설치한다.

```
<!-- https://mvnrepository.com/artifact/com.google.code.gson/gson -->
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
    <version>2.8.6</version>
</dependency>
```

## 4-6. Ajax/기본 자바스크립트/jQuery

**Ajax**

```
Asynchronous JavaScript and XML의 줄임말로 자바스크립트를 이용해서 비동기적으로 서버와 브라우저가 데이터를 교환할 수 있는 통신 방식
```

JavaScript Ajax

- JavaScript Ajax구현에 있어서 XMLHttpRequest객체(이하 XHR)는 반드시 필요한 객체이다.
- XHR을 쓰지 않고 IE에서 지원해주는 ActiveXObject를 사용한다.
- 텍스트 또는 XML타입으로만 데이터를 가져올 수 있다.

jQuery Ajax

- 보다 다양하고 단순한 방법으로 JavaScript Ajax의 구현을 할 수 있게 해준다.
- 순수 JavaScript로 Ajax를 구현 하는 것보다 좀 더 명시적으로 코드를 작성할 수 있다는 장점도 있다.

## 4-7. form태그의 enctype 속성

form 태그의 enctype 속성은 폼 데이터(form data)가 서버로 제출될 때 해당 데이터가 인코딩되는 방법을 명시한다. 이 속성은 form 요소의 method 속성값이 “post”인 경우에만 사용할 수 있다.

| 속성값                            | 설명                                               |
| --------------------------------- | -------------------------------------------------- |
| application/x-www-form-urlencoded | (기본값) 모든 문자 인코딩                          |
| multipart/form-data               | 인코딩 안함. 파일 업로드시 사용                    |
| text/plain                        | 공백은 + 기호로 변환하지만, 특수문자는 인코딩 안함 |

## 4-8. Log4j의 정의, 개념, 설정, 사용법

Log for Java의 줄임말로 프로그램을 작성하는 도중에 로그를 남기기 위해 사용되는 자바 기반 로깅 유틸리티이다.

1. pom.xml에 추가하여 설정한다.

   ```
   <!-- https://mvnrepository.com/artifact/log4j/log4j -->
   <dependency>
       <groupId>log4j</groupId>
       <artifactId>log4j</artifactId>
       <version>1.2.17</version>
   </dependency>
   ```

2. src/main/resources에 log4j.xml 파일을 생성한다.

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <!DOCTYPE log4j:configuration PUBLIC "-//APACHE//DTD LOG4J 1.2//EN" "log4j.dtd">
   <log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/">
       <!-- Appenders -->
       <appender name="console" class="org.apache.log4j.ConsoleAppender">
           <param name="Target" value="System.out" />
           <layout class="org.apache.log4j.PatternLayout">
               <param name="ConversionPattern" value="%-5p: %c - %m%n" />
           </layout>
       </appender>
       <!-- Application Loggers -->
       <logger name="com.mycompany.sd">
           <level value="info" />
       </logger>
       <!-- 3rdparty Loggers -->
       <logger name="org.springframework.core">
           <level value="info" />
       </logger>
       <logger name="org.springframework.beans">
           <level value="info" />
       </logger>
       <logger name="org.springframework.context">
           <level value="info" />
       </logger>
       <logger name="org.springframework.web">
           <level value="info" />
       </logger>
       <!-- Root Logger -->
       <root>
           <priority value="warn" />
           <appender-ref ref="console" />
       </root>
   </log4j:configuration>
   ```

3. web.xml을 수정한다.

   ```
       <context-param>
           <param-name>log4jConfigLocation</param-name>
           <param-value>
               classpath:project/config/log4j.xml
           </param-value>
       </context-param>
    
       <!-- Log4j -->
       <listener>
           <listener-class>
               org.springframework.web.util.Log4jConfigListener
           </listener-class>
       </listener>
   ```

- Logger : 로그 기록하고 Appender에 전달
- Appendar : 로그를 파일, 콘솔, DB 등의 위치에 출력
- Layout : 로그 출력 형식을 결정



# 5. Java, JDBC, Connection Pool

## 5-1. Lombok

자바 컴파일 시점에서 특정 어노테이션으로 해당 코드를 추가할 수 있는 라이브러리이다. 클래스 안에 있는 필드에 대해 Getter, Setter의 생성이나, toString(), equals(), hashCode() 메서드, 생성자를 자동으로 생성 해준다.

1. https://projectlombok.org/download에서 다운로드한다.

2. pom.xml에 추가하여 설정한다.

   ```
   <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
   <dependency>
       <groupId>org.projectlombok</groupId>
       <artifactId>lombok</artifactId>
       <version>1.18.8</version>
       <scope>provided</scope>
   </dependency>
   ```

3. lombok.jar가 다운로드된 경로로 가서  shift+우클릭 -> 여기에 PowerShell 창 열기 클릭 -> cmd 입력하면 cmd 창이 뜬다.

   ```
   java -jar lombok.jar
   ```

4. Installer 화면이 나오면 IDEs에 연결된 eclipse나 sts가 보인다. 보이지 않으면 Specify location... 클릭 -> Eclipse는 eclipse.exe STS는 sts.exe 선택 -> Install / Update 클릭

5. eclipse를 재시작

주의사항

- Setter는 객체의 안전성이 보장받기 힘들고, 양방향 연관관계시 ToString으로 인한 순환 참조 문제가 있기 때문에 @Setter, @Data 사용을 지양한다.
- @NoArgsConstructor 접근 권한을 최소화한다.
- @Builder 사용시 매개변수를 최소화한다.

## 5-2. Java - JDBC

Java Database Connectivity의 약자로서 자바에서 데이터베이스에 접속할 수 있도록 하는 자바 API이다. JDBC는 데이터베이스에서 자료를 쿼리하거나 업데이트하는 방법을 제공한다.

## 5-3. JAVA JDBC를 사용하여 MySQL과 연동

JDBC API를 사용하면 DBMS에 알맞은 JDBC 드라이버만 있으면 어떤 데이터베이스라도 사용할 수 있다.

MySQL JDBC 드라이버 설정

1. 프로젝트 우클릭 -> Build Path -> Conﬁgure Build Path... -> Libraries -> Add External JARs...
2. C:\Program Files (x86)\MySQL\Connector J 8.0\mysql-connector-java.jar 파일을 적용한다.

JDBC 프로그램의 실행 순서

1. JDBC 드라이버 로딩
2. 데이터베이스 커넥션 구함
3. 쿼리 실행을 위한 Statement 객체 생성
4. 쿼리 실행
5. 쿼리 실행 결과 사용
6. Statement 종료
7. 데이터베이스 커넥션 종료

## 5-4. Commons DBCP

대표적인 오픈소스 커넥션 풀 라이브러리이다.

사용법

1. pom.xml에 추가하여 설정한다.

   ```
   <!-- https://mvnrepository.com/artifact/commons-dbcp/commons-dbcp -->
   <dependency>
       <groupId>commons-dbcp</groupId>
       <artifactId>commons-dbcp</artifactId>
       <version>1.4</version>
   </dependency>
   ```

2. root-context.xml을 수정한다.

   ```
   <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource"  
       destroy-method="close"
       p:driverClassName="${db.driverClassName }"
       p:url="${db.url}"
       p:username="${db.username}"
       p:password="${db.password}"
       p:maxActive="${db.maxActive}"
       p:maxIdle="${db.maxIdle}"
       p:maxWait="${db.maxWait}"
   />
   ```

## 5-5. DBCP 구현 - DB Connection Pooling

자체로 DBCP 구현

1. DBManager 클래스를 구현한다.

   > https://gompangs.tistory.com/entry/DB-DBCP-%EA%B5%AC%ED%98%84-DB-Connection-Pooling

2. getConnection()으로 Connection을 받아온다.

3. Connection에 PSMT나 STMT를 사용해서 쿼리를 실행한다.(PSMT는 캐싱을 하므로 동일 쿼리 수행 시 STMT보다 성능이 훨씬 좋다.)

4. 해당 connection을 freeConnection()한다.

## 5-6. hikariCP

최근 유행하는 매우 빠른 경량 오픈소스 커넥션 풀 라이브러리이다.

사용법

1. pom.xml에 추가하여 설정한다.

   ```
   <!-- https://mvnrepository.com/artifact/com.zaxxer/HikariCP -->
   <dependency>
       <groupId>com.zaxxer</groupId>
       <artifactId>HikariCP</artifactId>
       <version>3.3.1</version>
   </dependency>
   ```

2. root-context.xml을 수정한다.

   ```
   <bean id="hikariConfig" class="com.zaxxer.hikari.HikariConfig">
   		<property name="driverClassName"
   			value="net.sf.log4jdbc.sql.jdbcapi.DriverSpy"></property>
   		<property name="jdbcUrl"
   			value="jdbc:log4jdbc:mysql://localhost:3306/스키마네임?characterEncoding=UTF-8&amp;serverTimezone=Asia/Seoul"></property>
   		<property name="username" value="유저네임"></property>
   		<property name="password" value="패스워드"></property>
   </bean>
   <!-- HikariCP configuration -->
   <bean id="dataSource" class="com.zaxxer.hikari.HikariDataSource"
   		destroy-method="close">
   		<constructor-arg ref="hikariConfig" />
   </bean>
   ```

## 5-7. 전자정부 페이징

5-7-1. 설정

1. pom.xml에 추가하여 설정한다.

   ```
   <repositories>
           <repository>
               <id>egovframe</id>
               <url>http://maven.egovframe.kr:8080/maven/</url>
               <releases>
               <enabled>true</enabled>
               </releases>
               <snapshots>
               <enabled>false</enabled>
               </snapshots>
           </repository>
   </repositories>
   <dependencies> 
           <dependency>
               <groupId>egovframework.rte</groupId>
               <artifactId>egovframework.rte.ptl.mvc</artifactId>
               <version>2.7.0</version>
           </dependency>
   </dependencies>
   ```

2. context-common.xml을 수정

   ```
   <bean id="textRenderer" class="egovframework.rte.ptl.mvc.tags.ui.pagination.DefaultPaginationRenderer"/>  
   <bean id="paginationManager" class="egovframework.rte.ptl.mvc.tags.ui.pagination.DefaultPaginationManager">
       <property name="rendererType">
           <map>
               <entry key="text" value-ref="textRenderer"/>
           </map>
       </property>
   </bean>
   ```

5-7-2. 영속 계층

1. sample_SQL.xml을 수정

   ```
   <select id="sample.selectBoardList" resultType="hashmap" parameterType="hashmap" >
      <![CDATA[
          SELECT
              (
                  SELECT
                      COUNT(*) 
                  FROM 
                      TB_BOARD
                  WHERE 
                      DEL_GB = 'N'
              ) AS TOTAL_COUNT ,
              IDX,
              TITLE,
              HIT_CNT,
              CREA_DTM
          FROM
              TB_BOARD
          WHERE
              DEL_GB= 'N'
          ORDER BY 
              IDX DESC
          LIMIT #{START} , #{END} 
      ]]>
   </select>
   ```

2. AbstractDAO를 수정

   ```java
   @SuppressWarnings({ "rawtypes", "unchecked" })
   public Map selectPagingList(String queryId, Object params){
       printQueryId(queryId);
         
       Map<String,Object> map = (Map<String,Object>)params;
       PaginationInfo paginationInfo = null;
         
       if(map.containsKey("currentPageNo") == false || StringUtils.isEmpty(map.get("currentPageNo")) == true)
           map.put("currentPageNo","1");
         
       paginationInfo = new PaginationInfo();
       paginationInfo.setCurrentPageNo(Integer.parseInt(map.get("currentPageNo").toString()));
       if(map.containsKey("PAGE_ROW") == false || StringUtils.isEmpty(map.get("PAGE_ROW")) == true){
           paginationInfo.setRecordCountPerPage(15);
       }
       else{
           paginationInfo.setRecordCountPerPage(Integer.parseInt(map.get("PAGE_ROW").toString()));
       }
       paginationInfo.setPageSize(10);
    
       int start = paginationInfo.getFirstRecordIndex();
       int end = paginationInfo.getRecordCountPerPage();
       map.put("START",start);
       map.put("END",end);
         
       params = map;
        
       Map<String,Object> returnMap = new HashMap<String,Object>();
       List<Map<String,Object>> list = sqlSession.selectList(queryId,params);
         
       if(list.size() == 0){
           map = new HashMap<String,Object>();
           map.put("TOTAL_COUNT",0); 
           list.add(map);
             
           if(paginationInfo != null){
               paginationInfo.setTotalRecordCount(0);
               returnMap.put("paginationInfo", paginationInfo);
           }
       }
       else{
           if(paginationInfo != null){
               paginationInfo.setTotalRecordCount(Integer.parseInt(list.get(0).get("TOTAL_COUNT").toString()));
    
               returnMap.put("paginationInfo", paginationInfo);
           }
       }
       returnMap.put("result", list);
       return returnMap;
   }
   ```

5-7-3. 화면 처리

1. 태그 라이브러리를 추가

   ```jsp
   <%@ taglib prefix="ui" uri="http://egovframework.gov/ctl/ui" %>
   ```

2. boardList.jsp를 수정

5-7-4. 프레젠테이션 계층

1. SampleController를 수정

   ```java
   @RequestMapping(value="/sample/openBoardList.do")
   public ModelAndView openBoardList(CommandMap commandMap) throws Exception{
       ModelAndView mv = new ModelAndView("/sample/boardList");
       
       Map<String,Object> map = sampleService.selectBoardList(commandMap.getMap());
       
       mv.addObject("paginationInfo", (PaginationInfo)map.get("paginationInfo"));
       mv.addObject("list", map.get("result"));
       
       return mv;
   }
   ```

5-7-5. 비즈니스 계층

1. SampleService를 수정

   ```java
   Map<String, Object> selectBoardList(Map<String, Object> map) throws Exception;
   ```

2. SampleServiceImpl을 수정

   ```java
   @Override
   public Map<String,Object> selectBoardList(Map<String, Object> map) throws Exception {
       return sampleDAO.selectBoardList(map);
   }
   ```

5-7-6. 영속 계층

1. SampleDAO를 수정

   ```
   @SuppressWarnings("unchecked")
   public Map<String,Object> selectBoardList(Map<String,Object> map) throws Exception{
       return (Map<String,Object>)selectPagingList("sample.selectBoardList",map);
   }
   ```

## 5-8. URL Encode - Decode

**URL Encode**

```
URL에 사용할 수 없는 문자를 인코딩하는 것을 말한다.
```

> URL에 사용할 수 있는 문자는 알파벳, 숫자와 몇 가지의 특수문자뿐이다. 따라서 한글 등의 다양한 문자를 URL에 표시하려면 URL에 허용하는 문자로 변환하여 표현하여야 한다. URL 메타문자들에 대한 인코딩이 필요하며 형식은 기존 문자열의 HEX값 앞에 %를 사용한다. 한글은 UTF-8을 사용한다.

HTML 형식을 encode하기 위한 유틸리티 클래스 URLEncoder를 사용한다.

```java
URLEncoder.encode("테스트", "UTF-8");
```

**URL Decode**

```
URL 인코딩한 문자열을 원래 문자열로 복원하는 것을 말한다.
```

HTML 형식을 decode하기 위한 유틸리티 클래스 URLDecoder를 사용한다.

```java
URLDecoder.decode("%ED%85%8C%EC%8A%A4%ED%8A%B8", "UTF-8");
```

## 5-9. Spring 어노테이션 정리

| 어노테이션        | 설명                                                         | 사용             |
| ----------------- | ------------------------------------------------------------ | ---------------- |
| @Controller       | 스프링 MVC의 컨트롤러 객체임을 명시                          | 클래스           |
| @RequestMapping   | 특정 URI에 매칭되는 클래스나 메소드임을 명시                 | 클래스, 메소드   |
| @RequestParam     | 요청에서 특정한 파라미터 값을 찾아낼 때 사용                 | 파라미터         |
| @RequestHeader    | 요청에서 특정 HTTP헤더 정보를 추출할 때 사용                 | 파라미터         |
| @PathVariable     | 현재의 URI에서 원하는 정보를 추출할 때 사용                  | 파라미터         |
| @CookieValue      | 현재 사용자의 쿠키가 존재하는 경우 쿠키의 이름을 이용해서 쿠키의 값을 추출 | 파라미터         |
| @ModelAttribute   | 자동으로 해당 객체를 뷰까지 전달하도록 만듬                  | 메소드, 파라미터 |
| @InitBinder       | 파라미터를 수집해서 객체로 만들 경우에 커스터마이징          | 메소드           |
| @ResponseBody     | 리턴 타입이 HTTP의 응답 메시지로 전송                        | 메소드, 리턴타입 |
| @RequestBody      | 요청 문자열이 그대로 파라미터로 전달                         | 파라미터         |
| @Repository       | DAO 객체                                                     | 클래스           |
| @Service          | 서비스 객체                                                  | 클래스           |
| @SessionAttribute | 세션상에서 모델의 정보를 유지하고 싶은 경우에 사용           | 클래스           |

## 5-10. Connection Pool

데이터베이스와 연결된 커넥션을 미리 만들어서 풀(pool) 속에 저장해 두고 있다가 필요할 때에 커넥션을 풀에서 가져다 쓰고 다시 풀에 반환하는 기법이다.

![커넥션 풀 기법](http://www.cubrid.com/files/attach/images/7900/753/822/003/227062f2c1c6a965bea274420c01819f.PNG)



# 6. 보안 관련

## 6-1. XSS(Cross Site Scripting) 공격

공격자가 웹 양식 또는 웹 앱 URL에 악성코드를 주입해 애플리케이션이 본래 애플리케이션의 의도와 다른 특정 작업을 실행하도록 유도하는 것이다.

보안 대책

- 외부입력값에 스크립트가 삽입되지 못하도록 문자변환 함수 또는 메서드를 사용하여 < > & “ 등을 < > & " 로 치환
- HTML태그를 허용하는 게시판에서는 허용되는 HTML 태그들을 화이트리스트로 만들어 해당 태그만 지원하도록 한다.

## 6-2. SQL Inject

응용 프로그램 보안 상의 허점을 의도적으로 이용해, 악의적인 SQL문을 실행되게 함으로써 데이터베이스를 비정상적으로 조작하는 코드 인젝션 공격 방법이다.

보안 대책

- SQL에 프로그래밍 방식으로 집어넣게 되는 값들에서 특수문자를 날려버리거나 따로 텍스트 인코딩을 수행한다.

## 6-3. prepare statement

prepare 문에서, sql 문을 실행하지 않은채 준비만 해놓고 execute 문에서, 나머지 중요 문자열을 변수 처리하면서 넘기면, 나중에 실행하는 것을 말한다. 일명, 동적 SQL 문이라고도 한다. (prepare 문 내에, ? 기호로 추후 입력될 값을 비워 놓게 된다.)

## 6-4. #{}, ${} 차이

| \#{}                                                         | ${}                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Parameter가 String 형태로 들어와 자동적으로 'Parameter' 형태가 된다. | Parameter가 바로 출력된다.                                   |
| 예를들어, VO에 담긴 id값이 getter로 반환될 때, id값이 123이라면 mybatis 쿼리에는 id='123'의 형태가 된다. | 예를 들어, VO에 담긴 id값이 getter로 반환될 때, id값이 123이라면 mybatis 쿼리에는 id=123의 형태가 된다. |
| SQL Injection을 예방할 수 있어 보안측면에서 유리하다.        | SQL Injection을 예방할 수 없어 보안측면에서 불리하다.        |

## 6-5. xml 사용이유

XML은 데이터를 텍스트 형식으로 저장하므로, 소프트웨어나 하드웨어에 독립적으로 데이터를 저장하고 전달할 수 있다. 따라서 XML을 사용하면 새로운 운영체제나 프로그램, 브라우저 등에 상관없이 데이터를 안전하고 손쉽게 전달할 수 있다.

> http://tcpschool.com/xml/intro

## 6-6. CSRF

웹사이트 취약점 공격의 하나로, 사용자가 자신의 의지와는 무관하게 공격자가 의도한 행위(수정, 삭제, 등록 등)를 특정 웹사이트에 요청하게 하는 공격을 말한다.

보안 대책

- 리퍼러(Referer) 체크
- 시큐리티 토큰(Security Token) 사용
- 더블 서밋 쿠키(Double Submit Cookie) 검증

## 6-7. OWASP Top 10

Open Web Application Security Project(오픈소스 웹 애플리케이션 보안 프로젝트) 에서 4년에 한번씩 발표하는 웹 취약점 Top 10이다.

**OWASP Top 10 - 2017**

| No   | 취약점                             |
| ---- | ---------------------------------- |
| 1    | 인젝션                             |
| 2    | 취약한 인증                        |
| 3    | 민감한 데이터 노출                 |
| 4    | XML 외부 개체(XXE)                 |
| 5    | 취약한 접근 통제                   |
| 6    | 잘못된 보안 구성                   |
| 7    | 크로스 사이트 스크립팅(XSS)        |
| 8    | 안전하지 않은 역직렬화             |
| 9    | 알려진 취약점이 있는 구성요소 사용 |
| 10   | 불충분한 로깅 및 모니터링          |



# 7. Cookie와 세션

## 7-1. Cookie와 세션

**Cookie**

- 쿠키는 클라이언트 **로컬에 저장**되는 **키와 값**이 들어있는 작은 데이터 **파일**이다.

- 쿠키에는 이름, 값, 만료날짜(쿠키 저장기간), 경로 정보가 들어있다.

- 쿠키는 일정시간동안 데이터를 저장할 수 있다. (로그인 상태 유지에 활용)

- 쿠키는 클라이언트의 상태 정보를 로컬에 저장했다가 참조한다.

- 쿠키 프로세스

  1. 브라우저에서 웹페이지 접속
  2. 클라이언트가 요청한 웹페이지를 받으면서 쿠키를 클라이언트 로컬(하드)에 저장
  3. 클라이언트가 재 요청시 웹페이지 요청과 함께 쿠키값도 전송
  4. 지속적으로 로그인 정보를 가지고 있는 것처럼 사용

- 쿠키 사용 사례

  자동 로그인, 팝업에서 "오늘 더 이상 이 창을 보지 않음" 체크, 쇼핑몰의 장바구니

- Response Header에 Set-Cookie 속성을 사용하면 클라이언트에 쿠키를 만들 수 있다.

- 쿠키는 사용자가 따로 요청하지 않아도 브라우저가 Request시에 Request Header를 넣어서 **자동으로 서버에 전송**한다.

**세션(Session)**

- **일정 시간동안** **같은 브라우저로 부터** 들어오는 일련의 요구를 하나의 상태로 보고 그 **상태를 유지하는 기술**

- 즉, 웹 브라우저를 통해 웹 서버에 접속한 이후로 브라우저를 종료할 때 까지 유지되는 상태

- 클라이언트가 Request를 보내면, 해당 서버의 엔진이 클라이언트에게 유일한 ID를 부여하는 데 이것이 세션ID다.

- 세션 사용 사례

  로그인 정보 유지

## 7-2. Servlet 세션

![세션 이용 방법](https://k.kakaocdn.net/dn/lwz3v/btqxHUonNmI/0DKKqXbko84pYe2WbLbqm1/img.png)

1. 웹 클라이언트가 서버측에 요청을 보내게 되면 서버는 클라이언트를 식별하는 session id를 생성한다.
2. 서버는 session id를 이용해서 key와 value를 이용한 저장소인 HttpSession을 생성한다.
3. 서버는 session id를 저장하고 있는 쿠키를 생성하여 클라이언트에 전송한다.
4. 클라이언트는 서버측에 요청을 보낼때 session id를 가지고 있는 쿠키를 전송한다.
5. 서버는 쿠키에 있는 session id를 이용해서 그 전 요청에서 생성한 HttpSession을 찾고 사용한다.

**세션 메소드들**

| 메소드 이름                             | 리턴 타입             | 설명                                                         |
| --------------------------------------- | --------------------- | ------------------------------------------------------------ |
| getAttribute(String name)               | java.lang.Object      | 세션 속성명이 name인 속성의 값을 Object 타입으로 리턴한다. 해당 되는 속성명이 없을 경우에는 null 값을 리턴한다. |
| getAttributeNames()                     | java.util.Enumeration | 세션 속성의 이름들을 Enumeration 객체 타입으로 리턴한다.     |
| getCreationTime()                       | long                  | 1970년 1월 1일 0시 0초를 기준으로 하여 현재 세션이 생성된 시간까지 경과한 시간을 계산하여 1/1000초 값으로 리턴한다. |
| getId()                                 | java.lang.String      | 세션에 할당된 고유 식별자를 String 타입으로 리턴한다.        |
| getMaxInactiveInterval()                | int                   | 현재 생성된 세션을 유지하기 위해 설정된 세션 유지시간을 int형으로 리턴한다. |
| invalidate()                            | void                  | 현재 생성된 세션을 무효화 시킨다.                            |
| removeAttribute(String.name)            | void                  | 세션 속성명이 name인 속성을 제거한다.                        |
| setAttribute(String name, Object value) | void                  | 세션 속성명이 name인 속성에 속성값으로 value를 할당한다.     |
| setMaxInactiveInterval(int interval)    | void                  | 세션을 유지하기 위한 세션 유지시간을 초 단위로 설정한다.     |

## 7-3. Authentication, Authorization

**Authentication**

```
자신이 누구라고 주장하는 사람을 확인하는 절차이다. 대표적인 것이 ID/PW, 공인인증서, 2-factor 인증 등이다.
```

**Authorization**

```
가고 싶은 곳으로 가도록 혹은 원하는 정보를 얻도록 허용하는 과정이다. 대표적인 것이 접근제어 등이다.
```

## 7-4. 세션을 이용한 로그인, 로그아웃 처리

1. MemberVO 클래스를 추가

   ```
   @Data
   public class MemberVO {
       private String userId;
       private String userPw;
       private String userName; 
       private String userEmail; 
       private Date userRegdate; // java.sql.Date
       private Date userUpdatedate;
   }
   ```

2. MemberController 클래스를 추가

   ```
   @Controller // 현재 클래스를 스프링에서 관리하는 컨트롤러 bean으로 생성
   @RequestMapping("/member/*") // 모든맵핑은 /member/를 상속
   public class MemberController {
       // 로깅을 위한 변수
       private static final Logger logger = LoggerFactory.getLogger(MemberController.class);
       
       @Inject
       MemberService memberService;
       
       // 01. 로그인 화면 
       @RequestMapping("login.do")
       public String login(){
           return "member/login";    // views/member/login.jsp로 포워드
       }
       
       // 02. 로그인 처리
       @RequestMapping("loginCheck.do")
       public ModelAndView loginCheck(@ModelAttribute MemberVO vo, HttpSession session){
           boolean result = memberService.loginCheck(vo, session);
           ModelAndView mav = new ModelAndView();
           if (result == true) { // 로그인 성공
               // main.jsp로 이동
               mav.setViewName("home");
               mav.addObject("msg", "success");
           } else {    // 로그인 실패
               // login.jsp로 이동
               mav.setViewName("member/login");
               mav.addObject("msg", "failure");
           }
           return mav;
       }
       
       // 03. 로그아웃 처리
       @RequestMapping("logout.do")
       public ModelAndView logout(HttpSession session){
           memberService.logout(session);
           ModelAndView mav = new ModelAndView();
           mav.setViewName("member/login");
           mav.addObject("msg", "logout");
           return mav;
       }
   }
   ```

3. MemberService 인터페이스를 추가

   ```
   public interface MemberService {
       // 01_01. 회원 로그인 체크
       public boolean loginCheck(MemberVO vo, HttpSession session);
       // 01_02. 회원 로그인 정보
       public MemberVO viewMember(MemberVO vo);
       // 02. 회원 로그아웃
       public void logout(HttpSession session);
   }
   ```

4. MemberServiceImpl 클래스를 추가

   ```
   @Service // 현재 클래스를 스프링에서 관리하는 service bean으로 등록
   public class MemberServiceImpl implements MemberService {
       
       @Inject
       MemberDAO memberDao;
       
       // 01_01. 회원 로그인체크
       @Override
       public boolean loginCheck(MemberVO vo, HttpSession session) {
           boolean result = memberDao.loginCheck(vo);
           if (result) { // true일 경우 세션에 등록
               MemberVO vo2 = viewMember(vo);
               // 세션 변수 등록
               session.setAttribute("userId", vo2.getUserId());
               session.setAttribute("userName", vo2.getUserName());
           } 
           return result;
       }
       // 01_02. 회원 로그인 정보
       @Override
       public MemberVO viewMember(MemberVO vo) {
           return memberDao.viewMember(vo);
       }
       // 02. 회원 로그아웃
       @Override
       public void logout(HttpSession session) {
           // 세션 변수 개별 삭제
           // session.removeAttribute("userId");
           // 세션 정보를 초기화 시킴
           session.invalidate();
       }
   }
   ```

5. MemberDAO 인터페이스를 추가

   ```
   public interface MemberDAO {
       // 01_01. 회원 로그인 체크
       public boolean loginCheck(MemberVO vo);
       // 01_02. 회원 로그인 정보
       public MemberVO viewMember(MemberVO vo);
       // 02. 회원 로그아웃
       public void logout(HttpSession session);
   }
   ```

6. MemberDAOImpl 클래스를 추가

   ```
   @Repository // 현재 클래스를 스프링에서 관리하는 dao bean으로 등록
   public class MemberDAOImpl implements MemberDAO {
       // SqlSession 객체를 스프핑에서 생성하여 주입
       // 의존관계 주입(Dependency Injection), 느슨한 결합
       @Inject
       SqlSession sqlSession; // mybatis 실행 객체
       
       // 01_01. 회원 로그인체크
       @Override
       public boolean loginCheck(MemberVO vo) {
           String name = sqlSession.selectOne("member.loginCheck", vo);
           return (name == null) ? false : true;
       }
       // 01_02. 회원 로그인 정보
       @Override
       public MemberVO viewMember(MemberVO vo) {
           return sqlSession.selectOne("member.viewMember", vo);
       }
       // 02. 회원 로그아웃
       @Override
       public void logout(HttpSession sessin) {
       }
   }
   ```

7. memberMapper.xml 파일을 추가

   ```
   <!DOCTYPE mapper
   PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
   "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
    
   <!-- 다른 mapper와 중복되지 않도록 네임스페이스 기재 -->
   <mapper namespace="member">
       
       <select id="loginCheck" resultType="String">
           SELECT user_name AS userName FROM tbl_member
           WHERE user_id = #{userId} AND user_pw = #{userPw}
       </select>
       
       <select id="viewMember" resultType="com.example.spring02.model.member.dto.MemberVO">
           SELECT 
               user_name AS userName,
               user_id AS userId,
               user_email AS userEmail,
               user_regdate AS userRegdate
           FROM tbl_member
           WHERE user_id = #{userId} AND user_pw = #{userPw}
       </select>
    
   </mapper>
   ```

8. login.jsp 파일을 추가(로그인 페이지 : 로그인 성공, 실패, 로그아웃 메시지 알림)

9. home.jsp 파일을 추가(메인 페이지)

10. menu.jsp 파일을 추가(상단 로그인 상태 표시, 로그아웃 링크)

## 7-5. Mysql을 이용한 세션처리

Springboot에서 Session 정보를 Mysql DB에 연동하는 방법

1. pom.xml에 추가하여 설정한다.

   ```
   <dependency>
       <groupId>org.springframework.session</groupId>
       <artifactId>spring-session-jdbc</artifactId>
   </dependency>
   <dependency>
   <groupId>mysql</groupId>
       <artifactId>mysql-connector-java</artifactId>
       <version>5.1.6</version>
   </dependency>
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-jdbc</artifactId>
   </dependency>
   ```

2. application.properties 파일을 수정

   ```
   spring.session.store-type=jdbc
   server.compression.enabled=true
   server.use-forward-headers=true
   server.compression.mime-types=application/json,application/xml,text/html,text/xml,text/plain,text/css,application/javascript
   logging.file=logbook-server.log
   spring.datasource.url=jdbc:mysql:DB서버 IP/DB 이름
   spring.datasource.username=ID입력
   spring.datasource.password=PW입력
   spring.datasource.driver-class-name=com.mysql.jdbc.Driver
   
   # Number of ms to wait before throwing an exception if no connection is available.
   spring.datasource.tomcat.max-wait=10000
   
   # Maximum number of active connections that can be allocated from this pool at the same time.
   spring.datasource.tomcat.max-active=50
   
   # Validate the connection before borrowing it from the pool.
   spring.datasource.tomcat.test-on-borrow=true
   
   spring.jpa.hibernate.ddl-auto=create // 기존에 생성된 테이블들 삭제하고 새로 만드는 옵션
   ```

3. Mysql 관련 처리

   ```
   CREATE TABLE SPRING_SESSION (
       SESSION_ID CHAR(36),
       CREATION_TIME BIGINT NOT NULL,
       LAST_ACCESS_TIME BIGINT NOT NULL,
       MAX_INACTIVE_INTERVAL INT NOT NULL,
       PRINCIPAL_NAME VARCHAR(100),
       CONSTRAINT SPRING_SESSION_PK PRIMARY KEY (SESSION_ID)
   ) ENGINE=InnoDB;
   
   CREATE INDEX SPRING_SESSION_IX1 ON SPRING_SESSION (LAST_ACCESS_TIME);
   
   CREATE TABLE SPRING_SESSION_ATTRIBUTES (
       SESSION_ID CHAR(36),
       ATTRIBUTE_NAME VARCHAR(200),
       ATTRIBUTE_BYTES BLOB,
       CONSTRAINT SPRING_SESSION_ATTRIBUTES_PK PRIMARY KEY (SESSION_ID, ATTRIBUTE_NAME),
       CONSTRAINT SPRING_SESSION_ATTRIBUTES_FK FOREIGN KEY (SESSION_ID) REFERENCES SPRING_SESSION(SESSION_ID) ON DELETE CASCADE
   ) ENGINE=InnoDB;
   
   CREATE INDEX SPRING_SESSION_ATTRIBUTES_IX1 ON SPRING_SESSION_ATTRIBUTES (SESSION_ID);
   ```

4. Spring Session JDBC를 위한 설정 클래스를 추가

   ```
   @Configuration
   @EnableJdbcHttpSession
   public class HttpSessionConfig {
   }
   ```

   SpringBoot에서는 @EnableJdbcHttpSession 어노테이션을 @Configuration 어노테이션과 함께 작성해 주면 JDBC Session이 적용된다.
