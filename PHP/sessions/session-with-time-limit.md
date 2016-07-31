## Setting a time limit on sessions
When the session first starts, typically when the user logs in, store the current time in a session variable. Then compare it with the lates time whenever the user does anything that treiggers a page to load. If the difference is greater than a predetermined limit,  destroy the session and its variables. Otherwise, update the variables to the latest time.
