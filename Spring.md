# 1. 스프링 MVC 프로젝트의 기본 설정

- JDK 1.8버전 설치
- Eclipse 설치
- Tomcat 9.0버전 설치
- Lombok 설치
- MySQL 설치
- JDBC Driver for MySQL (Connector/J) 설치

## 1-1. 프로젝트를 생성

New > Spring Legacy Project > Spring MVC Project

Project name을 지정

생성하는 프로젝트의 기본 패키지를 지정



## 1-2. pom.xml의 수정

1. Java 버전과 Springframework 버전 수정

   ```java
   <properties>
   <java-version>1.8</java-version>
   <org.springframework-version>5.0.7.RELEASE</org.springframework-version>
   <org.aspectj-version>1.6.10</org.aspectj-version>
   <org.slf4j-version>1.6.6</org.slf4j-version>
   </properties>
   ```

2. 라이브러리 추가

   ```java
   <!-- Spring Test -->
   <!-- https://mvnrepository.com/artifact/org.springframework/spring-test -->
   <dependency>
   <groupId>org.springframework</groupId>
   <artifactId>spring-test</artifactId>
   <version>${org.springframework-version}</version>
   <scope>test</scope>
   </dependency>
   <!-- Spring JDBC -->
   <!-- https://mvnrepository.com/artifact/org.springframework/spring-jdbc -->
   <dependency>
   <groupId>org.springframework</groupId>
   <artifactId>spring-jdbc</artifactId>
   <version>${org.springframework-version}</version>
   </dependency>
   <!-- Spring Transaction -->
   <!-- https://mvnrepository.com/artifact/org.springframework/spring-tx -->
   <dependency>
   <groupId>org.springframework</groupId>
   <artifactId>spring-tx</artifactId>
   <version>${org.springframework-version}</version>
   </dependency>
   <!-- HikariCP -->
   <!-- https://mvnrepository.com/artifact/com.zaxxer/HikariCP -->
   <dependency>
   <groupId>com.zaxxer</groupId>
   <artifactId>HikariCP</artifactId>
   <version>3.4.1</version>
   </dependency>
   <!-- MyBatis -->
   <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
   <dependency>
   <groupId>org.mybatis</groupId>
   <artifactId>mybatis</artifactId>
   <version>3.5.3</version>
   </dependency>
   <!-- MyBatis-Spring -->
   <!-- https://mvnrepository.com/artifact/org.mybatis/mybatis-spring -->
   <dependency>
   <groupId>org.mybatis</groupId>
   <artifactId>mybatis-spring</artifactId>
   <version>2.0.3</version>
   </dependency>
   <!-- log4jdbc -->
   <!-- https://mvnrepository.com/artifact/org.bgee.log4jdbc-log4j2/log4jdbclog4j2-jdbc4 -->
   <dependency>
   <groupId>org.bgee.log4jdbc-log4j2</groupId>
   <artifactId>log4jdbc-log4j2-jdbc4</artifactId>
   <version>1.16</version>
   </dependency>
   <!-- lombok -->
   <!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
   <dependency>
   <groupId>org.projectlombok</groupId>
   <artifactId>lombok</artifactId>
   <version>1.18.0</version>
   <scope>provided</scope>
   </dependency>
   <!-- MySQL 라이브러리 -->
   <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
   <dependency>
   <groupId>mysql</groupId>
   <artifactId>mysql-connector-java</artifactId>
   <version>8.0.15</version>
   </dependency>
   ```

3. Junit 버전 수정

   ```java
   <!-- Test -->
   <dependency>
   <groupId>junit</groupId>
   <artifactId>junit</artifactId>
   <version>4.12</version>
   <scope>test</scope>
   </dependency>
   ```

4. Servlet 아티팩트아이디와 버전 수정

   ```java
   <dependency>
   <groupId>javax.servlet</groupId>
   <artifactId>javax.servlet-api</artifactId>
   <version>3.1.0</version>
   <scope>provided</scope>
   </dependency>
   ```

5. Maven 관련 Java 버전을 1.8로 수정

   ```java
   <plugin>
   <groupId>org.apache.maven.plugins</groupId>
   <artifactId>maven-compiler-plugin</artifactId>
   <version>2.5.1</version>
   <configuration>
   <source>1.8</source>
   <target>1.8</target>
   <compilerArgument>-Xlint:all</compilerArgument>
   <showWarnings>true</showWarnings>
   <showDeprecation>true</showDeprecation>
   </configuration>
   </plugin>
   ```

