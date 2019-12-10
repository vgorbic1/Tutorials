## Domain-Driven Design (DDD)
To define domain-driven design we should first establish what we mean by **domain** in this 
context (and in development in general). Domain is: the *“sphere of knowledge and activity 
around which the application logic revolves.”*

Another common term used during software development is **business logic**. The business logic of 
an application refers to the higher-level rules for how business objects interact with one another 
to create and modify modelled data.

Initially introduced and made popular by programmer Eric Evans in his 2004 book, *Domain-Driven Design: 
Tackling Complexity in the Heart of Software*, DDD aims to ease the creation of complex applications 
by connecting the related pieces of the software into an ever-evolving model. 

DDD focuses on three core principles:
- Focus on the core domain and domain logic.
- Base complex designs on models of the domain.
- Constantly collaborate with domain experts, in order to improve the application model and resolve any 
emerging domain-related issues.

### Common Terms
- **Context:** The setting in which a word or statement appears that determines its meaning. Statements about 
a model can only be understood in a context.
- **Model:** A system of abstractions that describes selected aspects of a domain and can be used to solve 
problems related to that domain.
- **Ubiquitous Language:** A language structured around the domain model and used by all team members to 
connect all the activities of the team with the software.
- **Bounded Context:** A description of a boundary (typically a subsystem, or the work of a specific team) 
within which a particular model is defined and applicable.

Domain-driven design also heavily emphasizes the ever-more-popular practice of **continuous integration**, which 
asks the entire development team to use one shared code repository and push commits to it daily (if not multiple 
times a day).

### Advantages of Domain-Driven Design
- **Eases Communication:** With an early emphasis on establishing a common and ubiquitous language related 
to the domain model of the project, teams will often find communication throughout the entire development 
life cycle to be much easier. Typically, DDD will require less technical jargon when discussing aspects of 
the application, since the ubiquitous language established early on will likely define simpler terms to 
refer to those more technical aspects.
- **Improves Flexibility:** Since DDD is so heavily based around the concepts of object-oriented analysis and 
design, nearly everything within the domain model will be based on an object and will, therefore, be quite 
modular and encapsulated. This allows for various components, or even the entire system as a whole, 
to be altered and improved on a regular, continuous basis.
- **Emphasizes Domain Over Interface:** Since DDD is the practice of building around the concepts of domain and 
what the domain experts within the project advise, DDD will often produce applications that are accurately 
suited for and representative of the domain at hand, as opposed to those applications which emphasize 
the UI/UX first and foremost. While an obvious balance is required, the focus on domain means that a 
DDD approach can produce a product that resonates well with the audience associated with that domain.

### Disadvantages of Domain-Driven Design
- **Requires Robust Domain Expertise:** Even with the most technically proficient minds working on development, 
it’s all for naught if there isn’t at least one domain expert on the team that knows the exact ins and outs of the 
subject area on which the application is intended to apply. In some cases, domain-driven design may require the 
integration of one or more outside team members who can act as domain experts throughout the development life cycle.
- **Encourages Iterative Practices:** DDD practices strongly rely on constant iteration and continuous integration 
in order to build a malleable project that can adjust itself when necessary. Some organizations may have trouble 
with these practices, particularly if their past experience is largely tied to less-flexible development models, 
such as the **waterfall model** or the like.
- **Ill-Suited for Highly Technical Projects:** While DDD is great for applications where there is a great deal 
of domain complexity (where business logic is rather complex and convoluted), DDD is not very well-suited for 
applications that have marginal domain complexity, but conversely have a great deal of technical complexity. 
Since DDD so heavily emphasizes the need for (and importance of) domain experts to generate the proper ubiquitous 
language and then domain model on which the project is based, a project that is incredibly technically complex may 
be challenging for domain experts to grasp, causing problems down the line, perhaps when technical requirements 
or limitations were not fully understood by all members of the team.

[SOURCE](https://airbrake.io/blog/software-design/domain-driven-design)
