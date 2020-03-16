# PHP

## 1. PHP 함수들

### 1-1. dirname()

주어진 경로의 디렉토리 목록을 반환한다.

```php
<?php
    echo dirname("/kr/co/test/helloworld.php");
?>
```

```
/kr/co/test
```

### 1-2. basename()

파일경로에서 파일이름만 반환한다.

```php
<?php
    echo basename("/kr/co/test/helloworld.php");
?>
```

```
helloworld.php
```

### 1-3. pathinfo()

파일의 경로, 확장자 등등 관련된 몇가지 정보를 반환한다.

```php
<?php
	$path_parts = pathinfo("/kr/co/test/helloworld.php");
	echo $path_parts['dirname'], "<br>";
	echo $path_parts['basename'], "<br>";
	echo $path_parts['extension'], "<br>";
	echo $path_parts['filename'], "<br>";
?>
```

```
/kr/co/test
helloworld.php
php
helloworld
```

### 1-4. parse_url()

URL을 해석해서 각 구성요소를 반환한다.

```php
<?php
	$url = 'http://username:password@hostname:9090/path?arg=value#anchor';

	var_dump(parse_url($url));
?>
```

```
array(8) {
  ["scheme"]=>
  string(4) "http"
  ["host"]=>
  string(8) "hostname"
  ["port"]=>
  int(9090)
  ["user"]=>
  string(8) "username"
  ["pass"]=>
  string(8) "password"
  ["path"]=>
  string(5) "/path"
  ["query"]=>
  string(9) "arg=value"
  ["fragment"]=>
  string(6) "anchor"
}
```

### 1-5. urldecode()

인코딩된 URL문자열을 디코딩한다.

```php
<?php
	echo urldecode('%ED%97%AC%EB%A1%9C%EC%9B%94%EB%93%9C.php');
?>
```

```
헬로월드.php
```

### 1-6. urlencode()

문자열을 URL 인코딩한다.

```php
<?php
	echo urlencode('헬로월드.php');
?>
```

```
%ED%97%AC%EB%A1%9C%EC%9B%94%EB%93%9C.php
```

### 1-7. explode()

문자열은 분리해서 배열로 반환한다.

```php
<?php
	$pizza = "piece1 piece2 piece3 piece4 piece5 piece6";
	$pieces = explode(" ", $pizza);
	for($i = 0; $i < count($pieces); $i++){
		echo $pieces[$i], "<br>";
	}
?>
```

```
piece1
piece2
piece3
piece4
piece5
piece6
```

### 1-8. implode()

지정된 문자를 포함해 배열을 하나의 문자열로 연결한다.

```php
<?php
	$pizza = "piece1 piece2 piece3 piece4 piece5 piece6";
	$pieces = explode(" ", $pizza);
	$pizza = implode(',', $pieces);
	echo $pizza;
?>
```

```
piece1,piece2,piece3,piece4,piece5,piece6
```

---

### 1-9. eregi() -->

PHP는 UNIX 스타일의 정규표현식인 ereg와 Perl 스타일의 정규표현식인 preg를 지원한다. 이 중에서 ereg는 폐지 예정(Deprecated)이기 때문에 사용해서는 안된다.

### 1-10. preg_match()

pattern에 주어진 정규표현식을 subject에서 찾습니다.

**preg_match ( string $pattern , string $subject [, array &$matches [, int $flags [, int $offset ]]] ) : int**

- pattern : 탐색할 패턴 문자열
- subject : 입력 문자열
- matches : matches 가 주어지면, 검색 결과를 채워넣습니다. $matches[0]는 전체 패턴 텍스트가 들어가고, $matches[1]부터 괄호로 둘러싸인 서브 패턴을 채워넣습니다.
- flags : flags는 다음과 같은 플래그를 사용할 수 있습니다.
  - PREG_OFFSET_CAPTURE : 이 플래그를 넘기면, 모든 매치에 대한 문자열 시작 위치를 함께 반환합니다. 반환값을 *0*에 매치한 문자열을 가지고, *1*에 문자열 시작 위치를 가지는 배열을 원소로 갖는 배열로 변경하는 점에 주의하십시오.
