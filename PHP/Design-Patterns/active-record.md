##The ActiveRecord Pattern
The last pattern that we will examine is the Active Record pattern. This is
used to encapsulate access to a data source so that the act of accessing its
components—both for reading and for writing—is, in fact, hidden within the
class that implements the pattern, allowing its callers to worry about using the
data, as opposed to dealing with the database.

The concept behind Active Record is, therefore, quite simple, but its
implementation can be very complicated, depending on the level of
functionality that a class based on this pattern is to provide. This is usually
caused by the fact that, while developers tend to deal with database fields
individually and interactively, SQL deals with them as parts of rows that must
be written back to the database atomically. In addition, the synchronization of
data within your script to the data inside the database can be very challenging,
because the data may change after you’ve fetched it from the database without
giving your code any notice.