6. 프로젝트를 선택하고 Maven > Update Project

7. 프로젝트를 선택하고 Build Path > Configure Build Path > Libraries > Add External JARs > mysql-connector-java.jar 파일을 추가



## 1-3. Mysql 관련 처리

1. root 계정으로 Mysql에 접속

2. DB 생성

   ```mysql
   CREATE DATABASE DB명;
   ```

3. 일반 사용자 추가

   ```mysql
   CREATE USER 'user명'@'localhost' IDENTIFIED BY '비밀번호';
   ```

4. DB 사용권한 부여

   ```mysql
   GRANT ALL PRIVILEGES ON DB명.* TO 'user명'@'localhost';
   ```

5. 적용

   ```mysql
   FLUSH PRIVILEGES;
   ```

6. 테이블 생성과 더미 데이터 생성

   ```mysql
   USE DB명;
   
   CREATE TABLE tbl_board (
     bno INT NOT NULL AUTO_INCREMENT,
     title VARCHAR(200) NOT NULL,
     content TEXT NOT NULL,
     writer VARCHAR(50) NOT NULL,
     regdate TIMESTAMP NOT NULL DEFAULT NOW(),
     updatedate TIMESTAMP NOT NULL DEFAULT NOW(),
     PRIMARY KEY (bno)
   );
   
   INSERT INTO tbl_board (title, content, writer) VALUES ('테스트 제목', '테스트 내용', 'user00');
   ```

   

## 1-4. 데이터베이스 관련 설정 및 테스트

1. root-context.xml 파일을 열고, 아래쪽의 'Namespaces' 항목에서 'mybatis-spring' 탭을 선택

2. root-context.xml의 수정

   ```java
   <bean id="hikariConfig" class="com.zaxxer.hikari.HikariConfig">
   <property name="driverClassName"
   value="net.sf.log4jdbc.sql.jdbcapi.DriverSpy"></property>
   <property name="jdbcUrl"
   value="jdbc:log4jdbc:mysql://localhost:3306/DB명?characterEncoding=UTF-8&amp;serverTimezone=Asia/Seoul"></property>
   <property name="username" value="user명"></property>
   <property name="password" value="비밀번호"></property>
   </bean>
   <!-- HikariCP configuration -->
   <bean id="dataSource" class="com.zaxxer.hikari.HikariDataSource"
   destroy-method="close">
   <constructor-arg ref="hikariConfig" />
   </bean>
   <!-- SQLSessionFactory -->
   <bean id="sqlSessionFactory"
   class="org.mybatis.spring.SqlSessionFactoryBean">
   <property name="dataSource" ref="dataSource"></property>
   </bean>
   <mybatis-spring:scan base-package="기본 패키지 1st.기본 패키지 2nd.mapper" />
   ```

3. src/main/resources에 log4jdbc.log4j2.properties 파일 생성

   ```java
   log4jdbc.spylogdelegator.name=net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator
   ```

4. src/test/java에 기본 패키지 1st.기본 패키지 2nd.persistence.JDBCTests 클래스를 추가

   ```java
   @Log4j
   public class JDBCTests {
   
   	static {
   		try {
   			Class.forName("com.mysql.cj.jdbc.Driver");
   		} catch (Exception e) {
   			e.printStackTrace();
   		}
   	}
   
   	@Test
   	public void testConnection() {
   		try (Connection con = DriverManager.getConnection(
   				"jdbc:mysql://localhost:3306/DB명?characterEncoding=UTF8&serverTimezone=UTC", "user명", "비밀번호")) {
   			System.out.println(con);
   		} catch (Exception e) {
   			fail(e.getMessage());
   		}
   	}
   
   }
   ```

5. Run As > JUnit Test



# 2. 영속/비즈니스 계층의 CRUD 구현

## 2-1. 영속 계층의 구현 준비

1. src/main/java에 기본 패키지 1st.기본 패키지 2nd.domain.BoardVO 클래스를 추가

   ```java
   @Data
   public class BoardVO {
   
   	private Long bno;
   	private String title;
   	private String content;
   	private String writer;
   	private Date regdate;
   	private Date updateDate;
   
   }
   ```