- offset : 일반적으로, 검색은 목표 문자열의 처음에서 시작합니다. 선택적인 인수 *`offset`* 으로 검색을 시작할 다른 위치를 지정할 수 있습니다. (바이트 단위)

```php
<?php
    // 패턴 구분자 뒤의 "i"는 대소문자를 구별하지 않게 합니다.
	if (preg_match("/php/i", "PHP is the web scripting language of choice.", $match)) {
		echo "발견하였습니다.";
	} else {
    	echo "발견하지 못했습니다.";
	}
?>
```

```
발견하였습니다.
```

### 1-11. preg_split()

정규 표현식에 따라서 주어진 문자열을 나눕니다.

**preg_split ( string $pattern , string $subject [, int $limit [, int $flags ]] ) : array**

- pattern : 탐색할 패턴 문자열
- subject : 입력 문자열
- limit : 지정하면, limit회까지 나눠진 문자열을 반환하며, limit가 -1이면 "무제한"을 의미합니다. 이 값은 flags를 지정할 때 유용합니다.
- flags : flags는 다음 플래그들을 조합할 수 있습니다 (bitwise | 연산자로 조합합니다) :
  - PREG_SPLIT_NO_EMPTY : 이 플래그를 설정하면, preg_split()에 의해 나눈 후 비어있지 않은 조각만을 반환합니다.
  - PREG_SPLIT_DELIM_CAPTURE : 이 플래그를 설정하면, 구분자 패턴 안의 서브패턴도 검출하여 반환합니다.
  - PREG_SPLIT_OFFSET_CAPTURE : 이 플래그를 설정하면, 문자열의 시작 위치도 반환합니다. 반환값이 매치된 문자열을 오프셋 *0*으로, 문자열 시작 위치를 오프셋 *1*로 가지는 배열을 원소로 갖는 배열로 변하는 점에 주의하십시오.

```php
<?php
    // " ", \r, \t, \n, \f를 포함하여 임의 갯수의 콤마와 스페이스로 구문을 나눕니다.
	$keywords = preg_split("/[\s,]+/", "hypertext language, programming");
	for($i = 0; $i < count($keywords); $i++){
		echo $keywords[$i], "<br>";
	}
?>
```

```
hypertext
language
programming
```

### 1-12. preg_replace()

subject를 검색하여 매치된 pattern을 replacement로 치환합니다.

**preg_replace ( mixed $pattern , mixed $replacement , mixed $subject [, int $limit [, int &$count ]] ) : mixed**

- pattern : 검색할 패턴. 문자열이나 문자열을 가진 배열일 수 있습니다.
- replacement : 치환할 문자열이나 문자열을 가진 배열
- subject : 검색 치환할 문자열이나 문자열을 가진 배열
- limit : 각 subject 문자열에 대한 각 패턴의 최대 치환수. 기본값은 -1. (무제한)
- count : 지정하면, 이 변수는 치환이 일어난 횟수로 채워집니다.

```php
<?php
	$string = 'April 15, 2003';
	$pattern = '/(\w+) (\d+), (\d+)/i';
	$replacement = '${1}1,$3';
	echo preg_replace($pattern, $replacement, $string);
?>
```

```
April1,2003
```

---

### 1-13. strip_tags()

문자열로 부터 HTML,PHP 태그를 제거한다.

**strip_tags ( string $str [, mixed $allowable_tags ] ) : string**

```php
<?php
	$text = '<p>Test paragraph.</p><!-- Comment --> <a href="#fragment">Other text</a>';
	echo strip_tags($text);
	echo "\n";
	echo strip_tags($text, '<p><a>');
?>
```

```
Test paragraph. Other text
<p>Test paragraph.</p> <a href="#fragment">Other text</a>
```

### 1-14. addslashes()

',",\ 앞에 역슬래쉬를 추가한다.

