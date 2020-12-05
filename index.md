
# About Me

My name is Tim Alberts and I work in software development and technology.  Please refer to my [LinkedIn](https://www.linkedin.com/in/tim-alberts-87303430/) profile for more details.


## Education

While my original interests started with electronics and hardware, my passion for writing software eventually won over.

Having some general engineering and computer science education following high school, plus an AAS degree from ITT in electronics, I was able to get myself into the work world and continued to build my skills and experience.  Following some life and career changes I made the decision to finish my BA degree in computer science.  This landed me at SNHU.

With my journey through the CS program coming to an end, I can reflect back on what was achieved.

- collaborating in a team environment (IT-315 UML, CS-310 git) ... working with other developers
    - Functional structural behavioral
- communicating to stakeholders (IT-315 UML)
- data structures and algorithms (CS-260 algorithms, IT-365 operating systems)
- software engineering and database (CS-340, DAD-220, DAT-220)
- security
    - Operating Systems Authentication/Authorization
    - CS-340 server/defensive programming, A&A

As an exemplar of the skills developed, the following are projects to demonstrate skills and knowledge in three key areas:

- [Software design and engineering]
- [Algorithms and data structure]
- [Databases]

### Software design and engineering
[Software design and engineering]: #software-design-and-engineering

#### Description
The artifact is a C++ program that leverages OpenGL to render a 3D mesh and associated texture with appropriate lighting, camera and view controls.  This project is a critical exercise in understanding how computer graphics work with regard to both the mathematical modeling and the hardware interactions for the graphics rendering pipeline.  The original artifact was created in the CS-330 computer graphics course, approximately end of June 2020.

- Original Work: https://github.com/TimAl6ert5/Felix/commit/e6baa6bc0211a9c047adc7479420a5f644414717
- Enhancement: https://github.com/TimAl6ert5/Felix/tree/develop
- Code Review: https://youtu.be/v16AYueD9G0

#### Justification
This artifact demonstrates critical skills in modern OpenGL computer graphics software design and development.  This article is included in order to demonstrate competency in understanding modern computer graphics.  Given the state of the original project and the planned improvements being implemented, this project is an example of developing and improving existing software by being able to research, design, and implement improvements to existing codebase.  This is a critical skill for a software developer to have.

Given that the original project was implemented in a mostly structured and static design, the work to break down the application into reusable components and make the application more generalized is an important item to showcase.  A prime example of this artifact is the refactoring of the code in order to make the components more easily testable.  Specifically, the ‘Mesh’ class method originally read the OBJ file contents and then loaded these into graphics memory buffers.  This was convenient from the caller perspective, however this made the code to read the OBJ file untestable without also having the graphics context.  The refactor simply isolated the file read function from the buffer initialization, which allowed it to be independently unit tested.  This is a big win for the project because this is also a major point for improvement in the stability and capability of the program.  It is critical in any piece of software to have strong validation when receiving input from an outside source, such as the user.  Invalid input can easily corrupt or crash a program.  Rather than have the application exhibit any byzantine behavior, it is better to validate the input and let the user know they’re doing something wrong.

#### Reflection
The first important takeaway from this enhancement is the criticalness of ensuring code is maintainable and testable.  While developing tests for the Mesh loader I quickly realized the problem with having the method to load the object file do too much.  The code refactor made this easier to test, but also required the caller to perform additional steps.  The other ‘gotcha’ was in the destructor cleaning up the buffers.  A guard flag had to be implemented to make sure things were cleaned up only if they were actually initialized.

The second challenge in making these changes was to make sure that changes were implemented in some controlled and orderly fashion.  To accomplish this, I started the ‘CHANGELOG.md’ file and broke down the tasks to a list that can be checked off as they are completed.  This list serves both as a way to keep track of what needs to be changed, but also what has been changed.  Ultimately, this codebase needs to be put under source control.

The third, and biggest challenge comes from trying to encapsulate application behaviors while interacting with the freeGLUT library.  The challenge, as research indicates, comes from trying to pass class methods as callback functions for GLUT.  GLUT being written in C does not easily accept this.  For example, reference the function glutDisplayFunc (https://www.opengl.org/resources/libraries/glut/spec3/node46.html#SECTION00081000000000000000).  A possibility to work around this is to encapsulate the behavior as desired and create adapter functions to call the desired behaviors.  This modification may be beyond the scope of the current project enhancements timeline.
The result is the development of a Scene object that encapsulates rendering the subject, lighting and camera.


### Algorithms and data structure
[Algorithms and data structure]: #algorithms-and-data-structure

- Project Review: https://youtu.be/glkGPHE2GJo
- Artifact Result: https://github.com/TimAl6ert5/Elim

#### Description
The artifact partly comes from the CS-260 data structures course.  Graph data structures are particularly interesting for the wide variety of applications and problems that can be solved using this type of model.  Unfortunately, the course never dealt with graph data structures and algorithms.  This project will be my opportunity to teach myself these critical skills to better prepare me for any career moves in the field of Computer Science.  The goal of the project is to develop skills and understanding around the graph data structures by developing a library of tools for representing graphs in different ways and determining specific graph properties from these.

#### Justification
Graph data structures and algorithms are a fundamental concept to a variety of fields and applications in computer science.  For example, path finding and navigation.  In order to advance in the field of Computer Science, it is critical to develop strong understanding of these concepts.  The handling and study of graph data structures not only develops the skills specific to this type of model, but also develops skills necessary to develop algorithms that will scale well.  This involves being able to analyze the trade-offs between the time and space required for an algorithm.

The artifact as it exists currently, demonstrates several fundamental computer skills, in addition to basic knowledge of graph data structure representation and properties.  To begin with the artifact demonstrates the ability to develop a new Java project using industry standard build automation tools.  Next the artifact demonstrates the ability to design and develop an application using object-oriented techniques.  Next the artifact demonstrates knowledge of graph data structures being represented in different ways (i.e. adjacency matrix, edge list, adjacency list).  Finally, the artifact demonstrates understanding of how to apply a range of algorithms and data structures to solve problems in computer science.

#### Reflection
The development of the project covered many fundamental skills needed in computer science.  First is developing basic project structure that supports consistent, repeatable builds, handle source code formatting, and provide a framework for unit testing and reporting.  The Java language has several tools to choose from such as Ant, Maven, Gradle, SBT.  While Maven is one of the older tools, it is still a popular choice and has numerous well established tools and plugins.

Second, the application design work to put the application together in a way that supports expanding the application to support additional graph representations without the necessity to change the application structure.  This is mainly accomplished by the ‘io.github.timal6ert5.intarray.GraphDetails’ interface.  This use of interfaces in Java is a great way to establish abstraction.

Third, the development of the algorithms to determine the properties for each of the graph is a great exercise in thinking about complexity.  Additionally, there are larger design questions such as how to minimize the number of times a graph needs to be read.  For example, the constructor will do some basic analysis of the structure to verify it satisfies the expected format.  Then several method calls will iterate over the graph again to determine properties.  The first improvement to be done is to add properties to save the result so once the algorithm is run it does not have to be run again since the actual graph is immutable once constructed.  Second, it would be a better design to only iterate over the graph once to both verify the format and to capture the properties.  However, if the intention is to make a reusable library it may also be better to only run the algorithms when they are requested to minimize the amount of processing during construction.  The way this application uses it would be more performant to handle as much as possible during construction.


### Databases
[Databases]: #databases

- Original Work: https://github.com/TimAl6ert5/Cephas/commit/bae360f45c5c23e86440fa33a7844aec035791c1
- Enhancmenet:
- Code Review: https://youtu.be/ks6WGLAyLHg


#### Description
The artifact is a python-mongo [REST](https://developer.ibm.com/articles/ws-restful/) service that comes from the CS-340 data structures course.  It was originally developed around October, 2020.  The service originally operated on a set of stock data.  It included CRUD operations for data management and methods for searching and reporting data. This project served as an example of the backend implementation in a typical web service or three tier web application.

#### Justification
The artifact is included to demonstrate essential skills in developing services around data access and management.  Data processing is probably the most important aspect of computer science there is, regardless of the field or industry a person may work in.  RESTful services are a foundational part of the internet that provide a framework for sharing information between computers.  The ability to understand, develop, and enhance these types of services is an important skill for a software developer to have.

The enhancement of this artifact demonstrates the ability to analyze existing services and design improvements to both functionality and security.  The original service was a bare minimum needed to demonstrate a functional RESTful service.  The original service was functional, but gave absolutely no concern to any security, even allowing to store nearly arbitrary data of any size and shape.  The enhancements developed modify the service schema to a generic, reusable domain, and also add safeguards against users storing random, or malicious data.  Each create and update request is parsed to verify all of the data that needs to be there, is provided and that it satisfies the data format.  Additionally, the service rejects any input data that may be attached that is not part of the design.  Regardless of having authentication and authorization, this is one of the critical safeguards needed to ensure data integrity in a service.

Furthermore, the enhancements to the service include a framework for testing that ensures the code can be accepted based on the design requirements.  The Robot Framework is a favorite of mine due to it simplicity in getting potentially complex tests done very quickly and to include a reasonably comprehensive test report to show exactly what happened and when.  The test themselves are very readable so they are good to present to stakeholders when necessary.

#### Reflection
The development of the project from the services standpoint was really a rehash of things I have worked on professionally for a few years while working on a digital advertising platform.  That system had a set of client services that followed similar patterns, but were developed using Java and spring boot.  I have also developed similar services for my current employer, however they are [GraphQL](https://spec.graphql.org/June2018/) services, not REST services.  GraphQL offers several enhancements over REST API’s that allow the client to make a single request to get data as specified, without having to make potentially several calls to compile all the data in the desired format.

The most interesting, and surprisingly exciting, part of working on this project and the CS340 class was really getting to know more about Mongo and NoSQL databases.  I can see the potential benefit provided by the schemaless database.  Furthermore, the geoJson is, for lack of a better expression, really cool!  I’ve only skimmed through the source code a bit to try and get some understanding of how it is structured, but I’m very interested to read their library for handling geoJson data and performing the calculations for mapping regions and determine distances etc (looks like it is here https://github.com/mongodb/mongo/tree/master/src/mongo/db/geo).  From an application developer standpoint, this is a very powerful feature.

The main challenge I faced was dealing with, what seems to be, the simplicity of the bottle framework.  Most of the services I have worked on in the past were Java servlet and Spring boot services that involved things such as dependency injection and aspect oriented programming.  There seem to be specific ways of doing things and available libraries to do them with, such as input validation and persistence.  One of the things that makes Python an appealing language is there are so many libraries available that allow people to get things done very quickly.  The Bottle framework is no exception to this, as it touts being “fast, simple and lightweight.”  This appears to mean that if I want to add the more heavyweight stuff, I have to write it myself.  I believe I have accomplished a sufficient method for performing input validation by implementing an request class and manually populating it from the user request payload.  This at least guards the information going into the database.  Going forward, I would implement this service using a different framework.

