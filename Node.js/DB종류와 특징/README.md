# DB의 종류와 특징

과거엔 계층형, 네트워크 이런 데이터베이스들이 있었고, 최근들어 Graph 이런 데이터베이스까지도 등장했다.

하지만 현재 실제 웹서비스 개발시 이용하는 데이터베이스는 대부분 **관계형 데이터베이스, NoSQL 데이터베이스**이다.

### 1. 관계형(Relational) 데이터베이스

**정의**

관계형 데이텁이스는 짧게 요약하면 엑셀처럼 행과 열로 데이터를 저장할 수 있는 데이터베이스를 뜻한다.

엑셀의 시트처럼 생긴 테이블이라고 부르는 공간을 하나 생성한 다음 행과 열에 맞춰 데이터를 쭉 저장한다.

![image](https://user-images.githubusercontent.com/98325285/174443598-7ae0c694-0306-4284-96b3-fbd75aa1b28a.png)

**특징**

- 거의 모든 곳에 사용할 수 있어 범용적이다.
- 구조화된 데이터를 저장하기 가장 좋다.
- 보통 SQL이라는 언어를 이용해 데이터를 출력 입력한다.
- 해당 열에 어떤 정보가 들어오는지 스키마를 미리 정의하기 때문에 관리가 쉽다.
- 구조화된 데이터 덕분에 원하는 데이터 뽑기도 쉽다.
- 트랜젝션 롤백 이런 기능을 이용해 데이터의 무결성을 보존하기 쉽기 때문에 금융, 거래 서비스에 필수다.

**Relational이란?**

데이터를 간의 관계를 정해서 데이터를 저장할 수 있다라는 뜻이다.

예를 들어 학교를 운영하는데 학교 선생님들과 가르치는 과목 정보를 DB에 저장하려고 한다.

![image](https://user-images.githubusercontent.com/98325285/174443587-5ab36649-f8cb-4f96-bb60-9bd7bda71a73.png)

선생님들마다 가르치는 과목을 이렇게 저장할 수 있다.

만약 손흥민 선생님이 가르치는 과목이 많아지면 어떻게 DB에 저장하는 게 좋을까?

![image](https://user-images.githubusercontent.com/98325285/174443628-e4b77491-7c1e-4a1e-a760-fec7274c75e0.png)

위와 같이 저장하면 데이터를 꺼내쓸 때 문제가 발생한다.

손흥민 선생님 행을 하나 더 만들어도 문제가 발생한다. 번호 중복이 일어날 것이다.

이것이 **테이블 형 데이터베이스의 단점인데, 데이터가 3차원으로 늘어나게 되면 2차원의 데이블내에서 제대로 표현할 수가 없게 된다.**

그래서 테이블을 하나 더 만든 후 테이블 간의 관계를 지어준다.

![image](https://user-images.githubusercontent.com/98325285/174443651-8a7e2fe2-e639-4a56-bd06-0eacdb7c7ba9.png)

이런 식으로 테이블을 하나 더 만들어서 왼쪽에는 선생님 관리 테이블, 오른쪽에는 과목 관리하는 테이블을 만들어준다. 그리고 과목에 선생님 번호를 적어서 어떤 선생님이 가르치는지 관계를 지어준다.

이게 관계형 데이터베이스의 특징이자 구축방법이다.

관계의 종류도 있는데

- one to one, one to many, many to many

이런 관계들이 있다.

### 2. NoSQL 데이터베이스

**정의**

SQL문 없이도 사용할 수 있는 데이터베이스라고 보면 된다.

대부분 테이블에 국한되지 않고 자유로운 형식으로 데이터를 쉽게 분산저장할 수 있다.

![image](https://user-images.githubusercontent.com/98325285/174443684-1aaaeed0-eae5-42dc-92cc-207f02c9d102.png)

**종류**

1. key-value 모델 : Object, JSON 자료형 형식으로 데이터를 쉽게 저장, 출력이 가능하다. 가장 심플하다.
2. Document 모델 : 테이블 대신 Collection이라는 문서 기반으로 데이터를 분류하고 저장한다. 테이블보다는 훨씬 유연하다.

   (MongoDB도 Key-value, Document 모델 저장방식을 차용하고 있다.)

3. Graph 모델 : 데이터를 노드의 형태로 저장하고 노드간의 흐름 또는 관계를 저장할 수 있다.
4. Wide-column 모델 : 한 행마다 각각 다른 수, 다른 종류의 열을 가질 수 있다.(스키마가 자유롭다.)

**특징**

1. Scaling이 쉽다.

   찰나의 순간 대량의 데이터를 저장해야한다면 어떻게 할까

   기존 올드한 관계형 데이터베이스는 확장이 매우 어렵다. 보통 sacle up이라는 방법으로 **서버의 성능을 키워야**한다.

   하지만 대부분 NoSQL 데이터베이스는 scale out이라는 방법으로 데이터를 **분산저장**하는 걸 기본적으로 지원한다.

   대량의 데이터를 빠르게 입출력해야한다면 NoSQL이 제격이다.

   (관계형 데이터베이스도 요즘은 분산저장이 어느정도 가능하다.)

2. 대부분 다루기가 쉽다.

   SQL이라는 언어를 새로 배우지 않아도 데이터를 쉽게 입출력할 수 있다.

   자바스크립트 object{ } 자료형 다루듯이 데이터를 입출력할 수 있어서 사용자에게 매우 편리하다.

   그리고 서버에서 쓰던 프로그래밍 언어로 DB를 다룰 수 있다는 장점이 있다.

3. 대부분 스키마 정의 없이도 쉽게 쓸 수 있다.

   장점이자 단점일 수 있다. 그래서 MongoDB에서는 스키마를 미리 정의하기 위한 Mongoose같은 라이브러리를 추가해서 사용하기도 한다.

4. NoSQL 데이터베이스는 기본적으로 SQL에서의 JOIN 연산을 적용하는 게 기본적으로 어렵다.

   서버 단에서 JOIN 연산을 쉽게 처리해주는 라이브러리를 이용한다.

relation 데이터베이스의 문제도 나름 쉽게 해결할 수 있다.

![image](https://user-images.githubusercontent.com/98325285/174443707-3f1de549-c0d5-4354-a741-9a94d042967b.png)

여기서 손흥민 선생님이 가르치는 과목이 수학, 영어 이렇게 2개로 늘어나면 NoSQL인 MongoDB에서는 그냥 [’수학’, ‘영어'] 이걸 array로 만들어서 저 자리에 그냥 집어넣으면 된다.

MongoDB는 DB에 array, object 집어넣는 건 자유이다.

**물론 MongoDB에서도 relational database처럼 관계를 표현해 저장하기도 한다.**

또 다른 예로 게시물을 만들었는데 거기에 달린 댓글을 저장할 때는 어떻게 하면 좋을까

간단하게 보면 게시물 document 안에 댓글란을 만들면 된다.

![image](https://user-images.githubusercontent.com/98325285/174443745-c1380027-79cd-4a27-b07f-3e630a78cf21.png)

하지만 게시물 하나가 댓글이 1억개가 되면 문제가 생긴다.

MongoDB document 하나의 최대 용랑은 16mb이기 때문이다.

![image](https://user-images.githubusercontent.com/98325285/174443753-3c3dce83-a9cc-44fc-882a-16bec460bf27.png)

이런 식으로 댓글용 collection(table)을 하나 더 만드는 게 더 좋은 방법이라고 생각한다.

댓글만 전부 모아놓는 곳에 게시물 번호를 지정하여 나중에 게시물의 댓글을 불러오고 싶을 때 해당 게시물의 번호인 댓글만 불러오면 된다.

MongoDB도 이런 식으로 관계형으로 개발하면 편리할 수 있다.

두 데이터베이스가 공존하는 이유는 각각의 명확한 장점 때문이다.

정규화된 데이터와 안정성이 필요하다면 관계형 데이터베이스를 사용한다.

금융서비스를 만들거나 은행 전산시스템을 만든다면 안정적인 관계형이 더 적합하다.

하지만 일초에 수백만개의 데이터 입출력 요청이 들어오는 SNS 서비스를 만들 때, 뭔가 서비스의 변경사항이 잦아서 쉽고 유연하게 데이터를 저장하고 싶으면 NoSQL을 사용한다.

실제로 Facebook은 이런 대량의 데이터를 저장하기 위해 HBase 데이터베이스를 이용해 분산저장한다.