```php
<?php
	$str = "Is your name O'Reilly?";
	echo addslashes($str);
?>
```

```
Is your name O\'Reilly?
```

### 1-15. stripslashes()

addslashes()로 쿼트된 문자열을 언쿼트한다.

```php
<?php
	$str = "Is your name O\'reilly?";
	echo stripslashes($str);
?>
```

```
Is your name O'reilly?
```

### 1-16. htmlspecialchars()

특수문자를 HTML엔티티형태로 바꾼다.

**htmlspecialchars ( string $string [, int $flags = ENT_COMPAT | ENT_HTML401 [, string $encoding = ini_get("default_charset") [, bool $double_encode = TRUE ]]] ) : string**

| Character | Replacement        |
| --------- | ------------------ |
| &         | \&amp;             |
| "         | \quot;             |
| '         | \&#039; or \&apos; |
| <         | \&lt;              |
| >         | \&gt;              |

```php
<?php
	$new = htmlspecialchars("<a href='test'>Test</a>", ENT_QUOTES);
	echo $new;
?>
```

```
&lt;a href=&#039;test&#039;&gt;Test&lt;/a&gt;
```

---

### 1-17. ucfirst()

첫글자가 알파벳이면 첫문자만 대문자로 변환한다.

```php
<?php
	echo ucfirst("hello world");
?>
```

```
Hello world
```

### 1-18. lcfirst()

첫글자가 알파벳이면 첫문자만 소문자로 변환한다.

```php
<?php
	echo ucfirst("Hello World");
?>
```

```
hello World
```

### 1-19. strtolower()

문자열을 소문자로 변환한다.

```php
<?php
	echo strtolower("HeLlO WoRlD");
?>
```

```
hello world
```

### 1-20. strtoupper()

영문자를 대문자로 변환한다.

```php
<?php
	echo strtolower("HeLlO WoRlD");
?>
```

```
HELLO WORLD
```

### 1-21. strlen()

문자열의 길이를 반환한다.

```php
<?php
	echo "Hello world";
?>
```

```
11
```

### 1-22. count()

변수의 개수를 리턴한다.

```php
<?php
	$a[0] = 1;
	$a[1] = 3;
	$a[2] = 5;
	var_dump(count($a));
?>
```

```
int(3)
```

### 1-23. substr()

문자열의 일부를 잘라내어 반환한다.

**substr ( string $string , int $start [, int $length ] ) : string**

```php
<?php
	echo substr("abcdef", -1), "<br>";
	echo substr("abcdef", -2), "<br>";
	echo substr("abcdef", -3, 1), "<br>";
?>
```

```
f
ef
d
```

---

### 1-24. date()

주어진 함수의 타임스탬프를 지정한 포맷으로 변환한다.

```php
<?php
	echo date("Y-m-d H:i:s");
?>
```

```
2020-03-15 08:36:56
```

### 1-25. mktime()

주어진 날짜를 타임스탬프로 변환한다.

```php
<?php 
	$timestamp = mktime(1, 5, 25, 10, 18, 1995);
	echo date("Y-m-d H:i:s", $timestamp); 
?>
```

```
1995-10-18 01:05:25
```

### 1-26. strtotime()

주어진 날짜 형식의 문자열을 유닉스 타임스탬프로 변환한다.

```php
<?php 
	$timestamp = strtotime("+1 week");
	echo date("Y-m-d", $timestamp), "<br>";

	$timestamp = strtotime("2020-01-01 +1 week");
	echo date("Y-m-d", $timestamp), "<br>";
?>
```

```
2020-03-22
2020-01-08
```

### 1-27. time()

1970년 1월 1일을 기준으로 경과된 시간을 초단위로 표시한 시간

```php
<?php 
	echo time();
?>
```

```
1584261903
```

---

### 1-28. setcookie()

HTTP 헤더에 보낼 쿠키를 정의한다.

**setcookie (쿠키명, 쿠키값, 만료시간, 경로, 도메인, 보안, httponly) : bool**

