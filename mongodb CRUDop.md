Create database

use darshan
switched to db darshan

Insert into db
one
```
db.darshan.insertOne({
name:"darry",
age:20,
branch:"cse",
religion:"Hindu"})
```

many
```
db.darshan.insertMany(
{[
name:"ninad",
age:20,
branch:"cse",
religion:"Maratha"
},
{
name:"garima",
age:20,
branch:"cse",
religion:"Hindu"
},
  {
name:"tavish",
age:20,
branch:"cse",
religion:"Hindu"}
])
```

![image](https://github.com/Modilover69/dbms/assets/132368904/0e99cb66-156b-4ed3-a6fd-7e3b0248478b)

Read database

```
db.darshan.find()
```

![image](https://github.com/Modilover69/dbms/assets/132368904/30f608e2-7c6c-4a71-8195-9b03920ef932)

Update database

```
db.darshan.updateOne({name:"darry"},{$set:{age:21}})
```

![image](https://github.com/Modilover69/dbms/assets/132368904/eed5e516-c1e4-4ca1-a8ce-c86f45854ad5)

delete operation

```
db.darshan.deleteOne({name:"tavish"})
```

![image](https://github.com/Modilover69/dbms/assets/132368904/c8e924c0-759d-465d-90fe-d121f4d3ee42)


