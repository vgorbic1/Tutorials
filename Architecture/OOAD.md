## Object-Oriented Analysis and Design (OOAD)
OOAD is a technical method of analyzing and designing an application based on that 
system’s **object models**.

**Object Models** are the logical components of the system that interact with one another.

During the software development life cycle, development is typically broken up into stages, 
which are loose, abstract concepts used to separate the activities taking place within each 
phase of development. Often, these stages might include:
- requirements
- planning
- design
- coding/development
- testing
- deployment
- maintenance

In the case of stringent (strict) development methodologies, such as the **waterfall** method, these 
stages are sequential and intended to be completely separate from one another. Thus, when 
creating an application using the waterfall method, it’s unlikely that discoveries made 
during the testing or deployment phases can impact the decisions already made during the 
planning or design phases. These limitations, along with the strict step-by-step staging 
process of waterfall-esque models, led to the rise of iterative models like 
**object-oriented analysis and design**.

While OOAD practices have been around for a number of decades, these publications and 
methodologies are still in use today, including the **Unified Modeling Language** (UML) and the 
**Rational Unified Process**.

### Object-Oriented Analysis
When discussing OOAD concepts, an object most closely resembles the object-oriented programming 
version of an *object*, in that it is a representation of a real world object with specific 
characteristics (properties), behaviors (methods), and states (data).

OOA is an iterative stage of analysis, which takes place during the software development 
life cycle, that aims to model the functional requirements of the software while remaining 
completely independent of any potential implementation requirements.

A typical OOA phase consists of five stages:

- Find and define the objects.
- Organize the objects.
- Describe how the objects interact with one another.
- Define the external behavior of the objects.
- Define the internal behavior of the objects.

For example, a typical implementation of OOA is to create an object model for an application. 
The object modelmight describe the names, relationships, behaviors, and characteristics of 
each object in the system. 

With this information established for each object, the design process that follows is much simpler.

### Object-Oriented Design
The process of **object-oriented design** is really just an extension of the object-oriented analysis 
process that preceded it, except with a critical caveat: the consideration and implementation of 
constraints.

The OOD process takes the theoretical concepts and ideas planned out during the OOA stage, 
and tries to find a way to design and tangibly implement them, usually via code using whatever 
language and platforms the development team has settled upon. 

If OOA is the **what**, then OOD is the **how**.

### Advantages of Object-Oriented Analysis and Design
- **Encourages Encapsulation:** Since everything within OOAD revolves around the concept of objects,
one of the biggest advantages of OOAD is that it encourages planning and development of systems 
that are truly independent of one another. Just like a class written using object-oriented techniques, 
all the systems and objects produced during an OOAD development life cycle can be mixed and matched 
as necessary, since they will ideally be built as completely self-contained entities.
- **Easy to Understand:** Since OOAD principles are fundamentally based on real world objects, it’s 
quite easy for everyone on the team to quickly understand what an object name means or how a particular 
behavior, well, behaves. This makes the overall development life cycle a much smoother process, 
particularly if your team needs to frequently interact with customers or other non-technical users 
about the objects and components in the system. In such cases, most people still understand how 
system components and modelled objects work when they’re based on real world objects and ideas.

### Disadvantages of Object-Oriented Analysis and Design
- **Ill-Suited to Procedural Applications:** Given the object-oriented nature of OOAD, it is quite difficult 
(although not impossible) to practice OOAD techniques within a procedural programming language, or often 
to apply the techniques to non-object business logic. Whereas procedural applications are often logically 
bound by concepts of scope and modularity, object-oriented applications, of course, emphasize objects 
that simulate the real world.
- **Too Complex for Simple Applications:** While arguably not a disadvantage that is applicable to all projects, 
it’s certainly the case that OOAD practices are generally not ideal for simpler projects. Many developers have 
their own personal hard and fast rules to help when deciding whether a project should be procedural or 
object-oriented, but in most cases, the more basic the needs of the application, the more likely a 
less-structured, procedural approach is the best fit.

[SOURCE](https://airbrake.io/blog/design-patterns/object-oriented-analysis-and-design)
