# sql
mariadb-호텔신라,샤넬

-호텔신라

CREATE TABLE member (
  id varchar(45) NOT NULL primary key,
  pw varchar(45),
  name varchar(45),
  age varchar(45),
  email varchar(200),
phone varchar(45),
  address varchar(200)
)CHARSET=UTF8MB4;

create table room(
room_no int not null primary key, 
type varchar(40), 
base_price int, 
add_price INT, 
base_person int, 
max_person int,
imgLink varchar(40)
)CHARSET=UTF8MB4;


create table reservation(
rsv_idx int auto_increment not null primary key, 
id varchar(45), 
room_no int, 
person varchar(5),
date_in DATE, 
date_out DATE, 
cash int, 
payment varchar(12) DEFAULT '미결제', 
FOREIGN KEY (id) REFERENCES member(id)
on update cascade on delete cascade, 
FOREIGN KEY (room_no) REFERENCES room(room_no)
on update cascade on delete cascade)CHARSET=UTF8MB4;


create table review(
review_no int auto_increment not null primary key, 
review_title varchar(100),
review_content varchar(200),
type varchar(45),
room_rating varchar(45),
id VARCHAR(45),
date_in DATE,
review_date timestamp default NOW(),
FOREIGN KEY (id) REFERENCES member(id)
on update cascade on delete CASCADE
)CHARSET=UTF8MB4;

alter table review auto_increment = 1; -- auto-increament값 초기화할때 사용

insert into room values(201, 'Member Exclusive', 102600, 10000, 2, 5, '../resources/images/room-201.jpg');
insert into room values(202, 'Rewards Urban Island', 104500, 20000, 2, 6, '../resources/images/room-202.jpg');
insert into room values(203, 'Rewards Morning Delights', 106400, 30000, 3, 7, '../resources/images/room-203.jpg');
insert into room values(204, 'Rewards Suite', 106400, 30000, 3, 7, '../resources/images/room-204.jpg');
insert into room values(205, 'Rewards In Room Delights', 106400, 30000, 3, 7, '../resources/images/room-205.jpg');


-샤넬

CREATE TABLE TBL_MEMBER(
	memberId VARCHAR(45) PRIMARY KEY,
	memberPw VARCHAR(45),
	memberAge int(3),
	memberGender VARCHAR(45),
	memberEmail VARCHAR(45),
	memberZipcode VARCHAR(45),
	memberAddress VARCHAR(45),
	memberAddressDetail VARCHAR(45),
	memberAddressEtc VARCHAR(45)
)CHARSET=UTF8MB4;

INSERT INTO TBL_MEMBER
(MEMBERID, MEMBERPW, MEMBERAGE, MEMBERGENDER, MEMBEREMAIL, MEMBERZIPCODE, MEMBERADDRESS, MEMBERADDRESSDETAIL, MEMBERADDRESSETC)
VALUES('hds1234', '1234', 20, '남자', 'ted@han.com', '12341', '서울시 강남구 역삼동', '100동 100호', '');

CREATE TABLE TBL_BOARD(
	boardNum int(38) auto_increment not null, 
	boardTitle VARCHAR(45),
	boardContent VARCHAR(45),
	boardId VARCHAR(45),
	boardDate timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
	readCount int(38) DEFAULT 0,
	CONSTRAINT PRIMARY KEY(boardNum),
	CONSTRAINT FK_BOARD_MEMBER FOREIGN KEY(boardId)
	REFERENCES TBL_MEMBER(memberId)
)CHARSET=UTF8MB4;

CREATE TABLE TBL_FILES(
	fileName VARCHAR(45),
	boardNum int(38),
	fileNameOriginal VARCHAR(45),
	CONSTRAINT FK_FILES_BOARD FOREIGN KEY(boardNum)
	REFERENCES TBL_BOARD(boardNum)
)CHARSET=UTF8MB4;

CREATE TABLE TBL_REPLY(
	replyNum int(38) auto_increment,
	boardNum int(38),
	memberId VARCHAR(45),
	replyContent VARCHAR(45),
	CONSTRAINT PRIMARY KEY(replyNum),
	CONSTRAINT FK_REPLY_BOARD FOREIGN KEY(boardNum)
	REFERENCES TBL_BOARD(boardNum) ON DELETE CASCADE
)CHARSET=UTF8MB4;

CREATE TABLE TBL_SHOOSE (
  sId varchar(45) NOT NULL PRIMARY KEY,
  sName varchar(45),
  sImg VARCHAR(200),
  sSize INT,
  sPrice INT,
  sStock INT,
  memberId varchar(45),
  FOREIGN KEY (memberId) REFERENCES TBL_MEMBER(memberId)
on update cascade on delete CASCADE
) CHARSET=UTF8MB4;

CREATE TABLE TBL_CART (
  cId int NOT NULL PRIMARY KEY AUTO_INCREMENT,
  cQuantity INT,
  cPriceAll INT,
  cPayment varchar(45) DEFAULT '미결제',
  cDate timestamp NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
  sId varchar(45),
  memberId varchar(45),
  FOREIGN KEY (memberId) REFERENCES TBL_MEMBER(memberId)
on update cascade on delete CASCADE,
  FOREIGN KEY (sId) REFERENCES TBL_SHOOSE(sId)
on update cascade on delete CASCADE
) CHARSET=UTF8MB4;

INSERT INTO `chanel`.`TBL_SHOOSE` (`sId`, `sName`, `sImg`, `sSize`, `sPrice`, `sStock`) VALUES ('sd6220', '테이턴트 카프스킨', '../assets/images/sandle/sandals6.jpg', '220', '1458000', '100');
INSERT INTO `chanel`.`TBL_SHOOSE` (`sId`, `sName`, `sImg`, `sSize`, `sPrice`, `sStock`) VALUES ('sd6230', '테이턴트 카프스킨', '../assets/images/sandle/sandals6.jpg', '230', '1458000', '100');
INSERT INTO `chanel`.`TBL_SHOOSE` (`sId`, `sName`, `sImg`, `sSize`, `sPrice`, `sStock`) VALUES ('sd6240', '테이턴트 카프스킨', '../assets/images/sandle/sandals6.jpg', '240', '1458000', '100');
INSERT INTO `chanel`.`TBL_SHOOSE` (`sId`, `sName`, `sImg`, `sSize`, `sPrice`, `sStock`) VALUES ('sd6250', '테이턴트 카프스킨', '../assets/images/sandle/sandals6.jpg', '250', '1458000', '100');
INSERT INTO `chanel`.`TBL_SHOOSE` (`sId`, `sName`, `sImg`, `sSize`, `sPrice`, `sStock`) VALUES ('sd6260', '테이턴트 카프스킨', '../assets/images/sandle/sandals6.jpg', '260', '1458000', '100');
INSERT INTO `chanel`.`TBL_SHOOSE` (`sId`, `sName`, `sImg`, `sSize`, `sPrice`, `sStock`) VALUES ('sd6270', '테이턴트 카프스킨', '../assets/images/sandle/sandals6.jpg', '270', '1458000', '100');
INSERT INTO `chanel`.`TBL_SHOOSE` (`sId`, `sName`, `sImg`, `sSize`, `sPrice`, `sStock`) VALUES ('sd6280', '테이턴트 카프스킨', '../assets/images/sandle/sandals6.jpg', '280', '1458000', '100');
INSERT INTO `chanel`.`TBL_SHOOSE` (`sId`, `sName`, `sImg`, `sSize`, `sPrice`, `sStock`) VALUES ('sd6290', '테이턴트 카프스킨', '../assets/images/sandle/sandals6.jpg', '290', '1458000', '100');















		



