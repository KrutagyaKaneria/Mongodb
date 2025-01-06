Task 1: Create a "CodingGita Students" database

Create a new MongoDB database called CodingGita. Add two collections:

students: Name, roll number, department, year, courses enrolled.
courses: Course code, name, credits, instructor.
Insert sample data into both collections.

Ans:
use codinggita;
switched to db codinggita
db.createCollection("students");

db.createCollection("courses");

db.students.insertMany([{"Name":"Krutagya","roll_number":8,"departemnt":"Computer science","year":1,"courses_enrolled":["CS101", "CS102"]},])

db.students.insertMany([{"Name":"jatan","roll_number":9,"departemnt":"Computer science","year":2,"courses_enrolled":["CS103", "CS101"]},
{"Name":"jenil","roll_number":10,"departemnt":"Machanical enigineer","year":3,"courses_enrolled":["CS001", "CS100"]},
{"Name":"jagjeet","roll_number":11,"departemnt":"Electornoics enigineer","year":4,"courses_enrolled":["CS101", "CS103"]}]);


db.courses.insertMany([
  { 
    "courseCode": "CS101", 
    "courseName": "Introduction to Programming", 
    "credits": 3, 
    "instructor": "Prof. Sharma" 
  },
  { 
    "courseCode": "CS102", 
    "courseName": "Data Structures", 
    "credits": 3, 
    "instructor": "Prof. Gupta" 
  },
  { 
    "courseCode": "CS103", 
    "courseName": "Algorithms", 
    "credits": 3, 
    "instructor": "Prof. Kapoor" 
  },
  { 
    "courseCode": "EE101", 
    "courseName": "Basic Electrical Engineering", 
    "credits": 4, 
    "instructor": "Prof. Verma" 
  },
  { 
    "courseCode": "EE102", 
    "courseName": "Circuit Theory", 
    "credits": 4, 
    "instructor": "Prof. Yadav" 
  }
]);



Task 2: Perform CRUD operations

Add a few more students and courses to the database.
Query data based on:
Department (e.g., "Computer Science").
Year (e.g., "2").
Courses enrolled (e.g., "CS101").
Update the courses for a specific student (e.g., adding a new course).
Delete a student or course from the database.


Ans:

db.students.find({"departemnt":"Computer science"});

db.students.find({"year":1});

db.students.find({"courses_enrolled":"CS101"});

db.students.updateOne({"name":"krutagya"},{$push:{"coursesEnrolled": "CS105"}});

db.students.deleteOne({"name":"krutagya"});