2. src/main/java에 기본 패키지1st.기본 패키지 2nd.mapper.BoardMapper 인터페이스를 추가

   ```java
   public interface BoardMapper {
   
   	@Select("SELECT * FROM tbl_board WHERE bno > 0")
   	public List<BoardVO> getList();
   	
   }
   ```

3. src/test/java에 기본 패키지 1st.기본 패키지 2nd.mapper.BoardMapperTests 클래스를 추가

   ```java
   @RunWith(SpringJUnit4ClassRunner.class)
   @ContextConfiguration("file:src/main/webapp/WEB-INF/spring/root-context.xml")
   @Log4j
   public class BoardMapperTests {
   
   	@Setter(onMethod_ = @Autowired)
   	private BoardMapper mapper;
   
   	@Test
   	public void testGetList() {
   		mapper.getList().forEach(board -> log.info(board));
   	}
   	
   }
   ```

4. JUnit Test

5. src/main/resources에 기본 패키지 1st/기본 패키지 2nd/mapper 단계의 폴더를 생성하고 BoardMapper XML 파일을 작성 (폴더를 한 번에 생성하지 말고 하나씩 생성)

   ```java
   <!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
   "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <mapper namespace="com.test.mapper.BoardMapper">
   
   	<select id="getList" resultType="com.test.domain.BoardVO">
   	<![CDATA[
   	SELECT * FROM tbl_board WHERE bno >0
   	]]>
   	</select>
   	
   </mapper>
   ```

6. BoardMapper 인터페이스에 어노테이션을 제거

   ```java
   public interface BoardMapper {
   
   //	@Select("SELECT * FROM tbl_board WHERE bno > 0")
   	public List<BoardVO> getList();
   	
   }
   ```

7. 기존의 테스트 코드를 통해서 기존과 동일하게 동작하는지 확인



## 2-2. 영속 영역의 CRUD 구현

1. create(insert) 처리
2. read(select) 처리
3. delete 처리
4. update 처리

**BoardMapper 인터페이스**

```java
public interface BoardMapper {

//	@Select("SELECT * FROM tbl_board WHERE bno > 0")
	public List<BoardVO> getList();

	public void insert(BoardVO board);

	public void insertSelectKey(BoardVO board);

	public BoardVO read(long bno);

	public int delete(long bno);

	public int update(BoardVO board);
	
}
```

**BoardMapper.xml**

```java
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.test.mapper.BoardMapper">

	<select id="getList" resultType="com.test.domain.BoardVO">
	<![CDATA[
	SELECT * FROM tbl_board WHERE bno >0
	]]>
	</select>

	<insert id="insert">
		INSERT INTO tbl_board
		(title, content, writer) VALUES
		(#{title}, #{content},
		#{writer})
	</insert>

	<insert id="insertSelectKey">
		<selectKey keyProperty="bno" order="BEFORE"
			resultType="long">
			SELECT IFNULL(MAX(bno), 0) + 1 FROM tbl_board
		</selectKey>
		INSERT INTO tbl_board (bno, title,
		content, writer) VALUES (#{bno},
		#{title}, #{content}, #{writer})
	</insert>

	<select id="read" resultType="com.test.domain.BoardVO">
		SELECT * FROM tbl_board WHERE bno =
		#{bno}
	</select>

	<delete id="delete">
		DELETE FROM tbl_board WHERE
		bno = #{bno}
	</delete>

	<update id="update">
		UPDATE tbl_board SET
		title=#{title},
		content=#{content}, writer=#{writer},
		updatedate=NOW()
		WHERE bno=#{bno}
	</update>
	
</mapper>
```

**BoardMapperTests 클래스**

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("file:src/main/webapp/WEB-INF/spring/root-context.xml")
@Log4j
public class BoardMapperTests {

	@Setter(onMethod_ = @Autowired)
	private BoardMapper mapper;

	@Test
	public void testGetList() {
		mapper.getList().forEach(board -> log.info(board));
	}

	@Test
	public void testInsert() {
		BoardVO board = new BoardVO();
		board.setTitle("새로 작성하는 글");
		board.setContent("새로 작성하는 내용");
		board.setWriter("newbie");
		mapper.insert(board);
		log.info(board);
	}

	@Test
	public void testInsertSelectKey() {
		BoardVO board = new BoardVO();
		board.setTitle("새로 작성하는 글 select key");
		board.setContent("새로 작성하는 내용 select key");
		board.setWriter("newbie");
		mapper.insertSelectKey(board);
		log.info(board);
	}