- 쿠키명(필수) : 설정 될 쿠키 이름을 결정함
- 쿠키값(선택) : 쿠키 이름에 입력될 값
- 만료시간(선택) : Default 값은 0이며 쿠키가 유지될 시간을 설정
- 경로(선택) : 경로를 지정할 경우 특정 위치와 하위 경로에서만 사용가능하도록 설정됨
- 슬러쉬(/) : 슬러쉬 기호를 값으로 입력할 경우 전체 경로에서 사용됨을 의미
- 도메인(선택) : 사용될 도메인을 지정가능함. 서브도메인 입력시 해당 서브도메인만 사용가능
- 보안(선택) : 보안 프로토콜인 https에서만 사용가능하도록 설정함
- httponly : HTTP에서만 사용가능하도록 하여(서버단 언어로만...) 스크립트에 의한 쿠키 접근을 허용안하게 함

```php
<?php
	setCookie('cookie', time(), time() + 3600);
	echo $_COOKIE['cookie'];
?>
```

```
1584262661
```

### 1-29. header()

HTTP 응답 헤더를 직접 작성하여 전달할 수 있습니다.

**header ( string $header [, bool $replace = TRUE [, int $http_response_code ]] ) : void**

```php
<?php
	header("Location: http://www.example.com/");
	exit;
?>
```

### 1-30. session_start()

세션을 시작한다.

```php
<?php
    session_start();
?>
```

### 1-31. session_destroy()

생성된 모든 세션을 파괴한다.

```php
<?php
    session_destroy();
?>
```

---

### 1-32. $_GET

GET 방식으로 넘어온 변수

```html
<html>
<body>
    <form method="get" action="1.php">
        id :  <input type="text" name="id" />
        password :  <input type="text" name="password" />
        <input type="submit" />
    </form>
</body>
</html>
```

```php
<?php
  $id = $_GET['id'];
  $password = $_GET['password'];
?>
```

### 1-33. $_POST

POST 방식으로 넘어온 변수

```php
<html>
<body>
    <form method="post" action="2.php">
        id :  <input type="text" name="id" />
        password :  <input type="text" name="password" />
        <input type="submit" />
    </form>
</body>
</html>
```

```php
<?php
  $id = $_GET['id'];
  $password = $_GET['password'];
?>
```

### 1-34. $_COOKIE

```php
<?php
	setCookie('cookie', time(), time() + 3600);
	echo $_COOKIE['cookie'];
?>
```

```
1584262661
```

### 1-35. $_SESSION

```php
<?php
	session_start();
	$_SESSION['language'] = 'PHP';
	echo $_SESSION['language'];
?>
```

```
PHP
```

### 1-36. $_SERVER['HTTP_X_FORWARDED_FOR']

사용자가 프록시 서버를 경유해 접근하면 사용자의 IP주소를 가지고 있는 변수

```php
<?php
    $_SERVER['HTTP_X_FORWARDED_FOR'];
?>
```

### 1-37. $_SERVER

웹서버(아파치, nginx 등)를 통해 생성된 값들을 가지고 있는 배열 변수

```php
<?php
	// 사용자의 웹접속환경 정보
	echo $_SERVER['HTTP_USER_AGENT'], "<br>";
	// 쿼리 스트링
	echo $_SERVER['QUERY_STRING'], "<br>";
	// 사용자의 IP 주소
	echo $_SERVER["REMOTE_ADDR"], "<br>";
	// URI 스킴
	echo $_SERVER["REQUEST_SCHEME"], "<br>";
	// 요청 URI
	echo $_SERVER["REQUEST_URI"], "<br>";
	// 파일자신의 CLI경로
	echo $_SERVER["SCRIPT_FILENAME"], "<br>";
	// 페이지가 요청된 프로토콜 정보
	echo $_SERVER["SERVER_PROTOCOL"], "<br>";
	// 웹서버 정보
	echo $_SERVER["SERVER_SOFTWARE"], "<br>";
	// 파일자신의 웹경로(또는 CLI경로)
	echo $_SERVER["PHP_SELF"], "<br>";
?>
```

