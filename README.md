# ca105_assignment

# <center>INTERCITY EXPRESS TRAINS</center>

## Entity Relationship Diagram

<img
  src="/erDiagram.jpg"
  alt="Alt text"
  title="Optional title"
  style="display: inline-block; margin: 0 auto;width: 100%;height:100%;padding:10px">
<hr>

## Relations

Routes(Route_no,Route_name,time_taken,total_dist,Start_Stn,Start_time,End_Stn,End_time)
 
Stations(Station_code,Station_name,No_of_Platform,State)
 
Trains(Train_no,Train_name,Capacity,Route_no)
 
Coaches(coach_no,made_by,last_maintained,after_maintained_dist)
 
Active_Coaches(Coach_no,Train_no,Date)
 
Standby_Coaches(Coach_no,Date)
 
Maintainance(Maintain_no,Maintain_date,Maintain_type,Coach_no)
 
Tickets(Ticket_no,Train_no,Status,passenger_name,Age,Board_stn,drop_stn,date_of_journey,booking_date,fare,discount,
          travel_agent_id,agent_comm)
 
Travel_Agents(Travel_Agent_Id,Travel_Agent_Name,ADD,MOB,Email)
 
Staffs(Staff_no,Staff_name,Contact_no,residence_city)
 
Seats(Seat_no,Seat_type)
 
Staff_schedule(Route_no,Train_no,Driver_no,Remark,Time,Date,Accomodation)
 
Train_schedule(Route_no,Train_no,Station_code,Date,ETA,AAT,EDT,ADT)
 
Seat_allocated(Ticket_no,Coach_no,Seat_no,Seat_type,Date,Time)
 
Train_coaches(Train_no,Coach_no,Date_from)

```sql
create database intercity_express_trains;
```

```sql
create table active_coaches(coach_no varchar(10) primary key,train_no int,foreign key(train_no) references trains(train_no));
```
```sql
create table coaches(coach_no varchar(10) primary key,manufacturer varchar(50),last_maintained date,after_maintain_dist int,total_dist_covered int);
```
```sql
create table maintainance(maintain_no varchar(10) primary key,maintain_desc varchar(60),maintain_type varchar(20),active_coach_no varchar(10),foreign key(active_coach_no) references active_coaches(coach_no));
```
```sql
create table routes(route_no varchar(10) primary key,route_name varchar(30),time_taken time,total_dist_km int,start_stn varchar(10),start_time time,end_stn varchar(10),end_time time,foreign key(start_stn) references stations(station_no),foreign key(end_stn) references stations(station_no));
```
```sql
create table seat_allocated(ticket_no varchar(10),passenger_no varchar(10),coach_no varchar(10),seat_no int,Date date,Time time,foreign key(ticket_no) references tickets(ticket_no),foreign key(passenger_no) references passengers(passenger_no),foreign key(coach_no) references active_coaches(coach_no),foreign key(seat_no) references seats(seat_no),primary key(ticket_no,passenger_no,Date,Time));
```
```sql
create table staff_schedule(route_no varchar(10),train_no int,staff_no varchar(10),remark varchar(10),date date,time time,accomodation varchar(10),foreign key(route_no) references routes(route_no),foreign key(train_no) references trains(train_no),foreign key(staff_no) references staffs(staff_no),primary key(route_no,train_no,staff_no,date));
```
```sql
create table staffs(staff_no varchar(10) primary key,staff_name varchar(20),contact_no varchar(15),residence_city varchar(20));
```
```sql
create table standby_coaches(coach_no varchar(10) primary key);
```
```sql
create table stations(station_no varchar(10) primary key,station_name varchar(30),no_of_platform int,state varchar(20));

```
```sql
create table tickets(ticket_no varchar(10) primary key,status varchar(10),board_stn varchar(10),drop_stn varchar(10),date_of_journey date,booking_date date,fare float(2),travel_agent_id varchar(10),foreign key(board_stn) references stations(station_no), foreign key(drop_stn) references stations(station_no),foreign key(travel_agent_id) references travel_agents(travel_agent_id));
```
```sql
create table train_coaches(train_no int,coach_no varchar(10),date_from date,date_to date,foreign key(train_no) references trains(train_no),foreign key(coach_no) references active_coaches(coach_no),primary key(train_no,coach_no,date_from,date_to));

```
```sql
create table train_schedule(route_no varchar(10),train_no int,station_no varchar(10),Date date,EAT time,AAT time,EDT time,ADT time,foreign key(route_no) references routes(route_no),foreign key(train_no) references trains(train_no),foreign key(station_no) references stations(station_no),primary key(route_no,train_no,station_no,Date));
```
```sql
create table trains(train_no int primary key,train_name varchar(30),capacity int,route_no varchar(10) not null,foreign key(route_no) references routes(route_no));
```
```sql
create table travel_agents(travel_agent_id varchar(10) primary key,travel_agent_name varchar(30),address varchar(50),contactno varchar(15),email varchar(30));
```
```sql
create table seats(seat_no int primary key,type varchar(20));
```
<hr>