	@Test
	public void testRead() {
		BoardVO board = mapper.read(5L);
		log.info(board);
	}

	@Test
	public void testDelete() {
		log.info("DELETE COUNT : " + mapper.delete(3L));
	}

	@Test
	public void testUpdate() {
		BoardVO board = new BoardVO();
		board.setBno(5L);
		board.setTitle("수정된 제목");
		board.setContent("수정된 내용");
		board.setWriter("user00");
		int count = mapper.update(board);
		log.info("UPDATE COUNT: " + count);
	}
	
}
```



# 3. 비즈니스 계층

## 3-1. 비즈니스 계층의 설정

1. src/main/java에 기본 패키지 1st.기본 패키지 2nd.service.BoardService 인터페이스를 추가

   ```java
   public interface BoardService {
   
   	public void register(BoardVO board);
   
   	public BoardVO get(Long bno);
   
   	public boolean modify(BoardVO board);
   
   	public boolean remove(Long bno);
   
   	public List<BoardVO> getList();
   	
   }
   ```

2. src/main/java에 기본 패키지 1st.기본 패키지 2nd.service.BoardServiceImpl 클래스를 추가

   ```java
   @Service
   @AllArgsConstructor
   public class BoardServiceImpl implements BoardService {
   
   	private BoardMapper mapper;
   
   	@Override
   	public void register(BoardVO board) {
   		System.out.println("register......" + board);
   		mapper.insertSelectKey(board);
   	}
   
   	@Override
   	public List<BoardVO> getList() {
   		System.out.println("getList......");
   		return mapper.getList();
   	}
   
   	@Override
   	public BoardVO get(Long bno) {
   		System.out.println("get......" + bno);
   		return mapper.read(bno);
   	}
   
   	@Override
   	public boolean modify(BoardVO board) {
   		System.out.println("modify......" + board);
   		return mapper.update(board) == 1;
   	}
   
   	@Override
   	public boolean remove(Long bno) {
   		System.out.println("remove......" + bno);
   		return mapper.delete(bno) == 1;
   	}
   	
   }
   ```

3. root-context.xml의 네임스페이스 탭에서 context 항목을 추가

4. root-context.xml의 내부에 아래 내용을 추가

   ```java
   <context:component-scan
   base-package="com.test.service">
   </context:component-scan>
   ```



## 3-2. 비즈니스 계층의 구현과 테스트

1. src/test/java에 기본 패키지 1st.기본 패키지 2nd.service.BoardServiceTests 클래스를 작성

   ```java
   @RunWith(SpringJUnit4ClassRunner.class)
   @ContextConfiguration("file:src/main/webapp/WEB-INF/spring/root-context.xml")
   @Log4j
   public class BoardServiceTests {
   
   	@Setter(onMethod_ = { @Autowired })
   	private BoardService service;
   
   	@Test
   	public void testExist() {
   		log.info(service);
   		assertNotNull(service);
   	}
   	
   }
   ```

2. 등록 작업의 구현과 테스트

3. 목록(리스트) 작업의 구현과 테스트

4. 조회 작업의 구현과 테스트

5. 삭제/수정 구현과 테스트

**BoardServiceImpl 클래스**

```java
@Service
@AllArgsConstructor
public class BoardServiceImpl implements BoardService {

	private BoardMapper mapper;

	@Override
	public void register(BoardVO board) {
		System.out.println("register......" + board);
		mapper.insertSelectKey(board);
	}

	@Override
	public List<BoardVO> getList() {
		System.out.println("getList......");
		return mapper.getList();
	}

	@Override
	public BoardVO get(Long bno) {
		System.out.println("get......" + bno);
		return mapper.read(bno);
	}

	@Override
	public boolean modify(BoardVO board) {
		System.out.println("modify......" + board);
		return mapper.update(board) == 1;
	}

	@Override
	public boolean remove(Long bno) {
		System.out.println("remove......" + bno);
		return mapper.delete(bno) == 1;
	}

}
```

**BoardServiceTests 클래스**

```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration("file:src/main/webapp/WEB-INF/spring/root-context.xml")
@Log4j
public class BoardServiceTests {

	@Setter(onMethod_ = { @Autowired })
	private BoardService service;

