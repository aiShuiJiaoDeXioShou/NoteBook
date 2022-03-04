~~~ mysql
-- 任务一：
-- 创建数据库
CREATE DATABASE `account`;

-- 打开数据库
use `account`;

-- 创建数据库的表
CREATE TABLE `AccountIncomeType`(
	id int not null PRIMARY KEY auto_increment,
	category VARCHAR(20)
);
CREATE TABLE `AccountIncome`(
	id int not null PRIMARY KEY auto_increment,
	category VARCHAR(20),
	money DOUBLE(5,2),
	date VARCHAR(20),
	remark VARCHAR(20)
);
CREATE TABLE `AccountOutlayType`(
	id int not null PRIMARY KEY auto_increment,
	category varchar(20)
);
CREATE TABLE `AccountOutlay`(
	id int not null PRIMARY KEY auto_increment,
	category varchar(20),
	money DOUBLE(5,2),
	date VARCHAR(20),
	remark VARCHAR(50)
);

-- 任务二：录入收入数据
INSERT INTO accountincometype(`category`) VALUES('工资');
INSERT INTO accountincometype(`category`) VALUES('奖金');
INSERT INTO accountincometype(`category`) VALUES('其他');

INSERT INTO accountOutlaytype(`category`) VALUES('吃饭');
INSERT INTO accountOutlaytype(`category`) VALUES('交通');
INSERT INTO accountOutlaytype(`category`) VALUES('书籍');
INSERT INTO accountOutlaytype(`category`) VALUES('娱乐');

INSERT INTO accountincome(`category`,`money`,`date`,`remark`)VALUES('工资',200.2,'2021年1月12号','工资收入');
INSERT INTO accountincome(`category`,`money`,`date`,`remark`)VALUES('奖金',200.2,'2021年1月12号','奖金收入');
INSERT INTO accountincome(`category`,`money`,`date`,`remark`)VALUES('其他',200.2,'2021年1月12号','其他收入');

INSERT INTO accountoutlay(`category`,`money`,`date`,`remark`)VALUES('吃饭',200.2,'2021年1月12号','吃饭');
INSERT INTO accountoutlay(`category`,`money`,`date`,`remark`)VALUES('交通',200.2,'2021年1月12号','交通');
INSERT INTO accountoutlay(`category`,`money`,`date`,`remark`)VALUES('书籍',200.2,'2021年1月12号','书籍');
INSERT INTO accountoutlay(`category`,`money`,`date`,`remark`)VALUES('娱乐',229.2,'2021年1月12号','娱乐');

-- 任务三:
-- 查询所有收入类别
SELECT category FROM accountIncometype;
-- 查询所有收入明细
SELECT `category`,`money`,`date`,`remark` FROM accountincome;
-- 查询所有收入汇总
SELECT Sum(`money`) FROM accountincome;
-- 按照类别汇总
SELECT Sum(`money`) FROM accountincome WHERE category='工资';
SELECT Sum(`money`) FROM accountincome WHERE category='奖金';
SELECT Sum(`money`) FROM accountincome WHERE category='其他';

-- 任务四：
-- 查询所有支出类别
SELECT category FROM accountoutlay;
-- 查询所有支出明细
SELECT `category`,`money`,`date`,`remark` FROM accountoutlay;
-- 查询所有支出汇总
SELECT Sum(`money`) FROM accountoutlay;
-- 按照类别汇总
SELECT Sum(`money`) FROM accountoutlay WHERE category='吃饭';
SELECT Sum(`money`) FROM accountoutlay WHERE category='交通';
SELECT Sum(`money`) FROM accountoutlay WHERE category='书籍';
SELECT Sum(`money`) FROM accountoutlay WHERE category='娱乐';
~~~

