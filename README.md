# CIT281 Lab-5
Purpose of this lab:
- To create a Node.js and fastify server application with GET and respond with JSON using Postman
- Working with Postman application. 

### Lab Code: 
```
const students = [
    {
      id:1,
      last: "Last1",
      first: "First1",
    },
    {
      id:2,
      last: "Last2",
      first: "First2",
    },
    {
      id:3,
      last: "Last3",
      first: "First3",
    }
  ];
// Require the Fastify framework and instantiate it
const fastify = require("fastify")();
// Handle GET verb for / route using Fastify
// Note use of "chain" dot notation syntax

// Student route 
fastify.get("/cit/student", (request, reply) => {
    reply
      .code(200)
      .header("Content-Type", "application/json; charset=utf-8")
      .send(students);
  });
  
  // Student ID route
  fastify.get("/cit/student/:id", (request, reply) => {
// Recieve Request
console.log(request);
let studentIDFromClient = request.paramas.id;
// Do something with the information in the request 
let studentToGiveToClient = null; 

for (studentFromArray of students) {
    if (studentFromArray.id == studentIDFromClient){
        studentToGiveToClient = studentFromArray;
        break;
    }
}
// Provide a response 
if (studentToGiveToClient != null) {
    reply
      .code(200)
      .header("Content-Type", "application/json; charset=utf-8")
      .send(studentToGiveToClient);
}
else {
    reply
    .code(200)
    .header("Content-Type", "text/html; charset=utf-8")
    .send("Could not find student with given ID");
}
  });
  

  // An undefined/wildcard route
  fastify.get("*", (request, reply) => {
    reply
      .code(200)
      .header("Content-Type", "application/json; charset=utf-8")
      .send("<h1>At Wildcard Route</h1>");
  });
    // An undefined/wildcard route
  fastify.post("/cit/students/add", (request, reply) => {
      // get request from client
      let dataFromClient = JSON.parse(request.body);
      console.log(dataFromClient);
      // do something with the request
      // 1) figure out the max id currently in the arry
      let maxID = 0;
      for (individualStudent of students) {
          if (maxID < individualStudent.id) {
              maxID = individualStudent.id;
          } 
      }
      // 2) create a new student object 's' of the 
      // fname = dataFromClient.firstname
      // .....
      // id = maxID + 1 
      generatedStudent = {
          id: maxID + 1,
          last: dataFromClient.lname,
          first: dataFromClient.fname
      };
      // 3) Add student object created in (2) to 'student' array
      students.push(generatedStudent);
      // 4) send the student object created in (2) back to the client 
      // Reply to client 
    reply
      .code(200)
      .header("Content-Type", "application/json; charset=utf-8")
      .send(generatedStudent);
  });
// Start server and listen to requests using Fastify
const listenIP = "localhost";
const listenPort = 8080;
fastify.listen(listenPort, listenIP, (err, address) => {
  if (err) {
    console.log(err);
    process.exit(1);
  }
  console.log(`Server listening on ${address}`);
});
```
![AllStudents](https://user-images.githubusercontent.com/84296093/120626512-93544f00-c417-11eb-827c-030726410d2f.JPG)
![IndividualStudent](https://user-images.githubusercontent.com/84296093/120626567-a36c2e80-c417-11eb-8b96-358802c1b105.JPG)
![UnMatched](https://user-images.githubusercontent.com/84296093/120626558-9fd8a780-c417-11eb-92ab-7226abd89094.JPG)

### What I learned:
I learned how to use Postman to test server Get routes. I also learned how to gather the requested information quickly and effectivly. 

[SOurcecode](https://ruichen11.github.io/Ruichen11.CIT-Minor/)
