#Mongo DB CRUD명령어

###Insert
- SQL -> `insert into users("name","city") values("wan","seoul")`
- Mongo DB -> `db.users.insert({_id:"wan",city:"seoul")`

###Select
- SQL -> `select * from users where id = "wan"`
- Mongo DB -> `db.users.find({_id:"wan"})`

###Update
- SQL -> `update users set city = "busan" where _id = "wan"`
- Mongo DB -> `db.users.update({_id:"wan"},{$set:{city:"busan"}})`

###Delete
- SQL -> `delete from users where _id = "wan"`
- Mongo DB -> `db.users.remove({_id:"wan"})`