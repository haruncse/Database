## Stored-Procedure

![Figure 1](https://github.com/haruncse/Stored-Procedure/blob/master/Figure1.jpg)

![Figure 2](https://github.com/haruncse/Stored-Procedure/blob/master/Figure2.jpg)

``` Oracle SQL
create table person_info
(
pid number,
pname varchar(20),
paddress varchar(20)
);

insert into person_info values(1,'Rahim','Dhaka');
insert into person_info values(2,'Karim','Khulna');
insert into person_info values(3,'Rafiq','Bogra');

create table person_parent_info
(
pid number,
pfname varchar(20),
pmname varchar(20)
);

insert into person_parent_info values(1,'Salim','XXXXX');
insert into person_parent_info values(2,'Reza','YYYYY');
insert into person_parent_info values(3,'Tuhin','ZZZZZ');

create table person_academic_info
(
pid number,
psscgpa float,
phscgpa float,
pmobn number
);

insert into person_academic_info values(1,4.59,5.00,015698);
insert into person_academic_info values(2,5.00,5.00,01552);
insert into person_academic_info values(3,4.98,4.55,0171556);

select * from person_academic_info;
select * from person_parent_info;
select * from person_info;

create or replace procedure person(
    po_cur out sys_refcursor) is
begin
  open po_cur for
     select person_info.pid,person_info.pname,person_info.paddress,person_parent_info.pfname,
person_parent_info.pmname,person_academic_info.psscgpa,person_academic_info.phscgpa,
person_academic_info.pmobn from person_info
 inner join person_parent_info
on person_info.pid=person_parent_info.pid
inner join person_academic_info
on person_parent_info.pid=person_academic_info.pid;
end;
/

 var rc refcursor;
 exec person( :rc);
print rc;

create table t1(
id number,
name varchar2(10)
);

insert into t1 values(1,'abc');
insert into t1 values(2,'def');
insert into t1 values(3,'ghi');

create table t2(
id number,
name varchar2(10)
);

insert into t2 values(1,'abc');
insert into t2 values(2,'def');
insert into t2 values(3,'ghi');

create or replace procedure get_t1_and_t2(
    o_cur out sys_refcursor) is
begin
  open o_cur for
     select t1.id,t1.name from t1
     inner join t2
on t1.id=t2.id;
end;
/
```
