## Registry
By taking the Singleton pattern a little further, we can implement the Registry pattern. This allows us to use any object as a Singleton without it
being written specifically that way.

The Registry pattern can be useful, if, for example, for the bulk of your application, you use the same database connection, but need to connect to
an alternate database to perform a small set of tasks every now and then. If
your DB class is implemented as a Singleton, this is impossible (unless you
implement two separate classes, that is)—but a Registry makes it very easy:
