Task 1: Add more students to the students collection
Add at least 5 new students to the students collection with unique names, roll numbers, and course enrollments.
Ans:

use codinggita_3;
switched to db codinggita_3
db.createCollection("students");
{ ok: 1 }
db.students.insertMany([
  {
    name: "Jenil",
    rollNumber: "CS1001",
    coursesEnrolled: ["CS101", "MATH202", "PHY101"],
  },
  {
    name: "krutagya",
    rollNumber: "CS1002",
    coursesEnrolled: ["CS101", "MATH101"],
  },
  {
    name: "jatan",
    rollNumber: "CS1003",
    coursesEnrolled: ["CS301", "MATH303"],
  },
  {
    name: "jagjeet",
    rollNumber: "CS1004",
    coursesEnrolled: ["ECE201", "MATH202"],
  },
  {
name: "shivam",
rollNumber: "CS1004",
coursesEnrolled: ["ECE201","MATH404"]}
]);


Task 2: Insert a new course into the courses collection
Add a new course with the following details:
Course Code: CS202
Name: Data Structures
Credits: 3
Instructor: Prof. Krishna
Ans:
db.courses.insertMany([
  {
    courseCode: "CS101",
    name: "Introduction to Programming",
    credits: 3,
    instructor: "Prof. Krishna",
  },
  {
    courseCode: "MATH101",
    name: "Mathematics I",
    credits: 4,
    instructor: "Prof. Priyesha",
  },
  {
    courseCode: "PHY101",
    name: "Physics I",
    credits: 4,
    instructor: "Prof. Arjun",
  },
  {
    courseCode: "ECE201",
    name: "Digital Electronics",
    credits: 3,
    instructor: "Prof. Mahir",
  },
]);

Task 3: Fetch a specific student's record by roll number
Use find() to fetch a student's information using their roll number (CS1002).

Ans:db.students.find({rollNumber: "CS1002"});



Task 4: Query all students who are enrolled in a particular course
Retrieve all students who are enrolled in "MATH101".

Ans: db.students.find({},{"coursesEnrolled":"MATH101"});

Task 5: Update a student's courses
Update the student with roll number CS1001 to enroll in an additional course "CS202".

Ans:  db.students.updateOne({rollnumber:"CS1001"},{$push: {coursesEnrolled:"CS202"}});



Task 6: Remove a course from a student's courses list
Remove the course MATH101 from the student Mahir's list of enrolled courses.

Ans: db.students.updateOne({name:"krutagya"},{$pull:{coursesEnrolled:"MATH101"}});


Task 7: Find all courses with 3 credits
Query the courses collection to find all courses where the credits field equals 3.

Ans: db.courses.find({credits:3});


Task 8: Find students who have enrolled in more than 2 courses
Use $size operator to query students who are enrolled in more than 2 courses.

Ans: db.students.find({coursesEnrolled:{$size:3}});


Task 9: Use the $in operator to find students enrolled in multiple courses
Use the $in operator to find students who are enrolled in either CS101 or MATH202.

Ans: 


Task 10: Fetch all students from a specific department (e.g., CSE)
Use a query to find all students in the CSE department.

Ans: db.students.find({},{department: "CSE"});


Task 11: Query students who are in their 3rd year
Retrieve students who are in the 3rd year using the year field.

Ans: db.students.find({year:3});

Task 12: Query students using a range for their year
Find all students who are in 2nd or 3rd year by using the $gte operator.

Ans: db.students.find({$or: {year:2},{year:3}});

Task 13: Count the total number of students in each department
Use the $group stage of aggregation to group students by department and count them.

Ans: db.students.aggregate([
    {$group:{id_:'$department',total:{$sum:1}}}
]);

Task 14: Group courses by credits
Group courses by their credit value and count how many courses there are for each credit value.

Ans: db.courses.aggregate([
    {$group:{_id:"$credits",total:{$sum:1}}}
]);


Task 15: Find the highest credit course
Query for the course with the highest number of credits using the $sort operator.

Ans: db.courses.aggregate([
  {$sort:{credits:-1}},
  {$limit:1}
]);

Task 16: Use the $and operator for filtering students
Find all students who belong to the CSE department and are enrolled in more than 2 courses.

Ans: db.students.find({$and:[{"department":"CSE"},{"coursesEnrolled":{$size:3}}]});
    
Task 17: Add a new field to all documents in the students collection
Add a new field activeStatus and set it to true for all students.

Ans: db.students.updateMany(
  {}, // Match all documents
  { $set: { activeStatus: true } } // Add the new field and set it to true
);

Task 18: Use $rename to rename a field
Rename the coursesEnrolled field in the students collection to enrolledCourses.

Ans: db.students.updateMany({}, { $rename: { "coursesEnrolled": "enrolledCourses" }}):


Task 19: Set default values for new fields in all student documents
Add a field graduationYear with a default value for all students.

Ans: db.students.updateMany({},{$set:{"graduationYear":4}});


Task 20: Use the $push operator to add a new course to a student’s course list
Add the course "CS303" to Mahir’s coursesEnrolled list.

Ans: db.students.updateOne({"name":"shivam"},{$push:{coursesEnrolled:"CS303"}});
 
Task 21: Use $pull to remove a course from a student's courses list
Remove the course CS101 from Jenil’s list.

Ans: db.student.updateOne({"name":"jenil"},{$pull:{coursesEnrolled:"CS101"}});

Task 22: Remove a student from the students collection
Delete the student record with roll number CS1004.

Ans: db.students.DeleteOne({"rollnumber":"CS1004"});

Task 23: Find students who are enrolled in both CS101 and MATH202
Use $all operator to find students who are enrolled in both courses.

Ans: db.students.find({enrolledCourses: { $all: ["CS101", "MATH202"] }});
<!-- checck that araay wale sab hai ki nahi  -->


Task 24: Use $regex to search for students whose name starts with "A"
Use regular expressions to search for students whose names begin with the letter "A".

Ans: db.students.find({name:{$regex:^A}});

Task 25: Use $exists to find students with enrolled courses
Query students who have an entry in the coursesEnrolled array.

Ans: db.students.find({enrolledcourses: {$exists:true}});

Task 26: Add a field to store students' grades for each course
Add a new field grades to the students collection and store an array of grades for each course.

Ans: db.students.updateMany({},{$push:{"grades":["A","B","C","D"]}});

Task 27: Use $elemMatch to query students enrolled in specific courses
Find students enrolled in CS101 and have the grade A.

Ans: db.students.find({enrolledCourses: {$elemMatch: {course: "CS101",grade: "A"}}});


Task 28: Use $size operator to query students with exactly 2 courses enrolled
Query students who have enrolled in exactly two courses.

Ans: db.students.find({ enrolledCourses: { $size: 2 } })

Task 29: Perform a text search for a course title
Use text indexing to search for the course Digital Electronics in the courses collection.

Ans:
db.courses.createIndex({ courseName: "text" })
db.courses.find({ $text: { $search: "Digital Electronics"}});

Task 30: Create a compound index on department and year
Create a compound index on the fields department and year for better querying performance.

Ans: db.students.createIndex({department:1,year:-1});

Task 31: Use $sort to order students by their roll number
Sort the students in ascending order of their roll number.

Ans: db.students.find({$sort:{rollnumber:1}});

Task 32: Create a unique index on the roll number
Create a unique index to ensure that the roll numbers in the students collection are unique.

Ans: db.students.createIndex({ rollNumber: 1 }, { unique: true })

Task 33: Update the course name in the courses collection
Update the name of the course CS101 to Intro to Programming.

Ans: db.courses.updateOne({courseCode:{$set:{"name":"Intro"}}});

Task 34: Create a backup of the CodingGitaStudents database
Use mongodump to back up the entire CodingGitaStudents database.

Ans:

Task 35: Restore the CodingGitaStudents database from the backup
Use mongorestore to restore the database after a backup.

Ans:

Task 36: Use $project to reshape data in aggregation
Project only the name and department of students using an aggregation query.

Ans:

Task 37: Use $unwind to deconstruct the courses array
Use $unwind to split the coursesEnrolled array into individual documents.

Ans: db.students.aggregate([{ $unwind: "$coursesEnrolled" }]);

Task 38: Use $limit to retrieve only the first 3 students
Use $limit to limit the result to the first 3 students in the students collection.

Ans: db.students.aggregate({$limit:3});

Task 39: Use $skip to skip the first 2 students and get the rest
Use $skip to fetch all students except the first two.

Ans:  db.students.aggregate({$skip:3});

Task 40: Use $lookup to join student data with courses
Use $lookup to fetch the course information for students.

Ans: 
db.students.aggregate([
{
$lookup:{
        from:"courses",
        localField:"courseCode",
        foreignField:" rollNumber",
        as:"coursesdetails"
    }
}
]);


Task 41: Create a new collection for storing studentFeedback
Create a collection studentFeedback with fields: studentRollNumber, feedbackText, date.

Ans: db.createCollection("studentFeedback");
db.studentFeedback.insertMany({"studentRollNumber":"123"},{"feedbackText":"verygood"},{"data":"456"});

Task 42: Query the studentFeedback collection to find feedback from a specific student
Use find() to retrieve feedback from Jenil.

Ans:

db.students.aggregate([{$match:{"name":"Jenil"}},
{
$lookup:{
        from:"studentFeedback",
        localField:"rollNumber",
        foreignField:" studentRollNumber",
        as:"feedbackdetails"
    },
}
]
);


Task 43: Use $set to update multiple fields at once
Use the $set operator to update the department and coursesEnrolled fields for Arjun.

Ans: db.students.updateMany({'name':"Arjun"}:{$set:{department:"compputer",coursesEnrolled:""}});


Task 44: Create a custom index on the coursesEnrolled field
Create an index on the coursesEnrolled array for faster querying.

Ans: 

Task 45: Perform a query on nested documents in students collection
Query for students who have grades A in their courses.

Ans: