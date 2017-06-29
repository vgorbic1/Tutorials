## A Development Plan

Planning is a crucial task in web development, in which we will save a lot of time
and avoid potential risks in the long run. First, we need to get a basic idea about the
goal of this application, features and functionalities, and the structure of components
to see how it fits into WordPress.

### Sample Application Goals and Target Audience Statement:
Developers and designers who work online as freelancers know the importance
of a personal profile to show your skills for improved reputation. However, most
people, including experts who work full-time jobs don't maintain such profiles, and
hence get unnoticed among co-developers. The application developed throughout
this book is intended to provide the opportunity for web professionals to create
their public profiles and connect with the experts in the field.

#### Planning the Application
Basically, our application consists of both frontend and backend, which is common
to most web applications. In the frontend, both registered and unregistered users
will have different functionalities based on their user roles. The following diagram
shows the structure of our application home page:

![wpad](https://github.com/vgorbic1/Tutorials/blob/master/WordPress/App-Development/images/wpad1.jpg)

The backend will be developed by customizing the built-in admin features of
WordPress. Existing and new functionalities of the admin area will be customized
based on the user role permissions.

#### User roles of the application
Application consists of four user roles, including the built-in admin role. 
Registration is required for all the four user roles in the portfolio
management application. User roles
and their respective functionalities are explained in the following section:
- Admin: This manages the application configurations, settings, and
capabilities of the users.
- Developer: This is the user role common to all web professionals who want
to make profiles. All the developers will be able to create complete profile
details to enhance their reputation.
- Members: These are normal users who want to use the things created
by developers and designers. They will be able to access and download
the work made public by developers. Basically, members will have more
permission to directly interact with developers, compared to subscribers.
Also, we can implement premium content section in future for paid
members.
- Subscribers: These are also normal users who want to follow the activities
of their preferred developers. These users will be notified whenever their
preferred developers create a new activity within application.

#### List of features and functionality
Developer profile management: Users who register as developers will
be given the opportunity to construct their profile by completing content
divided into various sections such as services, portfolio, articles, and books.
- Frontend login and registration: Typically, web applications contain the
login and registration in the frontend, whereas WordPress provides it on the
admin area. Therefore, custom implementation of login and registration will
be implemented in the application frontend.
- Settings panel: Comprehensive settings panel will be developed for
administrators to configure general application settings from the backend.
- XML API: A large number of popular web applications come up with a fully
functional API to allow access to third-party applications. In this application,
we will be developing simple API to access the developer details and
activities from external sources.
- Notification service: A simple notification service will be developed to
manage subscriptions as well as manage updates about the application
activities.
- Responsive design: With the increase of mobile devices in Internet browsing,
more and more applications are converting their apps to suit various devices.
So, we will be targeting different devices for fully responsive design from the
beginning of the development process.
- Third-party libraries: Throughout the book, we will be creating
functionalities such as OpenAuth login, RSS feed generation, and template
management to understand the use of third-party libraries in WordPress.
