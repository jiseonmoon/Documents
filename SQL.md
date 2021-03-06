# SQL

## 1. SQL 이해하기

- **SQL** : 데이터베이스와 소통하기 위해 고안된 언어
- **데이터베이스** : 정리된 데이터(하나 또는 여러 개의 파일)를 저장하기 위한 공간
- **테이블** : 구조화된 특정한 타입의 데이터 목록
- **스키마** : 데이터베이스와 테이블 구조, 속성에 대한 정보
- **컬럼** : 테이블에 있는 하나의 필드. 모든 테이블은 한 개 이상의 컬럼으로 구성되어 있다.
- **데이터타입** : 허용되는 데이터의 유형. 모든 테이블 컬럼은 데이터 타입을 가지고 있고, 컬럼에는 정해진 데이터타입만 허용된다(정해지지 않은 데이터타입은 제한된다).
- **행** : 테이블에 있는 레코드
- **주 키** : 테이블에 있는 각 행을 구별하는 컬럼(또는 컬럼 집합)



## 2. 데이터 가져오기

**키워드** : SQL 언어의 일부분인 예약어로, 키워드는 테이블명 또는 컬럼명으로 사용할 수 없다.

### 2-1. 단일컬럼 가져오기

```sql
SELECT 컬럼명
FROM 테이블명;
```

### 2-2. 다중컬럼 가져오기

```sql
SELECT 컬럼명1, 컬럼명2, 컬럼명3
FROM 테이블명;
```

### 2-3. 모든컬럼 가져오기

```sql
SELECT *
FROM 테이블명;
```

### 2-4. 중복행 출력 방지하기

```sql
SELECT DISTINCT 컬럼명
FROM 테이블명;
```

### 2-5. 결과 제한하기

```mysql
SELECT 컬럼명
FROM 테이블명
LIMIT 몇 개의 행을 가져올지 OFFSET 몇 번째 행부터 가져올지;
```

### 2-6. 주석 사용하기

```sql
-- 한 줄 주석
/* 다중 행 주석
디중 행 주석*/
```



## 3. 가져온 데이터 정렬하기

### 3-1. 데이터 정렬하기

```sql
SELECT 컬럼명
FROM 테이블명
ORDER BY 정렬의 기준이 되는 컬럼명;
```

**절** : SQL 구문은 절로 구성되어 있는데, 절은 필수로 사용해야 하는 것과 선택해서 사용할 수 있는 것으로 나뉜다. 절은 보통 키워드와 그 키워드에 해당하는 데이터로 이루어진다.

### 3-2. 여러 개의 컬럼으로 정렬하기

```sql
SELECT 컬럼명
FROM 테이블명
ORDER BY 정렬의 기준이 되는 컬럼명1, 정렬의 기준이 되는 컬럼명2;
```

### 3-3. 컬럼의 위치로 정렬하기

```sql
SELECT 컬럼명
FROM 테이블명
ORDER BY 컬럼 위치;
```

### 3-4. 정렬 순서 지정하기

- **오름차순 정렬**

  ```sql
  SELECT 컬럼명
  FROM 테이블명
  ORDER BY 정렬의 기준이 되는 컬럼명 ASC;
  ```

  오름차순 정렬이 기본값이기 때문에 잘 사용하지 않는다.

- **내림차순 정렬**

  ```sql
  SELECT 컬럼명
  FROM 테이블명
  ORDER BY 정렬의 기준이 되는 컬럼명 DESC;
  ```



## 4. 데이터 필터링

### 4-1. WHERE절 사용하기

```sql
SELECT 컬럼명
FROM 테이블명
WHERE 컬럼명 연산자 값;
```

**WHERE절 연산자**

| 연산자                            | 설명                   |
| --------------------------------- | ---------------------- |
| =                                 | 같다.                  |
| <>                                | 같지 않다.             |
| !=                                | 같지 않다.             |
| <                                 | ~보다 작다.            |
| <=                                | ~보다 작거나 같다.     |
| !<                                | ~보다 작지 않다.       |
| >                                 | ~보다 크다.            |
| >=                                | ~보다 크거나 같다.     |
| !>                                | ~보다 크지 않다.       |
| BETWEEN 시작하는 값 AND 끝나는 값 | 두 개의 특정한 값 사이 |
| IS NULL                           | 값이 NULL이다.         |

