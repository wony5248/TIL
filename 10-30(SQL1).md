#### SQL 문법
* SELECT
```
SELECT 열_이름
	FROM 테이블_이름
	WHERE 조건식
	GROUP BY 열_이름
	HAVING 조건식
	ORDER BY 열_이름
	LIMIT 숫자
```
* USE - 스키마 선택
```
USE this_schema
```
* SELECT - 컬럼 지정
```
-- SELECT '컬럼명' FROM '테이블명'
SELECT table_num, table_name FROM table;

-- SELECT 와 FROM 사이에 *를 적으면 테이블의 모든 컬럼을 조회한다.
SELECT * FROM table;

-- 두 SQL은 동일한 기능을 한다.
SELECT * FROM this_schema.table;
SELECT * FROM table;
```
* WHERE - 조건 조회
```
SELECT * FROM table 
	WHERE table_num >= 5;
```
* BETWEEN - 범위 조회
```
SELECT * FROM table 
	WHERE table_num between 5 and 100;
```
* IN - 여러값 조회
```
SELECT * FROM table 
	WHERE table_num IN(1, 2, 3);

SELECT * FROM table
	WHERE table_num = 1 AND table_num = 2 AND table_num = 3
```
* LIKE 문자열의 일부 글자 검색
```
SELECT * FROM table WHERE table_name LIKE 'table___';

-- table 컬럼 값이 'table'로 시작하는 모든 데이터 조회
SELECT * FROM table WHERE table_name LIKE 'table%';

-- table 컬럼 값에 'table'이 들어가는 모든 데이터 조회
SELECT * FROM table WHERE table_name LIKE '%table%';
```
* ORDER BY - 조회된 데이터 정렬
```
SELECT * FROM table
  	WHERE table_id >= 164
	ORDER BY table_id DESC, table_name;
```
* LIMIT - 출력 개수 제한
```
SELECT * FROM table
	LIMIT 3;    		-- 상위 3건만 조회
SELECT * FROM table
	LIMIT 3, 2; 		-- 3번째 데이터부터 2건만 조회
	LIMIT 2 OFFSET 3; 	-- 위와 동일
```
* DISTINCT - 중복 데이터 제거
```
SELECT DISTINCT table_num
	FROM table;
```
* GROUP BY - 그룹화
```
SELECT table_num, SUM(amount) AS "합계"
	FROM table
  	GROUP BY table_num
  	ORDER BY table_num;
```