```
Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/70.0.3538.102 Safari/537.36 Edge/18.18362

::1
http
/test/test.php
C:/Bitnami/wampstack-7.3.15-1/apache2/htdocs/test/test.php
HTTP/1.1
Apache
/test/test.php
```

---

### 1-38. ini_get()

php.ini 설정 옵션의 값을 얻는다.

```php
<?php 
	echo ini_get('display_errors');
?>
```

```
1
```

### 1-39. ini_set()

php.ini 구성 옵션의 값을 설정합니다.

```php
<?php 
	ini_set('display_errors', 1);
	echo ini_get('display_errors');
?>
```

```
1
```

---

### 1-40. extract()

배열에서 키와 값을 변수와 값으로 추출한다.

```php
<?php
	$size = "large";
	$var_array = array("color" => "blue"
					"size"  => "medium",
					"shape" => "sphere");
	extract($var_array, EXTR_PREFIX_SAME, "wddx");
	echo "$color, $size, $shape, $wddx_size\n";
?>
```

```
blue, large, sphere, medium
```

### 1-41. ob_start()

출력 버퍼링이라는 기능을 사용하도록 해주는 함수로서 페이지의 첫 부분에 사용하면 출력문의 출력내용을 출력하지 않고, 페이지의 내용을 모두 처리한 다음에 비로소 출력문의 내용을 출력합니다.

```php
<?php
    ob_start();
?>
```

### 1-42. ob_get_length()

출력 버퍼의 길이를 반환

```php
<?php
	ob_start();
	echo "Hello ";
	$len1 = ob_get_length();
	echo "World";
	$len2 = ob_get_length();
	ob_end_clean();
	echo $len1 . ", ." . $len2;
?>
```

```
6, 11
```

### 1-43. ob_end_flush()

출력 버퍼를 전송하고 출력 버퍼링을 종료

```php
<?php
	ob_end_flush();
?>
```

### 1-44. flush()

출력 버퍼를 비웁니다.

```php
<?php
	ob_start();
	for ($i = 0; $i < 10; $i++) {
		echo "<br> Line to show.";
		echo str_pad('',4096)."\n";
		ob_flush();
		flush();
		sleep(1);
	}
	echo "Done.";
	ob_end_flush();
?>
```

```

Line to show. 
Line to show. 
Line to show. 
Line to show. 
Line to show. 
Line to show. 
Line to show. 
Line to show. 
Line to show. 
Line to show. Done.
```

---

### 1-45. mb_substr()

문자열의 일부를 얻는다.

**mb_substr ( string $str , int $start [, int $length = NULL [, string $encoding = mb_internal_encoding() ]] ) : string**

```php
<?php
	$sitename = '테스트';
	echo mb_substr($sitename, 0, 1, 'utf-8');
	// UTF-8 인코딩인 경우
?>
```

```
테
```

### 1-46. mb_detect_encoding()

문자 인코딩 감지

```php
<?php
	var_dump( mb_detect_encoding('안녕') );
?>
```

```
string(5) "UTF-8"
```

### 1-47. iconv

문자열을 요청 된 문자 인코딩으로 변환

```php
<?php
	iconv("euc-kr", "utf-8", "테스트");
?>
```

---

### 1-48. mysqli 함수들 - db 연결

```php
<?php
	mysql_connect('접속주소', '접속계정', '계정암호');
	mysql_select_db('데이터베이스명');

switch($_GET['mode']){
    case 'insert':
        $result = mysql_query("INSERT INTO topic (title, description, created) VALUES ('".mysql_real_escape_string($_POST['title'])."', '".mysql_real_escape_string($_POST['description'])."', now())");
        header("Location: list.php"); 
        break;
    case 'delete':
        mysql_query('DELETE FROM topic WHERE id = '.mysql_real_escape_string($_POST['id']));
        header("Location: list.php"); 
        break;
    case 'modify':
        mysql_query('UPDATE topic SET title = "'.mysql_real_escape_string($_POST['title']).'", description = "'.mysql_real_escape_string($_POST['description']).'" WHERE id = '.mysql_real_escape_string($_POST['id']));
        header("Location: list.php?id={$_POST['id']}");
        break;
}
?>
```

