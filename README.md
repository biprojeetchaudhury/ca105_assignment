# ca105_assignment

# <center>INTERCITY EXPRESS TRAINS</center>

## Entity Relationship Diagram

<img
  src="/erDiagram.jpg"
  alt="Alt text"
  title="Optional title"
  style="display: inline-block; margin: 0 auto;width: 100%;height:100%">
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