**NULL** : 값이 들어 있지 않은 상태. 0, 빈 문자열, 공백 문자열과는 다른 값이다.



## 5. 고급 데이터 필터링

### 5-1. WHERE절 조합하기

**연산자** : 절을 연결하거나 변경하기 위해 WHERE절에서 사용하는 특별한 키워드. 논리 연산자라고도 한다.

- **AND 연산자 사용하기**

  **AND** : 지정된 모든 조건을 충족하는 행을 가져오도록 WHERE절에서 사용하는 키워드

  ```sql
  SELECT 컬럼명
  FROM 테이블명
  WHERE 검색 조건1 AND 검색 조건2;
  ```

- **OR 연산자 사용하기**

  **OR** : 지정된 조건을 하나라도 만족하는 행을 가져오도록 WHERE절에서 사용하는 키워드

  ```sql
  SELECT 컬럼명
  FROM 테이블명
  WHERE 검색 조건1 OR 검색 조건2;
  ```

- 다른 언어와 비슷하게 SQL은 OR 연산자 전에 AND 연산자를 처리한다. WHERE절에서 AND와 OR 연산자를 같이 사용할 때는 괄호를 사용하여 연산자를 그룹핑하자.

- **IN 연산자 사용하기**

  **IN** : WHERE절에서 OR 비교로 일치하는 값을 찾기 위해 조건을 지정하는 키워드

  ```sql
  SELECT 컬럼명
  FROM 테이블명
  WHERE 컬럼명 IN (값1, 값2);
  ```

- **NOT 연산자 사용하기**

  **NOT** : WHERE절에서 조건을 부정하기 위해 사용하는 키워드

  ```sql
  SELECT 컬럼명
  FROM 테이블명
  WHERE NOT 검색 조건;
  ```



## 6. 와일드카드 문자를 이용한 필터링

### 6-1. LIKE 연산자 사용하기

**와일드카드** : 여러 데이터에서 부분적으로 일치하는 값이 있는지 확인할 때 사용되는 특수 문자

- % 와일드카드 : 임의의 수의 문자를 의미한다.
- _ 와일드카드 : 단 한 개의 문자를 대신한다.

**검색 패턴** : 문자나 와일드카드 또는 이 두 개의 조합으로 구성된 검색 조건

```sql
SELECT 컬럼명
FROM 테이블명
WHERE 컬럼명 LIKE 검색 패턴;
```



## 7. 계산 필드 생성하기

**필드** : 기본적으로는 컬럼과 같은 뜻이며, 종종 서로 바꿔가면 부르기도 한다. 하지만 데이터베이스 컬럼은 일반적으로 컬럼이라고 부르며, 필드란 용어는 보통 계산 필드와 함께 사용된다.

**연결하기** : 한 개의 긴 값을 만들기 위해 여러 개의 값을 합치는 것

### 7-1. 필드 연결하기

```mysql
SELECT Concat(컬럼명1, 컬럼명2)
FROM 테이블명;
```

### 7-2. 별칭 사용하기

```mysql
SELECT 컬럼명1 연산자 컬럼명2
	AS 별칭 이름
FROM 테이블명;
```

### 7-3. 수학 계산 수행하기

**SQL 산술 연산자**

| 연산자 | 설명   |
| ------ | ------ |
| +      | 더하기 |
| -      | 빼기   |
| *      | 곱하기 |
| /      | 나누기 |

```mysql
SELECT 컬럼명1 산술 연산자 컬럼명2
FROM 테이블명;
```



## 8. 데이터 조작 함수 사용하기

**호환** : 작성된 코드가 다양한 환경에서 동작하는 것

### 8-1. 함수 사용하기

- **문자 조작 함수**

  | 함수      | 설명                                    |
  | --------- | --------------------------------------- |
  | LOWER()   | 문자열을 소문자로 변환                  |
  | LTRIM()   | 문자열의 왼쪽에 있는 공백 문자를 삭제   |
  | RTRIM()   | 문자열의 오른쪽에 있는 공백 문자를 삭제 |
  | SOUNDEX() | 문자열의 SOUNDEX 값을 반환              |
  | UPPER()   | 문자열을 대문자로 변환                  |

- **날짜와 시간 조작 함수** : 날짜-시간 조작 함수는 특정 DBMS에 종속적

