# MySQL3
### 1. MySQL에서 between과 not between 사용법
- MySQL에서 숫자들 사이의 값을 between으로 나타낼수 있다. 아래와 같이 사용가능하다.
- select * from TABLE where 컬럼명 between 숫자 and 숫자;
- select * from TABLE where 컬럼명 not between 숫자 and 숫자;
- 이때 숫자~숫자 사이의 값들을 가져오는데, 이상과 이하 즉, 그 숫자를 포함하고, 그 사이의 값들을 가져온다. not beetween a and b 는 숫자 사이에 없는 값들을 가져온다.

### 2. MySQL에서 in과 not in 사용법
- MySQL에서는 리스트가 없다. 그래서 여러개의 값들이 포함 된 값을 가져올때는 in연산자를 사용하여 가져온다. 아래와 같이 사용 가능하다. 
- select * from TABLE where 컬럼명 in (값, 값, 값, 값);
- select * from TABLE where 컬럼명 not in (값, 값, 값, 값, 값);
- 이때, 값이 들어있는 데이터 들만 가져오며, not in 사용시 그 값들을 포함하지 않는 데이터들을 가져온다.

### 3. MySQL에서 Case End 조건식 사용법
- MySQL에서 조건문 사용시 Case End 조건문을 많이 사용한다. 이때, Case End 조건문은 컬럼을 나타내며 아래와 같이 사용가능하다.

select 컬럼명, 컬럼명,

  case
  
    when 컬럼명 (조건문)    
    	then 조건 만족시 새로운 컬럼 데이터의 값    
    else 조건 만족하지 않을시 새로운 컬럼 데이터의 값      
	end as 새로 만들 컬럼명
	
from TABLE;
- 이 때, case ~ end 사이에 when을 사용해 조건문을 입력해준다. 예를들면, when 컬럼 >= 2000과 같이 입력하면 2000이상인 컬럼들의 데이터를 가져온다. 2000이상인 데이터를 가져오면 then 뒤에다가 그 데이터를 어떻게 저장할지 입력한다. 만약 2000이상이 현대이고, 아니면 과거라고 할때, when 컬럼 >= 2000 then 현재 else 과거 라고 작성하면된다.

### 4. MySQL에서 조인문 만드는 방법
- join문은, 두개 이상의 테이블을 합칠 때 사용한다.

select *
from TABLE1 1

join TABLE2 2
	on 1.id = 2.id
	
- 위와 같이 사용 가능하며 보통 id라는 값을 중복되게 해서 공유하는데, 이때 유니크한 id의 값을 얻기위해선 on을 사용해준다.
- join한 TABLE들을 계속해서 불러오면 작업하는데 복잡해지므로 TABLE1 1과 같이 테이블 뒤에 이름을 지어준다. 여기서 TABLE1은 이름이 1이고, TABLE2는 2이다.
- 3개 이상의 TABLE을 합치기 위해선 위를 참고해, 아래와 같이 사용하면 된다.
- 
select *
from TABLE1 1

join TABLE2 2
	on 1.id = 2.id
	
join TABLE3 3
	on 1.id = 3.id
	
- 또한, null값 즉, 비어있는 값이 있는 TABLE의 값까지 합치려고 한다면, join 앞에 left를 붙여, left join과 같이 사용해주면 된다.	

### 5.여러 테이블 설계 시 foreign key 사용법
- 위의 4번설명에서 보통 id의 값들을 중복되게해서 설계한다고 했다.
- 이때, 테이블을 설계할때 foreign key를 사용하는데, 말 그대로 외부 키이다. 외부 TABLE과 연결시켜 줄 컬럼을 설계한다.
- 보통 references 와 같이 사용하며, 이해하기 쉽게 설명하면, foreign key가 컬럼을 연결 한다면, references는 TABLE과 연결해 준다. 아래와 같이 사용 가능하다.

create table TABLE1(
	id int auto_increment primary key,
    컬럼1,
    컬럼2,
    );


create table TABLE2(
	id int auto_increment primary key,
    컬럼1,
    컬럼2,
    );


create table TABLE3(
	id int auto_increment primary key,
    컬럼1,
    컬럼2,
    
    1_id int,
    2_id int,
    foreign key (1_id) references TABLE1(id),
    foreign key (2_id) references TABLE2(id)
    );

- 이때, TABLE3를 보면 1_id와, 2_id가 있다. 여기서 1_id는 TABLE1에 있는 id와, 2_id는 TABLE2에 있는 id와 연결 되었다고 볼 수 있다.

### 6. MySQL의 ifnull()함수, if()함수 사용법
- 모든 데이터가 완벽한 것이 아니고, 비어있는 값들이 있는 데이터가 있다. 비어있는 값들을 null값이라고 한다. 이때, ifnull함수를 사용할 수 있는데, 어떤 컬럼의 null값을 지정한 값으로 채워주는 동작을 한다. 아래와 같이 사용 가능하다.
select ifnull(컬럼명, 0)
from TABLE;

- 위와 같이 사용시 TABLE에서 select한 컬럼에 비어있는 값, 즉 null값이 있을 경우, 0으로 채운 후 데이터를 가져온다.
- 0 말고 다른 데이터로도 채울 수 있다.

- if() 함수 또한 존재한다. CASE-END 조건문과 같은 조건문이다. if 조건문 또한 CASE-END조건문 처럼 컬럼을 나타낸다. 아래와 같이 사용 가능하다.
select 
	if(조건문, 참일경우 값, 거짓일경우 값) as 만들 컬럼명
from TABLE;