### 1-49. pdo 함수들 - db 연결

```php
<?php
$dbh = new PDO('mysql:host=접속주소;dbname=데이터베이스명', '접속계정', '계정암호', array(PDO::MYSQL_ATTR_INIT_COMMAND => "SET NAMES utf8"));
switch($_GET['mode']){
    case 'insert':
        $stmt = $dbh->prepare("INSERT INTO topic (title, description, created) VALUES (:title, :description, now())");
        $stmt->bindParam(':title',$title);
        $stmt->bindParam(':description',$description);
 
        $title = $_POST['title'];
        $description = $_POST['description'];
        $stmt->execute();
        header("Location: list.php"); 
        break;
    case 'delete':
        $stmt = $dbh->prepare('DELETE FROM topic WHERE id = :id');
        $stmt->bindParam(':id', $id);
 
        $id = $_POST['id'];
        $stmt->execute();
        header("Location: list.php"); 
        break;
    case 'modify':
        $stmt = $dbh->prepare('UPDATE topic SET title = :title, description = :description WHERE id = :id');
        $stmt->bindParam(':title', $title);
        $stmt->bindParam(':description', $description);
        $stmt->bindParam(':id', $id);
 
        $title = $_POST['title'];
        $description = $_POST['description'];
        $id = $_POST['id'];
        $stmt->execute();
        header("Location: list.php?id={$_POST['id']}");
        break;
}
?>
```



## 2. 정규식

### 2-1. 정규식 기본

문자열을 처리하는 방법 중의 하나로 특정한 조건의 문자를 '검색'하거나 '치환'하는 과정을 매우 간편하게 처리 할 수 있도록 하는 수단이다.

### 2-2. 정규식 패턴

**2-2-1. Hex color code**