- **숫자 조작 함수**

  | 함수   | 설명                         |
  | ------ | ---------------------------- |
  | ABS()  | 숫자의 절대 값을 반환한다.   |
  | COS()  | 숫자의 코사인 값을 반환한다. |
  | EXP()  | 숫자의 지수 값을 반환한다.   |
  | PI()   | 숫자의 파이 값을 반환한다.   |
  | SIN()  | 숫자의 사인 값을 반환한다.   |
  | SQRT() | 숫자의 제곱근을 반환한다.    |
  | TAN()  | 숫자의 탄젠트 값을 반환한다. |



## 9. 데이터 요약

### 9-1. 그룹 함수 사용하기

```sql
SELECT 그룹 함수(컬럼명)
FROM 테이블명;
```

**SQL 합계 함수**

| 함수    | 설명                            |
| ------- | ------------------------------- |
| AVG()   | 컬럼의 평균값을 반환한다.       |
| COUNT() | 컬럼에 있는 행 개수를 반환한다. |
| MAX()   | 컬럼의 최대 값을 반환한다.      |
| MIN()   | 컬럼의 최소 값을 반환한다.      |
| SUM()   | 컬럼의 합계를 반환한다.         |

중복되는 값을 제거하기 위해 DISTINCT라는 인자를 쓴다(ALL이 기본값이기 때문에 아무 인자를 주지 않으면 ALL로 인식한다).



## 10. 데이터 그룹핑

### 10-1. 그룹 생성하기

```sql
SELECT 컬럼명
FROM 테이블명
GROUP BY 그룹핑하는 컬럼명;
```

- GROUP BY절에 중첩된 그룹이 있다면, 데이터는 가장 마지막에 지정된 그룹에서 요약된다. 즉, 지정된 컬럼은 그룹핑될 때 같이 측정된다(그래서 각 컬럼 단위로는 데이터를 얻지 못한다).
- GROUP BY에 있는 컬럼은 가져오는 컬럼이거나, 그룹 함수는 아니면서 유효한 수식이어야 한다. SELECT 안에서 수식을 사용한다면, GROUP BY에도 같은 수식을 사용해야 한다. 별칭은 사용할 수 없다.
- 대부분의 SQL 실행 환경에서는 GROUP BY절에서 문자나 메모와 같은 가변형 길이의 데이터형은 사용할 수 없다.
- 그룹 함수 구문을 제외하고 SELECT문에 있는 모든 컬럼은 GROUP BY절에 존재해야 한다.
- 그룹핑하는 컬럼의 행에 NULL 값이 있다면, NULL도 그룹으로 가져온다. 여러 행이 NULL 값을 가진다면, 모두 함께 그룹화된다.

### 10-2. 그룹 필터링

```sql
SELECT 컬럼명
FROM 테이블명
GROUP BY 그룹핑하는 컬럼명
HAVING 필터링 조건;
```

### 10-3. 그룹핑과 정렬

**ORDER BY와 GROUP BY 비교**

| ORDER BY                                              | GROUP BY                                                     |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| 결과를 정렬한다.                                      | 행을 그룹핑한다. 결과는 그룹 순서대로 출력되지 않을 수 있다. |
| 어떤 컬럼이라도(가져오지 않는 컬럼도) 사용할 수 있다. | 가져오는 컬럼이나 수식 컬럼을 사용할 수 있고 선택된 모든 컬럼 수식을 사용해야 한다. |
| 필수 항목은 아니다.                                   | 그룹 함수와 함께 사용하는 컬럼(또는 수식)이 있는 경우 필수 항목이다. |

- GROUP BY절을 사용할 때마다 ORDER BY절을 명시해야 한다.

### 10-4. SELECT절 순서

**SELECT절과 순서**

| 절       | 설명                   | 필수                                           |
| -------- | ---------------------- | ---------------------------------------------- |
| SELECT   | 가져올 컬럼이나 수식   | Yes                                            |
| FROM     | 데이터를 가져올 테이블 | 테이블에서 데이터를 가져오려면 사용한다.       |
| WHERE    | 행 레벨 필터링         | No                                             |
| GROUP BY | 그룹 지정              | 그룹핑한 데이터에 집계 계산을 한다면 사용한다. |
| HAVING   | 그룹 레벨 필터링       | No                                             |
| ORDER BY | 정렬 순서              | No                                             |



