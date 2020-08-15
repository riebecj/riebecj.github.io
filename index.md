## Welcome to my GitHub Pages

This page was developed for my Capstone Project at Southern New Hampshire University while finishing my Bachelor's of Science in Computer Science.

### Professional Assessment

I, personally, don't think that this ePortfoloio can really showcase my true strengths, mainly because I deal with far more complicated and complex processes and distributed software and server systems on a daily basis. However, it is a good basis for me to show that I can do a multitude of programming functions and play in a variety of categories. The catagories shown in this project are software design and engineering, data structures and algorithms, and databases.

There isn't much to shape here, as far as professional goals, as I am already a Systems Development Engineer for a big tech company. So, I can definitly say my employability is pretty high. I collaborate in a team setting every day, and that team can change depending if I'm focusing more on development code projects or working more DevOps and Linux command line. I communicate daily with stakeholders, whether it's for my own team looking for updates to my project, or a different team that I'm working with to build out thier service. And those services that I develop or help another team to build can utilze various data structures, algorithms, various engineering methods, databases, security measures, or any combination of them; usually almost all of them. These are areas I'm very famliar with, but unfortunatly I cannot show projects or code due to company policies.

In the code artifacts referenced in the artifact section below, I took the artifacts from CS-340 Advanced Programming Concepts, specifically because it uses a multitude of concepts and areas that would allow me to hit all three categories while still only working on a singular code package. This artifact is the database interface and RESTful API used in conjunction with MongoDB. However, in an effort to challenge myself, as well as showcase an ability to leverage Pythonic integrations without utilizing third-party software, only third part libraries that can be required within the setup.py and installed along with the package, I transitioned the CLI and API to utilize TinyDB, a pure python NoSQL database. Then I added features and functions, as described in my Code Review below, to showcase my engineering and data structures knowledge. More of what I've done is detailed in the Narrative section below.

### Code Review

This video below details a review of the current code and proposed changes and updates to be made.

[![CODE RIEVIEW](https://i9.ytimg.com/vi/am-uSrdg3wE/mq3.jpg?sqp=CJyJ4fkF&rs=AOn4CLCWVGOSZSlcDcThdPc_NByUB2vb_A)](https://youtu.be/am-uSrdg3wE)

### Code Artifacts

This is [the link](https://github.com/riebecj/TinyIntegration/tree/master/src/TinyIntegration) to my code artifacts of the completed project.

### Narrative

##### Software Design and Engineering

In order to revamp the API to run in a different process that can be started via the accompanying CLI, I had to reimplement the run function of the ServerAdapter in Bottle. This allows the storing of a reference to the server process object in memory that can eventually be called to shut itself down. Due to the way process do not share memory or address space, the API itself has to handle its own shutdown. This is where I implemented the `/stop` call within the API. I also left the standard python `__main__` function for the CLI to execute the entire script self-contained via a subprocess call. The CLI has a feature to start an api-daemon with the `-op` flag.

The biggest, and only, challenge was figuring out how to implement the API within its own process that can be started from the CLI. This would give the user the ability to start the API that can be used by other automated systems, like front end code, to display database information or interact with the database in a meaningful way, while not having to sacrifice the process in the CLI, or closing it by mistake. I leveraged the subprocess module and the Windows “start” call to start a new python process with the API script as the argument. A nice, but emergent behavior is that a command window opens after making the call to display the API logs. It gives the user a peak into how the API is being called and the successes of such calls. 


##### Algorithms and Data Structure

I had planned on implementing rotating credentials, but shortly came to the conclusion that this type of implementation was out of the scope of this project. The necessity for logging in was primarily to control the deletion of databases and creation of users. Those operations will happen more infrequently, and no other operations would really require administrator access to the database. So, in light of that, I implemented a login feature in the CLI that will validate a user is an Administrator before deleting a database or creating a new user. The password is salted and hashed before being entered into the database or being compared to entries already in the database as a means of increased security. ***No unhashed credential data is stored anywhere.*** 

The feature of YAML being a valid format of data returned from a database read was also implemented. I added a `/yaml` option to the URL, im betwqeen the data arguments and the optional `/all` argument and looked for that string. If present, I returned a formatted YAML response. This was easily done through implementing PyYAML and converting the JSON dump of the database client response to YAML. 

I definitely learned that there are some features worth pursuing, and there are other features that, despite being *cool* or *interesting* don’t really provide value added to the entire system. In todays job economy for the software engineer, it’s incredibly important to know when to implement a feature, and when to put in on the back burner. This is true here, as much as it is at my current job. 

##### Databases

I was re-implemented everything, the API, the CLI, and the interface client to use TinyDB, which is a pure-python NoSQL document database. This was chosen to showcase my abilities and reading documentation and understanding various aspects of database client functionality, as I had to rewrite functions and implementations for a completely different database system. I have successfully achieved a basic integration of all of the core features necessary for database operations. Those are the ability to create and delete databases and to create, read, update, and delete documents within the databases. Not only did I give the user two methods to which they can interact with the database (API and CLI), I also provided a database client that the user can re-implement for their own purposes to develop their own interaction or automation around.

This was honestly one of the more time consuming aspects of this project, as it wasn't really a direct one-for-one replacement of functions from one database system to another. Once the ineractions were understood, it became pretty easy to understand how the re-implementations should go, it was more finding out the exact syntax to use to get the correct interactions.