## Insert Statements

```sql
insert into trains(train_no,train_name,capacity,route_no) values ('22945','SAURASHTRA MAIL',90,"RT001"),('14553','HIMACHAL EXPRESS',90,"RT002"),('11019','KONARK EXPRESS',90,"RT003"),('22223','SHIRDI VANDEBHARAT EXPRESS',90,"RT004"),(11301,"UDYAN EXPRESS",90,"RT005"),(12715,"SACHKHAND EXPRESS",90,"RT006"),(19628,"AJMER SUPERFAST EXPRESS",90,"RT007"),(17325,"VISHWAMANAVA EXPRESS",90,"RT008"),(18234,"NARMADA EXPRESS",90,"RT009"),(10103,"MANDOVI EXPRESS",90,"RT010"),(13022,"MITHILA EXPRESS",90,"RT011"),('22946','SAURASHTRA MAIL',90,"RT014"),('14552','HIMACHAL EXPRESS',90,"RT015"),('11020','KONARK EXPRESS',90,"RT016"),('22222','SHIRDI VANDEBHARAT EXPRESS',90,"RT017"),(11302,"UDYAN EXPRESS",90,"RT018"),(12716,"SACHKHAND EXPRESS",90,"RT019"),(19627,"AJMER SUPERFAST EXPRESS",90,"RT020"),(17326,"VISHWAMANAVA EXPRESS",90,"RT021"),(18235,"NARMADA EXPRESS",90,"RT022"),(10102,"MANDOVI EXPRESS",90,"RT023"),(13021,"MITHILA EXPRESS",90,"RT024");

```
```sql
insert into stations( station_no, station_name, no_of_platform, state) values ('PUNE','Pune',6,'MAHARASHTRA'),("CSMT","MUMBAI",12,"MAHARASHTRA"),('JAM','GANDHINAGAR',10,"GUJARAT"),("ST","SURAT",6,"GUJARAT"),("SINA","SRINAGAR",7,"JAMMU-KASHMIR"),("SNSI","SAINAGAR SHIRDI TERMINUS",6,"MAHARASHTRA"),("SUR","SOLAPUR",5,"MAHARASHTRA"),("SOP","SHIVPUR",3,"MAHARASHTRA"),("VSG","GOA",8,"GOA"),("NDLS","NEW DELHI",15,"NEW DELHI"),("UHL","UNA HIMACHAL",7,"HIMACHAL PRADESH"),("LJN","LUCKNOW",12,"UTTAR PRADESH"),("SC","SECUNDERABAD",12,"ANDHRA PRADESH"),("VSKP","VISHAKHAPATNAM",20,"ANDHRA PRADESH"),("BSB","VARANASI",12,"UTTAR PRADESH"),("BPL","BHOPAL",5,"MADHYA PRADESH"),("INDB","INDORE",6,"MADHYA PRADESH"),("LNL","LONAVALA",4,"MAHARASHTRA"),("AII","AJMER",7,"RAJASTHAN"),("DWR","DHARWAD",6,"KARNATKA"),("SBC","BENGALURU",20,"KARNATKA"),("NGP","NAGPUR",9,"MAHARASHTRA"),("MFP","MUZAFFARPUR",8,"BIHAR"),("PNBE","PATNA",10,"BIHAR"),("RXL","RAXAUL",8,"BIHAR"),("BUI","BALLIA",6,"UTTAR PRADESH"),("GKP","GORAKHPUR",15,"UTTAR PRADESH"),("PRYJ","PRAYAGRAJ",8,"UTTAR PRADESH"),("HWH","HOWRAH",20,"WEST BENGAL"),("CNB","KANPUR",11,"UTTAR PRADESH");

```
```sql
INSERT INTO ROUTES (route_no,route_name,time_taken,total_dist_km,start_stn,start_time,end_stn,end_time) values("RT001","MUMBAI CENTRAL-GANDHINAGAR",'05:40:00',548,"CSMT",'09:00:00',"JAM",'14:40:00'),("RT014","GANDHINAGAR-MUMBAI CENTRAL",'05:40:00',548,"JAM",'16:40:00',"CSMT",'22:20:00'),("RT002","NEW DELHI-HIMACHAL",'06:10:00',412,"NDLS",'07:00:00',"UHL",'13:10:00'),("RT015","HIMACHAL-NEW DELHI",'06:10:00',412,"UHL",'16:10:00',"NDLS",'22:20:00'),("RT003","SECUNDERABAD-VISAKHAPATNAM",'08:30:00',500,"SC",'10:00:00',"VSKP",'18:30:00'),("RT016","VISAKHAPATNAM-SECUNDERABAD",'08:30:00',500,"VSKP",'21:30:00',"SC",'06:00:00'),("RT004","MUMBAI-SAINAGAR SHIRDI",'05:20:00',248,"CSMT",'11:40:00',"SNSI",'05:00:00'),("RT017","SAINAGAR SHIRDI-MUMBAI",'05:20:00',248,"SNSI",'07:00:00',"CSMT",'12:20:00'),("RT005","MUMBAI-SOLAPUR",'06:35:00',400,"CSMT",'08:25:00',"SUR",'15:00:00'),("RT018","SOLAPUR-MUMBAI",'06:35:00',400,"SUR",'17:00:00',"CSMT",'23:35:00'),("RT006","BHOPAL-DELHI",'07:45:00',700,"BPL",'20:15:00',"NDLS",'04:00:00'),("RT019","DELHI-BHOPAL",'07:45:00',700,"NDLS",'06:00:00',"BPL",'13:45:00'),("RT007","LONAVALA-AJMER",'10:45:00',1062,"LNL",'02:15:00',"AII",'13:00:00'),("RT020","AJMER-LONAVALA",'10:45:00',1062,"AII",'16:00:00',"LNL",'02:45:00'),("RT008","DHARWAD-BENGALURU",'05:00:00',432,"DWR",'05:00:00',"SBC",'10:00:00'),("RT021","BENGALURU-DHARWAD",'05:00:00',432,"SBC",'12:00:00',"DWR",'17:00:00'),("RT009","BHOPAL-INDORE",'03:00:00',246,"BPL",'21:15:00',"INDB",'00:15:00'),("RT022","INDORE-BHOPAL",'03:00:00',246,"INDB",'03:15:00',"BPL",'06:15:00'),("RT010","MUMBAI-GOA",'06:00:00',588,"CSMT",'03:00:00',"VSG",'09:00:00'),("RT023","GOA-MUMBAI",'06:00:00',588,"VSG",'12:15:00',"CSMT",'18:15:00'),("RT011","RAXAUL-HOWRAH",'17:50:00',691,"RXL",'10:10:00',"HWH",'04:00:00'),("RT024","HOWRAH-RAXAUL",'17:50:00',691,"HWH",'06:00:00',"RXL",'23:50:00');

```
```sql
insert into seats (seat_no,type) values (1,"LOWER"),(2,"MIDDLE"),(3,"UPPER"),(7,"S_LOWER"),(8,"S_UPPER"),(4,"LOWER"),(5,"MIDDLE"),(6,"UPPER"),(9,"LOWER"),(10,"MIDDLE"),(11,"UPPER"),(12,"LOWER"),(13,"MIDDLE"),(14,"UPPER"),(17,"LOWER"),(18,"MIDDLE"),(19,"UPPER"),(20,"LOWER"),(21,"MIDDLE"),(22,"UPPER"),(25,"LOWER"),(26,"MIDDLE"),(27,"UPPER"),(28,"LOWER"),(29,"MIDDLE"),(30,"UPPER"),(15,"S_LOWER"),(16,"S_UPPER"),(23,"S_LOWER"),(24,"S_UPPER");

```
```sql
INSERT INTO maintainance (maintain_no, maintain_type, maintain_date, coach_no)
SELECT CONCAT('MNT', LPAD(ROW_NUMBER() OVER (), 3, '0')) AS maintain_no,
    CASE
        WHEN DATEDIFF((SELECT SEC_TO_TIME(FLOOR(TIME_TO_SEC('15:00:00') + RAND() * (TIME_TO_SEC(TIMEDIFF('22:00:00', '15:00:00')))))), last_maintained) >= 180 THEN '6 Month'
        ELSE 'Mileage'
    END AS maintain_type,
    last_maintained AS maintain_date,
    coach_no AS coach_no
FROM coaches;

```
```sql
insert into train_schedule(route_no,train_no,station_code,Date,EAT,AAT,EDT,ADT) values
('RT001',22945,'CSMT','2023-10-12',NULL,NULL,'09:00:00','09:00:00'),
('RT001',22945,'JAM','2023-10-12','14:40:00','14:40:00',NULL,NULL),
('RT014',22946,'JAM','2023-10-12',NULL,NULL,'16:40:00','16:40:00'),
('RT014',22946,'CSMT','2023-10-12','22:20:00','22:20:00',NULL,NULL),
('RT002',14553,'NDLS','2023-12-25',NULL,NULL,'07:00:00','07:00:00'),
('RT002',14553,'UHL','2023-12-25','13:10:00','13:10:00',NULL,NULL),
('RT015',14552,'UHL','2023-12-25',NULL,NULL,'16:10:00','16:10:00'),
('RT015',14552,'NDLS','2023-12-25','22:20:00','22:20:00',NULL,NULL),
('RT003',11019,'SC','2023-12-28',NULL,NULL,'10:00:00','10:00:00'),
('RT003',11019,'VSKP','2023-12-28','18:30:00','18:30:00',NULL,NULL),
('RT016',11020,'VSKP','2023-12-28',NULL,NULL,'21:30:00','21:30:00'),
('RT016',11020,'SC','2024-12-29','00:20:00','00:20:00',NULL,NULL),
('RT004',22223,'CSMT','2024-01-03',NULL,NULL,'11:40:00','11:40:00'),
('RT004',22223,'SNSI','2024-01-03','17:00:00','17:00:00',NULL,NULL),
('RT017',22222,'SNSI','2024-01-03',NULL,NULL,'19:00:00','19:00:00'),
('RT017',22222,'CSMT','2024-01-04','00:20:00','00:20:00',NULL,NULL),
('RT005',11301,'CSMT','2024-01-15',NULL,NULL,'08:25:00','08:25:00'),
('RT005',11301,'SUR','2024-01-15','15:00:00','15:00:00',NULL,NULL),
('RT018',11302,'SUR','2024-01-15',NULL,NULL,'17:00:00','17:00:00'),
('RT018',11302,'CSMT','2024-01-15','23:35:00','23:35:00',NULL,NULL),
('RT006',12715,'BPL','2024-01-25',NULL,NULL,'20:15:00','20:15:00'),
('RT006',12715,'NDLS','2024-01-26','04:00:00','04:00:00',NULL,NULL),
('RT019',12716,'NDLS','2024-01-26',NULL,NULL,'06:00:00','06:00:00'),
('RT019',12716,'BPL','2024-01-26','13:45:00','13:45:00',NULL,NULL),
('RT007',19628,'LNL','2024-02-05',NULL,NULL,'02:15:00','02:15:00'),
('RT007',19628,'AII','2024-02-05','13:00:00','13:00:00',NULL,NULL),
('RT020',19627,'AII','2024-02-05',NULL,NULL,'16:00:00','16:00:00'),
('RT020',19627,'LNL','2024-02-06','02:45:00','02:45:00',NULL,NULL),
('RT008',17325,'DWR','2024-02-15',NULL,NULL,'05:00:00','05:00:00'),
('RT008',17325,'SBC','2024-02-15','10:00:00','10:00:00',NULL,NULL),
('RT021',17326,'SBC','2024-02-15',NULL,NULL,'12:00:00','12:00:00'),
('RT021',17326,'DWR','2024-02-15','17:00:00','17:00:00',NULL,NULL),
('RT009',18234,'BPL','2024-02-25',NULL,NULL,'21:15:00','21:15:00'),
('RT009',18234,'INDB','2024-02-26','00:15:00','00:15:00',NULL,NULL),
('RT022',18235,'INDB','2024-02-26',NULL,NULL,'03:15:00','03:15:00'),
('RT022',18235,'BPL','2024-02-26','06:15:00','06:15:00',NULL,NULL),
('RT010',10103,'CSMT','2024-03-05',NULL,NULL,'03:00:00','03:00:00'),
('RT010',10103,'VSG','2024-03-05','09:00:00','09:00:00',NULL,NULL),
('RT023',10102,'VSG','2024-03-05',NULL,NULL,'12:15:00','12:15:00'),
('RT023',10102,'CSMT','2024-03-05','18:15:00','18:15:00',NULL,NULL),
('RT011',13022,'RXL','2024-03-15',NULL,NULL,'10:10:00','10:10:00'),
('RT011',13022,'HWH','2024-03-16','04:00:00','04:00:00',NULL,NULL),
('RT024',13021,'HWH','2024-03-16',NULL,NULL,'06:00:00','06:00:00'),
('RT024',13021,'RXL','2024-03-16','23:50:00','23:50:00',NULL,NULL)

```
```sql

```