## 11. 서브쿼리 사용하기

**쿼리** : 모든 SQL 구문. 하지만 쿼리라는 용어는 보통 SELECT문을 참조할 때 사용한다.

### 11-1. 서브쿼리로 필터링하기

```sql
SELECT 컬럼명
FROM 테이블명
WHERE 컬럼명 연산자 (SELECT 컬럼명
               FROM 테이블명
               WHERE 컬럼명 연산자 값);
```

### 11-2. 계산 필드로 서브쿼리 사용하기

```sql
SELECT 컬럼명,
			(SELECT COUNT(*)
             FROM 테이블명
            ) AS 별칭 이름
FROM 테이블명;
```



## 12. 테이블 조인

**확장성** : 증가하는 양의 데이터를 적절히 처리하는 것. 잘 설계된 데이터베이스나 애플리케이션은 확장성이 좋다고 말한다.

### 12-1. 조인 생성하기

- **내부 조인(동등 조인 혹은 이퀴 조인)**

  ```sql
  SELECT 컬럼명
  FROM 테이블명1, 테이블명2
  WHERE 테이블명1.연결 가능한 컬럼명 x = 테이블명2.연결 가능한 컬럼명 x;
  ```

  ```sql
  SELECT 컬럼명
  FROM 테이블명1 INNER JOIN 테이블명2
  ON 테이블명1.연결 가능한 컬럼명 x = 테이블명2.연결 가능한 컬럼명 x;
  ```



## 13. 고급 테이블 조인 생성하기

### 13-1. 테이블 별칭 사용하기

```sql
SELECT 컬럼명
FROM 테이블명1 AS 별칭 이름1 INNER JOIN 테이블명2 AS 별칭 이름2
ON 별칭 이름1.연결 가능한 컬럼명 c = 별칭 이름2.연결 가능한 컬럼명 c;
```

### 13-2. 다른 조인 타입 사용하기

- **셀프 조인**

  ```sql
  SELECT 컬럼명
  FROM 테이블명 t AS 별칭 이름1, 테이블명 t AS 별칭 이름2
  WHERE 별칭 이름1.컬럼명 c = 별칭 이름2.컬럼명 c;
  ```

- **자연 조인**

  ```sql
  SELECT 별칭 이름1.*, 별칭 이름2.중복되지 않는 컬럼명
  FROM 테이블명 t AS 별칭 이름1, 테이블명 t AS 별칭 이름2
  WHERE 별칭 이름1.컬럼명 c = 별칭 이름2.컬럼명 c;
  ```

- **외부 조인**

  ```sql
  SELECT 테이블명1.컬럼명1, 테이블명2.컬럼명2
  FROM 테이블명1 LEFT OUTER JOIN 테이블명2
  ON 테이블명1.연결 가능한 컬럼명 c = 테이블명2.연결 가능한 컬럼명 c;
  ```

- 그룹 함수는 조인과 함께 사용할 수 있다.



## 14. 쿼리 결합하기

### 14-1. 결합 쿼리 이해하기

기본적으로 결합 쿼리를 사용하는 두 가지 경우의 시나리오가 있다.

- 여러 테이블에 있는 비슷한 구조의 데이터를 하나의 쿼리로 가져오는 경우
- 한 개의 테이블에서 여러 개의 쿼리를 수행하고, 하나의 결과로 가져오는 경우

### 14-2. 결합 쿼리 만들기

- **UNION 사용하기**

  ```sql
  SELECT 컬럼명
  FROM 테이블명
  WHERE 컬럼명 연산자 값
  UNION
  SELECT 컬럼명
  FROM 테이블명
  WHERE 컬럼명 연산자 값;
  ```

- **UNION 규칙**

  - UNION에서 각 쿼리는 같은 컬럼이나 수식, 그룹 함수를 가져야 한다(일부 DBMS는 심지어 컬럼의 순서까지 맞춰야 한다).
  - 컬럼 데이트형은 호환될 수 있다. 정확히 같은 데이터형일 필요는 없지만, DBMS가 내부적으로 변환할 수 있어야 한다(예를 들면 다른 숫자형이나 다른 날짜형).

- **중복 행 포함하기와 제거하기**

  ```sql
  SELECT 컬럼명, 컬럼명 c
  FROM 테이블명
  WHERE 컬럼명 연산자 값
  UNION ALL
  SELECT 컬럼명, 컬럼명 c
  FROM 테이블명
  WHERE 컬럼명 연산자 값;
  ```

