# MYSQL

## Data Types :
- varchar is variable length data type
- char is fixed length datatype


## Commands

    insert into town1 (id,city,age) values 
      (1,"muz",18),
      (2,"muz",20);

    insert into town1 values(3,"muz",20);


    create table town1 (
      create table town1 (
            id int primary key,
      city varchar(20),
      age int,
      constraint age_check check (age >= 18 and city = "muz")
      );


    create table st2(
      age int check (age >= 10)
      );


    select id, city, age from town1;

    select distinct city from town1;	// not repeat same value

    select * from town1 where age < 20;	// Condition where clause

    select * from town1 where age < 20 and city = "muz";

    select * from town1 where age between 22 and 25;

    select * from town1 where city in ("muz");		// can give more than  1 city

    select * from town1 where age not in (22); 

    select * from town1 where age not in (22,21,23); 	// check more data as condition of same col

    select * from town1 limit 3;

    select * from town1 where age > 21 limit 3;

    select * from town1 order by age desc;

    select * from town1 order by age asc;

    select * from town1 order by age desc limit 3;



## Aggregate Functions :

    select max(age) from town1;

    select min(age) from town1;

    select sum(age) from town1;

    select avg(age) from town1;

    select count(age) from town1;




## Group By Clause :

    select city, count(totalPerson) from town2 group by city;

    select city,leaderName, count(totalPerson) from town2 group by 	city,leaderName;


    select city, count(totalPerson) 
    from town2
    group by city
    order by city;

    select city, count(totalPerson) 
    from town2
    group by city
    order by city desc;


## Having Clause :

    select mode, count(city)
    from payment 
    group by mode 
    having count(cus_id) > 105;


    select city from payment 
    where mode = "netbanking"
    group by city
    having max(cus_id) > 105
    order by cus_id asc;




## General Order :

    select columns
    from table_name
    where condition
    group by columns
    having condition
    order by columns asc;




## Note :
- for safe mode off 

		( set sql_safe_updates = 0; )



## Conclusion

- where puts condition on row
- having put condition on groups



## Table Related Queries : 

### Update : 

    update payment 
    set customer = 'jack' 
    where customer = 'eathan';

    update payment 
    set cus_id = cus_id - 100;


### delete : 

    delete from payment 
    where cus_id = 10;



## Foreign Key : 

    Foreign key table is child table
    primary key table is parent table


foreign key (courseID) references courde(id)

### Cascading in foreign key :

    create table student (
    id int primary key,
    coursed int,
    foreign key(courseId) references course(id)
    on delete cascade
    on update cascade 
    );

    create table teacher(
    id int primary key,
    name varchar(50),
    dept_id int,
    foreign key (dept_id) references dept(id) 
    on update cascade
    on delete cascade
    );


- foreign key cascade the table by change value in other table
[ 

        create table dept(
        id int primary key,
        name varchar(50)
        );

        insert into dept values (101,"english");
        insert into dept values (102,"science");
        insert into dept values (103,"maths");

        update dept set  id = 104 
        where id = 103; 

        select * from dept;

        create table teacher(
        id int primary key,
        name varchar(50),
        dept_id int,
        foreign key (dept_id) references dept(id) 
        on update cascade
        on delete cascade
        );



        insert into teacher (id,name,dept_id) values 
        (101,"bob",101),
        (102,"adam",102),
        (103,"donakd",103);

        select * from teacher;

]



## Alter command to change the schema : 

- alter will help to change design of table

### Add Column

    alter table std 
    add column age int;


### Delete column

      alter table std
      drop column age;


### rename table name

    alter table std
    rename to st;

### change column name and datatype

    alter table st
    change column roll id int ;

### change datatype or constraint

    alter table st
    modify course varchar2(20);

### adding new column and setting default value
    alter table st
    add column age int not null default 20;

### changing age datatype into varchar

    alter table st
    modify column age varchar(2);



### Drop 

    Delete the whole table 

    drop table teacher;



### Truncate

    Delete all data from the table

    truncate table town1;


### Delete :

    delete row from the table

    delete from st
    where marks < 400;



## Joins in SQL :

### 1) Inner Join (overlapping column value as result from table A and B)

[

    create table a(
    id int ,
    name varchar(20)
    );

    insert into a (id, name) values
    (101,"aman"),
    (102,"raman"),
    (103,"chaman"),
    (104,"madan");

    create table b(
    roll int ,
    name varchar(20),
    marks int
    );

    insert into b (roll, name, marks) values
    (101,"aman",100),
    (102,"raman",102),
    (103,"chaman",103),
    (104,"madan",105);


    select * from a 
    inner join b
    on a.id = b.roll;

]

### short the name of table 

    select * from a as aj
    inner join b as bj
    on aj.id = bj.roll;



### 2) outer Join  i) left join   ii)right join  iii) full join	

#### i) left join -> join all data of left table but match data of right table

      select * from a 
      left join b 
      on a.id = b.id;


#### ii) right join -> join all data of right table and left table matching data joins

    select * from a 
    right join b 
    on a.id = b.id;

#### iii) full -> return all record when there is a match in either left or right table

#### Note : in sql there is no full join command. so we use union

    select * from a
    left join b 
    on a.id = b.id
    union
    select * from a
    right join b
    on a.id = b.id;


### left exclusive join : means only left side table part

    select * from a
    left join b 
    on a.id = b.id
    where b.id is null;


### right exclusive join : means only left side table part

    select * from a
    right join b 
    on a.id = b.id
    where a.id is null;

### H.W) find left join and right join not the mid common join..

### Self join 

- It is a regular join but the table is joined with itself.

      create table emp(
      id int primary key,
      name varchar(20),
      manager_id int
      );

      insert into emp (id,name,manager_id) values
      (101,"adam",103),
      (102,"bob",104),
      (103,"casey", NULL),
      (104, "donald", 103);

      select * 
      from emp as a
      join emp as b
      on a.id = b.manager_id;


## Union

- it is used to combine the result-set of two or more select statements.

- gives UNIQUE records.

      select name from a
      union
      select name from b;


## SQL sub Queries (with where):

- A subquery or Inner query or a nested query is a query within another SQL query.

- it involved 2 select statements.

      select * from student;

      select avg(stud_age) from student;

      select stud_name 
      from student
      where stud_age > 20.833;


### Proper way to write sql sub Query

    select stud_name 
    from student
    where stud_age > (select avg(stud_age) from student);


## To find even data

    select stud_age from student
    where stud_age % 2 = 0;

## Specific group of data from table

    select stud_name, stud_age from student 
    where stud_age in (22,20);


### With Sub Queries

    select stud_name, stud_age from student 
    where stud_age in (select stud_age from student
    where stud_age % 2 = 0);



## sub Queries (with from) :

    select all from student
    where age = 22;

    select max(stud_id) 
    from (select * from student where stud_sem = 5) as temp;








