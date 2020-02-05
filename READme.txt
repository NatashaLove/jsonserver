*****//This file - db.json-

// is where our Jason server is going to eventually store all of its information- all the blog POsts.
//We have to create this file ahead of time and inside of here we're going to add some configuration
//to tell Jason server about the different types of resources that we wanted to manage.

{
    "blogposts": []   // key:value
}
---create a endpoint for managing a resource called "blogpost" - all the blog posts we create are going to end up as objects inside this array [].
---can manually add in a blog post initially - Just adding in an object inside of that empty array- and it'll be at the server:
"blogposts": [
        {
            "id": 1,
            "title": "API POST",
            "content": "content for my post"
        }
    ]


*****// This file - package.json -

//Adding 2 scripts into package.json: 1. starting up json server; 2. starting up nGrok:
(deleted from scripts this code:
//"test": "echo \"Error: no test specified\" && exit 1"
and instead put these 2 scripts:

    "db": "json-server -w db.json", //anytime we run this "DB" script I want to run this command: "json-server -w db.json"-the command that's going to start up our Jason server;
    "tunnel": "ngrok http 3000" // second command -"tunnel" - going to run "nGrok HTTP  " and provide some port that we want in grok to connect to on our local machine.

//So this is going to be the server that we're going to expose to the outside world -so that we can connect to it from our ReACT native application.
//So we want ngrok to expose Json server; by default-Json server runs on port 3000- so I'll put it here '3000'.
test in 2 terminals: 
1) npm run db (from the folder with jsonserver); -can  work from GITBASH // now can access json server on our local machine- BUT no one else can see it..
!!!If there's an ERROR -(another service running on port )- should make changes in the pacjage.json on jsonserver in the script like: (another port instead of 3000)
(added "-p 3001")
"scripts": {
    "db": "json-server -w db.json -p 3001",
    "tunnel": "ngrok http 3001"
  },
***** HOW TO KILL A PROCESS (port connection): https://stackoverflow.com/questions/39632667/how-do-i-kill-the-process-currently-using-a-port-on-localhost-in-windows

2) Ngrok is going to make this Json server available to the outside world- so inside of that second terminal window-I'm going to run command:
! IN COMMAND PROMPT!  -npm run tunnel(from the folder with jsonserver) - that's going to start up a tunnel for us.

//Ngrok is only going to run for a small amount of time-in this case just eight hours.
//So every time that you are running your project -after eight hours this session is going to expire and you're going to have to restart it-
//to restart it -press "control + C" and then we can run: "NPM run tunnel" again-And that's going to give a new session of eight hours again.
//after nGrok restarts- url where the server is running updates (can see URL in the 2nd terminal after running "npm run tunnel"):
-----in cmd---- "Forwarding  http://4131c3f0.ngrok.io -> http://localhost:3000  "
//- so we must use the new url in ReactNative ( http://4131c3f0.ngrok.io - is the url,for ex).
// can pay for nGrok account (not much) - don't have to restart, will get a static subdomain.
//otherwise- if someone uses the app- i'll have to make sure manually update the url in React Native...(inconvenient, unstable)...

//TOTAL 3 terminal windows now for a project: 
!whenever we're going to do development on our application we're going to run three different terminal windows:
1) One is for a React Native bundler: we start that up with "NPM start";
2) the second one is inside of our Json server directory -the command "NPM run DB";
3) the third will also be inside of our Json server directory-the command "NPM run tunnel"- and NPM run tunnel has to be restarted every eight hours.

******// address/ route to make request to nGrok -server with saved blogPosts-
example: http://4131c3f0.ngrok.io/blogposts 
//-(added /blogposts manually to the address- http://4131c3f0.ngrok.io- copied it from the terminal with tunnel.)
//-that's how we're going to get our list of all of our different blog posts.

***********
API - application programming interface is an interface or communication protocol between different parts of a computer program intended 
to simplify the implementation and maintenance of software. An API may be for a web-based system, operating system, database system, computer hardware, or software library.
----our list of blogposts is stored at API (server)..