- **결합 쿼리 결과 정렬하기**

  - UNION으로 쿼리를 결합할 때는 딱 하나의 ORDER BY절을 사용할 수 있는데, 이때 이 ORDER BY절은 마지막 SELECT 구문 뒤에 와야 한다.



## 15. 데이터 삽입하기

### 15-1. 행 삽입하기

```sql
INSERT INTO 테이블명(컬럼명,
                ...)
VALUES(값,
      ...);
```

### 15-2. 쿼리 결과 삽입하기

```sql
INSERT INTO 테이블명(컬럼명,
                ...)
SELECT 컬럼명,
	...
FROM 테이블명;
```

### 15-3. 다른 테이블로 복사하기

```sql
CREATE TABLE 새로운 테이블명 AS
SELECT * FROM 테이블명;
```



## 16. 데이터 업데이트와 삭제

### 16-1. 데이터 업데이트

- 테이블에 있는 특정 행 업데이트

  ```sql
  UPDATE 업데이트할 테이블
  SET 컬럼명 = 새로운 값
  WHERE 어떤 행이 업데이트되어야 하는지를 지정하는 필터 조건;
  ```

- 테이블에 있는 모든 행 업데이트

  ```sql
  UPDATE 업데이트할 테이블
  SET 컬럼명 = 새로운 값;
  ```

- 컬럼 값을 삭제하려면 컬럼에 NULL을 설정하면 된다.

### 16-2. 데이터 삭제

- 테이블에 있는 특정 행 삭제

  ```sql
  DELETE FROM 데이터를 삭제할 테이블명
  WHERE 어떤 행이 삭제되어야 하는지를 지정하는 필터 조건;
  ```

- 테이블에 있는 모든 행 삭제

  ```sql
  DELETE FROM 데이터를 삭제할 테이블명;
  ```



## 17. 테이블 생성과 조작

### 17-1. 테이블 생성

- **기본 테이블 생성**

  ```sql
  CREATE TABLE 새로운 테이블명
  (
      컬럼명 데이터형 제약 조건,
      ...
  );
  ```

- **기본값 지정하기**

  ```sql
  CREATE TABLE 새로운 테이블명
  (
      컬럼명 데이터형 제약 조건 DEFAULT 기본값,
      ...
  );
  ```

### 17-2. 테이블 변경하기

```sql
ALTER TABLE 변경할 테이블명
변경할 사항;
```

### 17-3. 테이블 삭제하기

```sql
DROP TABLE 테이블명;
```



## 18. 뷰 사용하기

**뷰** : 뷰는 가상 테이블이다. 데이터를 저장하는 대신 필요할 때마다 데이터를 가져올 수 있는 쿼리를 저장하고, SQL SELECT 구문을 여러 단계로 캡슐화 할 수 있다. 또 뷰는 데이터 조작을 단순화하는 것 외에 가져오는 데이터의 형식을 변경하거나 보호할 때도 사용한다.

### 18-1. 뷰 생성하기

- **복잡한 조인을 단순화하기 위한 뷰 생성하기**

  ```sql
  CREATE VIEW 뷰 이름 AS
  SELECT 컬럼명
  FROM 테이블명1, 테이블명2, 테이블명3
  WHERE 테이블명1.연결 가능한 컬럼명 c1 = 테이블명2.연결 가능한 컬럼명 c1
  AND 테이블명3.연결 가능한 컬럼명 c2 = 테이블명2.연결 가능한 컬럼명 c2;
  ```

- **가져온 데이터의 형식을 변경하기 위해 뷰 사용하기**

  ```mysql
  CREATE VIEW 뷰 이름 AS
  SELECT Concat(컬럼명1, 컬럼명2)
  	AS 별칭 이름
  FROM 테이블명;
  ```

- **원하지 않는 데이터를 필터링하기 위해 뷰 사용하기**

  ```sql
  CREATE VIEW 뷰 이름 AS
  SELECT 컬럼명
  FROM 테이블명
  WHERE 컬럼명 연산자 값;
  ```

- **계산 필드와 함께 뷰 사용하기**

  ```sql
  SELECT 컬럼명1 연산자 컬럼명2 AS 별칭 이름
  FROM 테이블명;
  ```