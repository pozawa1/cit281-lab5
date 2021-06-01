# Objectives
1. Create a Node.js and fastify server application with GET and respond with JSON
2. Use Postman to test server routes

# Technologies Used
- VSCode
- Postman 

# Part 1
Download and install Postman. 

# Part 2
Create a CIT 281 collection and folders. 

# Part 3
Create a Node.js and fastify server application that supports GET and responds with JSON.
```
// Require the Fastify framework and instantiate it
const fastify = require("fastify")();

// Student Route
fastify.get("/cit/student", (request, reply) => {
  reply
    .code(200)
    .header("Content-Type", "application/json; charset=utf-8")
    .send(students);
});

// Student ID Route
fastify.get("/cit/student/:id", (request, reply) => {
    // Receive Request
    let studentIDFromClient = request.params.id;
    // Do something with the information in the request
    let studentToGiveToClient = null; 

    for (studentFromArray of students) {
        if (studentFromArray.id == studentIDFromClient) {
            studentToGiveToClient = studentFromArray;
            break;
        }
    }
    
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

// Undefined/Wildcard Route
  fastify.get("*", (request, reply) => {
    reply
      .code(200)
      .header("Content-Type", "text/html; charset=utf-8")
      .send("<h1>At Wildcard Route</h1>");
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

# Part 4
Add array of students object.
```
const students = [
  {
    id: 1,
    last: "Last1",
    first: "First1",
  },
  {
    id: 2,
    last: "Last2",
    first: "First2",
  },
  {
    id: 3,
    last: "Last3",
    first: "First3",
  }
];
```

# Part 5
Use Postman to test server GET routes. 

All students:

![AllStudents](https://user-images.githubusercontent.com/83732149/120226989-30876b80-c1fd-11eb-8215-4dd014988dfb.png)

Single student:

![SingleStudent](https://user-images.githubusercontent.com/83732149/120226999-34b38900-c1fd-11eb-9e56-83e8cf17ec6c.png)

Unmatched:

![Unmatched](https://user-images.githubusercontent.com/83732149/120227016-3aa96a00-c1fd-11eb-84ee-c685cd9ec7dc.png)

# Part 6
Add a POST route handler that will accept a JSON request body with properties last and first.
```   
fastify.post("/cit/students/add", (request, reply) => {
        let dataFromClient = JSON.parse(request.body);
        console.log(dataFromClient);
            let maxID = 0;
            for (individualStudent of students) {
                if (maxID < individualStudent.id) {
                    maxID = individualStudent.id;
                }
            }
            let generatedStudent = {
                    id: maxID + 1,
                    last: dataFromClient.lname,
                    first: dataFromClient.fname         
                 };
            students.push(generatedStudent);

        reply
          .code(200)
          .header("Content-Type", "application/json; charset=utf-8")
          .send(generatedStudent);
      });
```

# Part 6
Use Postman to test server POST routes.

![StudentPost](https://user-images.githubusercontent.com/83732149/120227006-38471000-c1fd-11eb-9dca-cb587f540adc.png)

[Return to Homepage](https://pozawa1.github.io/)