	@Test
	public void testExist() {
		log.info(service);
		assertNotNull(service);
	}

	@Test
	public void testRegister() {
		BoardVO board = new BoardVO();
		board.setTitle("새로 작성하는 글");
		board.setContent("새로 작성하는 내용");
		board.setWriter("newbie");
		service.register(board);
		log.info("생성된 게시물의 번호 : " + board.getBno());
	}

	@Test
	public void testGetList() {
		service.getList().forEach(board -> log.info(board));
	}

	@Test
	public void testGet() {
		log.info(service.get(1L));
	}

	@Test
	public void testUpdate() {
		BoardVO board = service.get(1L);
		if (board == null) {
			return;
		}
		board.setTitle("제목 수정합니다.");
		log.info("MODIFY RESULT : " + service.modify(board));
	}

	@Test
	public void testDelete() {
		log.info("REMOVE RESULT : " + service.remove(2L));
	}

}
```



# 4. 프레젠테이션(웹) 계층의 CRUD 구현

## 4-1. BoardController의 작성

1. src/main/java에 기본 패키지 1st.기본 패키지 2nd.controller.BoardController 클래스를 추가
2. src/test/java에 기본 패키지 1st.기본 패키지 2nd.controller.BoardControllerTests 클래스를 추가
3. 목록에 대한 처리와 테스트
4. 등록 처리와 테스트
5. 조회 처리와 테스트
6. 수정 처리와 테스트
7. 삭제 처리와 테스트

**BoardController 클래스**

```java
@Controller
@RequestMapping("/board/*")
@AllArgsConstructor
public class BoardController {

	private BoardService service;

	@GetMapping("/list")
	public void list(Model model) {
		model.addAttribute("list", service.getList());
	}

	@PostMapping("/register")
	public String register(BoardVO board, RedirectAttributes rttr) {
		service.register(board);
		rttr.addFlashAttribute("result", board.getBno());
		return "redirect:/board/list";
	}

	@GetMapping("/get")
	public void get(@RequestParam("bno") Long bno, Model model) {
		model.addAttribute("board", service.get(bno));
	}

	@PostMapping("/modify")
	public String modify(BoardVO board, RedirectAttributes rttr) {
		if (service.modify(board)) {
			rttr.addFlashAttribute("result", "success");
		}
		return "redirect:/board/list";
	}

	@PostMapping("/remove")
	public String remove(@RequestParam("bno") Long bno, RedirectAttributes rttr) {
		if (service.remove(bno)) {
			rttr.addFlashAttribute("result", "success");
		}
		return "redirect:/board/list";
	}

	@GetMapping("/register")
	public void register() {
	}

}
```

**BoardControllerTests 클래스**

```java
@RunWith(SpringJUnit4ClassRunner.class)
@WebAppConfiguration
@ContextConfiguration({ "file:src/main/webapp/WEB-INF/spring/root-context.xml",
		"file:src/main/webapp/WEB-INF/spring/appServlet/servlet-context.xml" })
@Log4j
public class BoardControllerTests {

	@Setter(onMethod_ = { @Autowired })
	private WebApplicationContext ctx;
	private MockMvc mockMvc;

	@Before
	public void setup() {
		this.mockMvc = MockMvcBuilders.webAppContextSetup(ctx).build();
	}

	@Test
	public void testList() throws Exception {
		log.info(
				mockMvc.perform(MockMvcRequestBuilders.get("/board/list")).andReturn().getModelAndView().getModelMap());
	}

	@Test
	public void testRegister() throws Exception {
		String resultPage = mockMvc
				.perform(MockMvcRequestBuilders.post("/board/register").param("title", "테스트 새글 제목")
						.param("content", "테스트 새글 내용").param("writer", "user00"))
				.andReturn().getModelAndView().getViewName();
		log.info(resultPage);
	}

	@Test
	public void testGet() throws Exception {
		log.info(mockMvc.perform(MockMvcRequestBuilders.get("/board/get").param("bno", "2")).andReturn()
				.getModelAndView().getModelMap());
	}

	@Test
	public void testModify() throws Exception {
		String resultPage = mockMvc
				.perform(MockMvcRequestBuilders.post("/board/modify").param("bno", "1").param("title", "수정된 테스트 새글 제목")
						.param("content", "수정된 테스트 새글 내용").param("writer", "user00"))
				.andReturn().getModelAndView().getViewName();
		log.info(resultPage);
	}

