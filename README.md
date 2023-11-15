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

  -Routes(Route_no,Route_name,time_taken,total_dist,Start_Stn,Start_time,End_Stn,End_time)
 
  -Stations(Station_code,Station_name,No_of_Platform,State)
 
  -Trains(Train_no,Train_name,Capacity,Route_no)
 
  -Coach(coach_no,made_by,last_maintained,after_maintained_dist)
 
  -Active_Coach(Coach_no,Train_no,Date)
 
 -Standby_Coach(Coach_no,Date)
 
 -Maintainance(Maintain_no,Maintain_date,Maintain_type,Coach_no)
 
 -Tickets(Ticket_no,Train_no,Status,passenger_name,Age,Board_stn,drop_stn,date_of_journey,booking_date,fare,discount,travel_agent_id,agent_comm)
 
 -Travel_Agents(Travel_Agent_Id,Travel_Agent_Name,ADD,MOB,Email)
 
 -Staff(Staff_no,Staff_name,Contact_no,residence_city)
 
 -Seats(Seat_no,Seat_type)
 
 -Staff_schedule(Route_no,Train_no,Driver_no,Remark,Time,Date,Accomodation)
 
 -Train_schedule(Route_no,Train_no,Station_code,Date,ETA,AAT,EDT,ADT)
 
 -Seat_allocated(Ticket_no,Coach_no,Seat_no,Seat_type,Date,Time)
 
 -Train_coaches(Train_no,Coach_no,Date_from)

```sql
SELECT * FROM table
```
