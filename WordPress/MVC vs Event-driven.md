## The MVC versus event-driven architecture
A vast majority of web development frameworks are built to work with MVC
architecture, where an application is separated into independent layers called
models, views, and controllers. In MVC, we have a clear understanding of what goes
where and when each of the layers will be integrated in the process.

So, the first thing most developers will look at is the availability of MVC in
WordPress. Unfortunately, WordPress is not built on top of the MVC architecture.
This is one of the main reasons why developers refuse to choose it as a development
framework. Even though it is not MVC, we can create custom execution process to
make it work like a MVC application. Also, we can find frameworks such as WP
MVC, which can be used to take advantage of both WordPress's native functionality
and a vast plugin library and all of the many advantages of an MVC framework.

Unlike other frameworks, it won't have the full capabilities of MVC. However,
unavailability of the MVC architecture doesn't mean that we cannot develop quality
applications with WordPress. There are many other ways to separate concerns in
WordPress applications.

WordPress on the other hand, relies on a procedural event-driven architecture with
its action hooks and filters system. Once a user makes a request, these actions will
get executed in a certain order to provide the response to the user.

In the event-driven architecture, both model and controller code gets scattered
throughout the theme and plugin files. However, there is a way to
separate these concerns with the event-driven architecture, in order to
develop maintainable applications.