	@Test
	public void testRemove() throws Exception {
		String resultPage = mockMvc.perform(MockMvcRequestBuilders.post("/board/remove").param("bno", "25")).andReturn()
				.getModelAndView().getViewName();
		log.info(resultPage);
	}
	
}
```



# 5. 화면 처리

- jQuery 라이브러리를 head 태그 사이에 추가

  ```jsp
  <script src="https://code.jquery.com/jquery-3.4.1.min.js"></script>
  ```

- JSTL의 출력과 포맷을 적용할 수 있는 태그 라이브러리를 추가

  ```jsp
  <%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
  <%@ taglib uri="http://java.sun.com/jsp/jstl/fmt" prefix="fmt"%>
  ```

  

## 5-1. 기본 작업

1. src에 main/webapp/WEB-INF/views/board 폴더를 추가
2. 프로젝트를 선택하고, Run As > Run on Server
3. Servers > Tomcat 더블클릭 > Modules > Edit > Path를 '/'(절대경로)로 조정



## 5-2. 목록 화면 처리

- list.jsp를 작성
- Model에 담긴 데이터 출력



## 5-3. 등록 입력 페이지와 등록 처리

- register.jsp를 작성
- 한글 문제와 UTF-8 필터 처리
- 재전송(redirect) 처리
- 목록에서 버튼으로 이동하기



## 5-4. 조회 페이지와 이동

- get.jsp를 작성
- 조회 페이지 작성
- 목록 페이지와 뒤로 가기 문제



## 5-5. 게시물의 수정/삭제 처리

- modify.jsp를 작성
- 수정/삭제 페이지로 이동
- 게시물 수정/삭제 확인
- 조회 페이지에서 <form> 처리
- 수정 페이지에서 링크 처리



# 6. Mysql 데이터베이스 페이징 처리

**재귀 복사**

```mysql
INSERT INTO tbl_board (title, content, writer) (SELECT title, content, writer FROM tbl_board);
```

**LIMIT**

```mysql
SELECT * FROM table명 LIMIT 출력할 레코드의 시작 행 오프셋 값, 출력하고자 하는 레코드 개수;
```



# 7. MyBatis와 스프링에서 페이징 처리

1. src/main/java에 기본 패키지 1st.기본 패키지 2nd.domain.Criteria 클래스를 추가

   ```java
   @Getter
   @Setter
   @ToString
   public class Criteria {
   
   	private int pageNum;
   	private int amount;
   
   	public Criteria() {
   		this(1, 10);
   	}
   
   	public Criteria(int pageNum, int amount) {
   		this.pageNum = pageNum;
   		this.amount = amount;
   	}
   
   	public int getPageStart() {
   		return (this.pageNum - 1) * amount;
   	}
       
   }
   ```



## 7-1. MyBatis 처리와 테스트

1. BoardMapper 인터페이스에 Criteria 타입을 파라미터로 사용하는 getListWithPaging() 메서드를 작성

   ```java
   public List<BoardVO> getListWithPaging(Criteria cri);
   ```

2. BoardMapper.xml에 getListWithPaging에 해당하는 태그를 추가

   ```java
   <select id="getListWithPaging"
   		resultType="com.test.domain.BoardVO">
   	<![CDATA[
   	SELECT * FROM tbl_board
   	limit #{pageStart}, #{amount}
   	]]>
   	</select>
   ```

3. BoardMapperTests 클래스에 메서드를 추가

   ```java
   @Test
   	public void testPaging() {
   		Criteria cri = new Criteria();
   		cri.setPageNum(3);
   		cri.setAmount(10);
   		List<BoardVO> list = mapper.getListWithPaging(cri);
   		list.forEach(board -> log.info(board.getBno()));
   	}
   ```



## 7-2. BoardController와 BoardService 수정

1. BoardService 인터페이스를 수정

   ```java
   //	public List<BoardVO> getList();
   
   	public List<BoardVO> getList(Criteria cri);
   ```

2. BoardServiceImple 클래스를 수정

   ```java
   //	@Override
   //	public List<BoardVO> getList() {
   //		System.out.println("getList......");
   //		return mapper.getList();
   //	}
   
   	@Override
   	public List<BoardVO> getList(Criteria cri) {
   		System.out.println("get List with criteria:" + cri);
   		return mapper.getListWithPaging(cri);
   	}
   ```

3. BoardServiceTests 클래스를 수정

   ```java
   @Test
   	public void testGetList() {
   //		service.getList().forEach(board -> log.info(board));
   		service.getList(new Criteria(2, 10)).forEach(board -> log.info(board));
   	}
   ```

4. BoardController 클래스를 수정

   ```java
   //	@GetMapping("/list")
   //	public void list(Model model) {
   //		model.addAttribute("list", service.getList());
   //	}
   
   	@GetMapping("/list")
   	public void list(Criteria cri, Model model) {
   		model.addAttribute("list", service.getList(cri));
   	}
   ```

5. BoardControllerTests 클래스에 메서드를 추가

   ```java
   @Test
   	public void testListPaging() throws Exception {
   		log.info(mockMvc.perform(MockMvcRequestBuilders.get("/board/list").param("pageNum", "2").param("amount", "50"))
   				.andReturn().getModelAndView().getModelMap());
   	}
   ```



# 7. 페이징 화면 처리

## 7-1. 페이징 처리를 위한 클래스 설계

1. src/main/java에 기본 패키지 1st.기본 패키지 2st.domain.PageDTO 클래스를 추가

   ```java
   @Getter
   @ToString
   public class PageDTO {
   
   	private int startPage;
   	private int endPage;
   	private boolean prev, next;
   	private int total;
   	private Criteria cri;
   
   	public PageDTO(Criteria cri, int total) {
   		this.cri = cri;
   		this.total = total;
   		this.endPage = (int) (Math.ceil(cri.getPageNum() / 10.0)) * 10;
   		this.startPage = this.endPage - 9;
   		int realEnd = (int) (Math.ceil((total * 1.0) / cri.getAmount()));
   		if (realEnd < this.endPage) {
   			this.endPage = realEnd;
   		}
   		this.prev = this.startPage > 1;
   		this.next = this.endPage < realEnd;
   	}
   
   }
   ```

2. list.jsp를 수정

3. BoardController 클래스를 수정

   ```java
   @GetMapping({ "/get", "/modify" })
   	public void get(@RequestParam("bno") Long bno, @ModelAttribute("cri") Criteria cri, Model model) {
   		model.addAttribute("board", service.get(bno));
   	}
   @PostMapping("/modify")
   	public String modify(BoardVO board, @ModelAttribute("cri") Criteria cri, RedirectAttributes rttr) {
   		if (service.modify(board)) {
   			rttr.addFlashAttribute("result", "success");
   		}
   		rttr.addAttribute("pageNum", cri.getPageNum());
   		rttr.addAttribute("amount", cri.getAmount());
   		return "redirect:/board/list";
   	}
   
   	@PostMapping("/remove")
   	public String remove(@RequestParam("bno") Long bno, @ModelAttribute("cri") Criteria cri, RedirectAttributes rttr) {
   		if (service.remove(bno)) {
   			rttr.addFlashAttribute("result", "success");
   		}
   		rttr.addAttribute("pageNum", cri.getPageNum());
   		rttr.addAttribute("amount", cri.getAmount());
   		return "redirect:/board/list";
   	}
   ```

4. get.jsp를 수정

5. modify.jsp를 수정



## 7-2. MyBatis에서 전체 데이터의 개수 처리

1. BoardMapper 인터페이스를 수정

   ```java
   public int getTotalCount(Criteria cri);
   ```

2. BoardMapper.xml을 수정

   ```java
   <select id="getTotalCount" resultType="int">
   		select count(*) from
   		tbl_board where bno>0
   	</select>
   ```

3. BoardService 인터페이스를 수정

   ```java
   public int getTotal(Criteria cri);
   ```

4. BoardServiceImpl 클래스를 수정

   ```java
   @Override
   	public int getTotal(Criteria cri) {
   		System.out.println("get total count");
   		return mapper.getTotalCount(cri);
   	}
   ```

5. BoardController 클래스를 수정

   ```java
   @GetMapping("/list")
   	public void list(Criteria cri, Model model) {
   		model.addAttribute("list", service.getList(cri));
   //		model.addAttribute("pageMaker", new PageDTO(cri, 123));
   		int total = service.getTotal(cri);
   		model.addAttribute("pageMaker", new PageDTO(cri, total));
   	}
   ```



# 8. 파일 업로드 처리

## 8-1. 스프링의 첨부파일을 위한 설정

1. C 드라이브 밑에 upload 폴더와 임시 업로드 파일을 저장할 temp 폴더를 생성

2. 프로젝트를 생성

3. 생성된 프로젝트의 pom.xml을 수정

   ```java
   <properties>
   		<java-version>1.8</java-version>
   		<org.springframework-version>5.0.7.RELEASE</org.springframework-version>
   		<org.aspectj-version>1.9.0</org.aspectj-version>
   		<org.slf4j-version>1.7.25</org.slf4j-version>
   	</properties>
       
   <dependency>
   			<groupId>javax.servlet</groupId>
   			<artifactId>javax.servlet-api</artifactId>
   			<version>3.1.0</version>
   			<scope>provided</scope>
   		</dependency>
       
   <!-- lombok -->
   		<!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
   		<dependency>
   			<groupId>org.projectlombok</groupId>
   			<artifactId>lombok</artifactId>
   			<version>1.18.0</version>
   			<scope>provided</scope>
   		</dependency>
   ```

4. web.xml을 수정

   ```java
   <web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
   	xmlns="http://xmlns.jcp.org/xml/ns/javaee"
   	xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
   	id="WebApp_ID" version="3.1">
   	
   <multipart-config>
   			<location>C:\\upload\\temp</location>
   			<max-file-size>20971520</max-file-size> <!--1MB * 20 -->
   			<max-request-size>41943040</max-request-size><!-- 40MB -->
   			<file-size-threshold>20971520</file-size-threshold> <!-- 20MB -->
   		</multipart-config>
   ```

5. servlet-context를 수정

   ```java
   <beans:bean id="multipartResolver"
   		class="org.springframework.web.multipart.support.StandardServletMultipartResolver">
   	</beans:bean>
   ```



## 8-2. <form> 방식의 파일 업로드

1. src/main/java에 org.zerock.controller.UploadController를 추가

   ```java
   @Controller
   public class UploadController {
   
   	@GetMapping("/uploadForm")
   	public void uploadForm() {
   		System.out.println("upload form");
   	}
   
   }
   ```

2. WEB-INF/views에 uploadForm.jsp를 작성

3. UploadController 클래스를 수정

   ```java
   @PostMapping("/uploadFormAction")
   	public void uploadFormPost(MultipartFile[] uploadFile, Model model) {
   		String uploadFolder = "C:\\upload";
   		for (MultipartFile multipartFile : uploadFile) {
   			System.out.println("----------");
   			System.out.println("Upload File Name : " + multipartFile.getOriginalFilename());
   			System.out.println("Upload File Size : " + multipartFile.getSize());
   
   			File saveFile = new File(uploadFolder, multipartFile.getOriginalFilename());
   
   			try {
   				multipartFile.transferTo(saveFile);
   			} catch (Exception e) {
   				System.out.println(e.getMessage());
   			} // end catch
   		} // end for
   	}
   ```



## 8-3. Ajax를 이용하는 파일 업로드

1. UploadController 클래스를 수정

   ```java
   @GetMapping("/uploadAjax")
   	public void uploadAjax() {
   		System.out.println("upload ajax");
   	}
   ```

2. WEB-INF/views에 uploadAjax.jsp를 작성

3. UploadController 클래스를 수정

   ```java
   @PostMapping("/uploadAjaxAction")
   	public void uploadAjaxPost(MultipartFile[] uploadFile) {
   		System.out.println("update ajax post.........");
   		String uploadFolder = "C:\\upload";
   		for (MultipartFile multipartFile : uploadFile) {
   			System.out.println("---------------");
   			System.out.println("Upload File Name : " + multipartFile.getOriginalFilename());
   			System.out.println("Upload File Size : " + multipartFile.getSize());
   			String uploadFileName = multipartFile.getOriginalFilename();
   
   			// IE has file path
   			uploadFileName = uploadFileName.substring(uploadFileName.lastIndexOf("\\") + 1);
   			System.out.println("only file name : " + uploadFileName);
   
   			File saveFile = new File(uploadFolder, multipartFile.getOriginalFilename());
   
   			try {
   				multipartFile.transferTo(saveFile);
   			} catch (Exception e) {
   				System.out.println(e.getMessage());
   			} // end catch
   		} // end for
   	}
   ```