![tmb_Hex color code.png](https://www.tuwlab.com/files/attach/images/2382/809/025/4ce0820ae6652174d8afda602ce45125.png)

**2-2-2. 전화번호**

![Phone number.png](https://www.tuwlab.com/files/attach/images/2382/809/025/1a45b1fcb4ad6591cc5473885dcb1e93.png)

**2-2-3. 이메일 주소**

![E-mail address.png](https://www.tuwlab.com/files/attach/images/2382/809/025/6a6f632fa8fe18bb3d9925ae252cacfe.png)

**2-2-4. 웹 페이지 URL**

![Web page URL.png](https://www.tuwlab.com/files/attach/images/2382/809/025/29a59f1042c0458cb5c2725691900624.png)

**2-2-5. 그림 파일명**

![Image file name.png](https://www.tuwlab.com/files/attach/images/2382/809/025/0b91d330ef2196d7ad1cf1deb97b8702.png)

### 2-3. 정규식 사용언어

**Java** : Pattern클래스와 Matcher클래스를 이용

- Java에서는 `\` 대신 `\\`를 적어야 합니다.

```java
import java.io.Console;
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class MyRegex{
    public static void main(String[] args){
        String searchTarget = "Luke Skywarker 02-123-4567 luke@daum.net\n다스베이더 070-9999-9999 darth_vader@gmail.com\nprincess leia 010 2454 3457 leia@gmail.com";

        Pattern pattern = Pattern.compile("0\\d{1,2}[ -]?\\d{3,4}[ -]?\\d{3,4}");
        Matcher matcher = pattern.matcher(searchTarget);
        while(matcher.find()){
            System.out.println(matcher.group(0));
        }
    }
}
```

```
02-123-4567
070-9999-9999
010 2454 3457
```

**Mysql** : REGEXP

```mysql
SELECT * FROM 테이블명
WHERE searchTarget REGEXP '0\d{1,2}[ -]?\d{3,4}[ -]?\d{3,4}';
```

**Javascript** : String 클래스의 match 함수를 이용 혹은 RegExp 객체를 생성하여 사용

```javascript
var searchTarget = "Luke Skywarker 02-123-4567 luke@daum.net\
다스베이더 070-9999-9999 darth_vader@gmail.com\
princess leia 010 2454 3457 leia@gmail.com";

/* g는 global의 약자로, 정규표현식과 일치하는 모든 내용을 찾아오라는 옵션입니다.
 */
var regex = /0\d{1,2}[ -]?\d{3,4}[ -]?\d{3,4}/g;
console.log(searchTarget.match(regex));
```

```
[ '02-123-4567', '070-9999-9999', '010 2454 3457' ]
```

### 2-4. 브라우저 에이전트 판별 방식

**Php**

```php
$_SERVER['HTTP_USER_AGENT'];
```

**Java** : request.getHeader("user-agent"); 

```java
String userAgent = request.getHeader("User-Agent");
```

**Javascript**

```javascript
var userAgent = navigator.userAgent;
```



## 3. 기타

### 3-1. URL, URI

| URL             | URI                   |
| --------------- | --------------------- |
| Locator         | Identifier            |
| URI의 하위 개념 | URL과 URN의 상위 개념 |
| 자원의 위치     | 자원의 식별자         |

### 3-2. PATH

파일이나 디렉터리의 일반적인 형태로서 파일 시스템에서 고유한 위치를 지정한다.

**3-2-1. 디렉터리**

디렉터리는 파일과 다른 디렉터리를 갖는 파일 시스템 내의 존재물로서 폴더라고도 불리운다.

- 루트 디렉터리

  파일 시스템 계층 구조 상의 최상위 디렉터리이다.

  - Unix: /
  - Windows: C:\

- 홈 디렉터리

  시스템의 사용자에게 각각 할당된 개별 디렉터리이다.

  - Unix: /Users/{계정명}
  - Windows: C:\Users\{계정명}

- 작업 디렉터리

  작업 중인 파일의 위치한 디렉터리이다.

  - ./

- 부모 디렉터리

  작업 디렉터리의 부모 디렉토리이다.

  - ../

**3-2-2. 파일 경로**

파일 경로는 파일 시스템에서 파일의 위치를 나타내는 방법이다. 경로에는 절대경로와 상대경로가 있다.

- 절대경로

  현재 작업 디렉터리와 관계없이 특정 파일의 절대적인 위치를 가리킨다. 루트 디렉터리를 기준으로 파일의 위치를 나타낸다.

  - http://www.mysite.com/index.html
  - /Users/leeungmo/Desktop/myImage.jpg
  - C:\users\leeungmo\Desktop\myImage.jpg
  - /index.html

- 상대경로

  현재 작업 디렉터리를 기준으로 특정 파일의 상대적인 위치를 가리킨다.

  - ./index.html
  - ../dist/index.js
  - ../../dist/index.js
  - index.html
  - html/index.html

### 3-3. QUERY

데이터베이스와 정보 시스템에 질의를 할 수 있게 하는 고급 컴퓨터 언어이다.

**3-3-1. 데이터베이스 생성/보기**

데이터베이스를 생성하고,

```mysql
mysql> CREATE DATABASE dbname;
```

현재 존재하는 데이터베이스 목록을 보여준다.

```mysql
mysql> SHOW DATABASES;
```

특정 데이타베이스를 사용하겠다고 선언한다.

```mysql
mysql> USE dbname;
```

쓸모 없으면 과감히 삭제한다.

```mysql
mysql> DROP DATABASE [IF EXISTS] dbname;
```

**IF EXISTS** 옵션은 비록 데이타베이스가 없더라도 오류를 발생시키지 말라는 의미이다.

**3-3-2. 테이블 생성/보기**

테이블을 생성하고,

```
mysql> CREATE TABLE tablename (
column_name1 INT,
column_name2 VARCHAR(15),
column_name3 INT );
```

현재 데이타베이스의 테이블 목록을 보고

```
mysql> SHOW TABLES;
```

테이블 구조를 살펴본다.

```
mysql> EXPLAIN tablesname;
혹은
mysql> DESCRIBE tablename;
```

이름을 잘못 지정했으면 이름을 변경할 수도 있다.

```
mysql> RENAME TABLE tablename1 TO tablename2[, tablename3 TO tablename4];
```

필요 없으면 삭제한다.

```
mysql> DROP TABLE [IF EXISTS] tablename;
```

**3-3-3. INSERT**

```
mysql> INSERT INTO tablename VALUES(값1, 값2, …);
```

혹은

```
mysql> INSERT INTO tablename (col1, col2, …) VALUES(값1, 값2, …);
```

**3-3-4. SELECT**

```
mysql> SELECT col1, col2, … FROM tablename;
```

컬럼명을 *로 하면 모든 컬럼 의미.

```
mysql> SELECT col1 AS ‘성명’, col2 AS ‘국어점수’ FROM grade;
```

컬럼의 이름을 바꿔서 출력.

```
mysql> SELECT * FROM tablename ORDER BY col1 DESC;
mysql> SELECT col1, korean + math english AS ‘총점’ FROM tablename ORDER BY ‘총점’ ASC;
```

**DESC**는 내림차순 **ASC**는 오름차순.

```
mysql> SELECT * FROM grade WHERE korean < 90;
```

조건줘서 SELECT.

```
mysql> SELECT * FROM grade LIMIT 10;
```

결과중 처음부터 10개만 가져오기

```
mysql> SELECT * FROM grade LIMIT 100, 10;
```

결과중 100번째부터 10개만 가져오기. **첫번째 레코드는 0번 부터 시작**한다.

**3-3-5. UPDATE**

```
mysql> UPDATE tablename SET col1=새값 WHERE 조건;
```

**3-3-6. DELETE**

```
mysql> DELETE FROM tablename WHERE 조건;
```

### 3-4. REFERER

HTTP 리퍼러는 웹 브라우저로 월드 와이드 웹을 서핑할 때, 하이퍼링크를 통해서 각각의 사이트로 방문시 남는 흔적을 말한다.

> 예를 들어 A라는 웹 페이지에 B 사이트로 이동하는 하이퍼링크가 존재한다고 하자. 이때 웹 사이트 이용자가 이 하이퍼링크를 클릭하게 되면 웹 브라우저에서 B 사이트로 참조 주소(리퍼러)를 전송하게 된다. B 사이트의 관리자는 이 전송된 리퍼러를 보고 방문객이 A 사이트를 통해 자신의 사이트에 방문한 사실을 알 수 있다.

### 3-5. Browser Agent

사용자 에이전트는 사용자를 대신하여 일을 수행하는 소프트웨어 에이전트이다. 대개 웹 브라우저를 뜻한다.

![Browser Agent](https://mblogthumb-phinf.pstatic.net/20160707_259/heungmusoft_1467873663251K06wC_JPEG/image_424864681467873164117.jpg?type=w800)

### 3-6. Cookie - Session

**Cookie**

- 클라이언트(브라우저)에 데이터를 저장

**Session**

- SID(session ID)를 식별자로 서버에 데이터를 저장
- 주로 사용자 인증시에 사용함

### 3-7. 1사 쿠키, 3사 쿠키

**1사 쿠키**

사용자가 방문한 웹사이트에 의해 생성된 쿠키로서 이 1사 쿠키를 발급한 웹사이트만 이들 쿠키를 읽을 수 있음

**3사 쿠키**

사용자가 방문한 웹사이트가 아닌 제3의 웹사이트에 의해 생성된 쿠키. 사용자가 웹 사이트를 탐색하고 다른 기관이 해당 웹 사이트를 통해 쿠키를 설정하면 이는 제3사쿠키.