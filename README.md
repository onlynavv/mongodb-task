# mongodb-task

## 1) 

### db.topics.aggregate([{$project:{title:1, month:{$month:"$taughtAt"}}},{$match:{month:10}}]).pretty()

![image](https://user-images.githubusercontent.com/77113035/146791130-5fbc03b5-d4f0-4353-9757-e0fa073bf8fe.png)


### db.tasks.aggregate([{$project:{description:1, month:{$month:"$taughtAt"}}},{$match:{month:10}}]).pretty()

![image](https://user-images.githubusercontent.com/77113035/146791373-1cb96b77-5926-43f2-b32c-7d9dde96a378.png)


## 2) 
### db.drives.find({"date":{$gte:ISODate('2020-11-15T00:00:00.000Z'),$lte:ISODate('2020-11-31T00:00:00.000Z')}},{"driveId":1, "userId":1}).pretty()

![image](https://user-images.githubusercontent.com/77113035/146777260-73267b95-52e0-47d2-be65-48cbfd82459b.png)

## 3)

### db.attendance.find({heldOn:ISODate("2020-11-27T00:00:00Z")},{userId:1}).pretty().toArray()

![image](https://user-images.githubusercontent.com/77113035/146791943-585cd0ec-b343-48db-a3fd-dd43afcd0544.png)


### db.drives.find({date:ISODate("2020-11-27T00:00:00Z")},{driveId:1,userId:1}).pretty().toArray()

![image](https://user-images.githubusercontent.com/77113035/146792216-f967238b-33d4-4cee-beb3-2bc08525c9e5.png)


## 4) 

### db.codekata.find({"solvedBy.userId":ObjectId("61c04b3bbc70e9c003883989")}).count()

![image](https://user-images.githubusercontent.com/77113035/146788485-2c841d7a-f8ba-4dfb-bb15-5fe7d5c0969f.png)

![image](https://user-images.githubusercontent.com/77113035/146788382-6832e533-50ca-4a3c-9722-1e2793cf3906.png)


## 5) 

### db.mentors.aggregate([{"$project":{"mentorName":1,"menteeCount":{"$size":"$userId"}}},{"$match":{"menteeCount":{"$gte":15}}}]).pretty()

![image](https://user-images.githubusercontent.com/77113035/146773156-3a255e23-3c43-435c-84cb-0abe0d66cc77.png)

## 6)

### const data = db.attendance.find({heldOn:ISODate("2020-11-27T00:00:00Z")},{userId:1}).pretty().toArray()

data[0].userId =  [
                        ObjectId("61c04b60bc70e9c00388398f"),
                        ObjectId("61c04b3bbc70e9c003883989"),
                        ObjectId("61c04b23bc70e9c003883987"),
                        ObjectId("61c04b35bc70e9c003883988")
                ]
                
### db.users.find({name:{$nin:[ObjectId("61c04b60bc70e9c00388398f"),ObjectId("61c04b3bbc70e9c003883989"),ObjectId("61c04b23bc70e9c003883987"),ObjectId("61c04b35bc70e9c003883988")]}}).pretty().toArray()

![image](https://user-images.githubusercontent.com/77113035/146793418-82f2e6a2-bb2c-4864-935f-5297fac91266.png)


const data = db.tasks.aggregate([{$unwind:"$solvedBy"},{$match:{"solvedBy.submittedOn":{$gte:ISODate('2020-10-29T00:00:00.000Z'),$lte:ISODate('2020-10-31T00:00:00.000Z')}}}]).pretty()

this gives the users who have solved the tasks during 15 oct-2020 and 31-oct-2020

const arr = newArr.map((item)=>{
    return item.solvedBy.userId
})

after accessing the users who have solved the tasks list, and then give that list in the $nin operator we will get the not submitted users during that period,

### db.users.find({name:{$nin:[ObjectId("61c04b60bc70e9c00388398f"),ObjectId("61c04b3bbc70e9c003883989"),ObjectId("61c04b23bc70e9c003883987"),ObjectId("61c04b35bc70e9c003883988")]}}).pretty().toArray()
