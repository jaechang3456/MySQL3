# MySQL3
### 1. MySQL에서 between과 not between 사용법
- MySQL에서 숫자들 사이의 값을 between으로 나타낼수 있다. 아래와 같이 사용가능하다.
- select * from TABLE where 컬럼명 between 숫자 and 숫자;
- select * from TABLE where 컬럼명 not between 숫자 and 숫자;
- 이때 숫자~숫자 사이의 값들을 가져오는데, 이상과 이하 즉, 그 숫자를 포함하고, 그 사이의 값들을 가져온다. not beetween a and b 는 숫자 사이에 없는 값들을 가져온다.

### 2. MySQL에서 in과 not in 사용법
- MySQL에서는 리스트가 없다. 그래서 여러개의 값들이 포함 된 값을 가져올때는 in연산자를 사용하여 가져온다. 아래와 같이 사용 가능하다. 
- select * from TABLE where released_year in (값, 값, 값, 값);
- select * from TABLE where released_year not in (값, 값, 값, 값, 값);
- 이때, 값이 들어있는 데이터 들만 가져오며, not in 사용시 그 값들을 포함하지 않는 데이터들을 가져온다.

### 3. MySQL에서 Case End 조건식 사용법
- MySQL에서 조건문 사용시 Case End 조건문을 많이 사용한다. 이때, Case End 조건문은 컬럼을 나타내며 아래와 같이 사용가능하다.
select 컬럼명, 컬럼명,
  case
  
    when 컬럼명 >= 2000 then 조건 만족시 새로운 컬럼 데이터의 값
      else 조건 만족하지 않을시 새로운 컬럼 데이터의 값
	end as 새로 만들 컬럼명
	
from TABLE;
- 이 때,
