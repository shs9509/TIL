## SQL

비절차적 언어 



### DDL (Data Definition Language)

데이터 정의 언어 

생성, 수정, 삭제



- Create

  ```sqlite
  create table book (
  	id 	int primary key,
      name char,
      price int not null
  );
  ```

- Alter

  ```sqlite
  alter table book rename cloumn name to book_name;
  alter table book add(author char);
  ```

- Drop

  ```sqlite
  drop table book;
  ```

- Truncate

  ```sqlite
  truncate table book;
  ```

  이거는 테이블만 남기고 남은 데이터를 모두 삭제한다.



### DML (Data Manipulation Language)

데이터 조작언어

데이터의 레코드를 조회하거나 수정, 삭제



- Select

  ```sqlite
  select *
  from book
  where id = 1
  limit 3;
  ```

  ORM

  ```sh
  Book.objects.filter(id=1)[:3]
  ```

- Insert

  ```sqlite
  insert into book(id, name, price, author) values(4,'개미',23000,'베르나르');
  ```

- Update

  ```sqlite
  update book
  set price = 30000
  where id = 4;
  ```

- Delete

  ```sqlite
  delete 
  from book 
  where id = 4;
  ```

  



### DCL (Data Control Language)

데이터 제어언어

데이터 베이스에 접근과 객체에 권한을 주는 역할



- Grant

- Revoke

- Commit

- Rollback

  

