## About Laravel
It was clear to most developers that Rails, and similar web application frameworks,
were the wave of the future, and PHP frameworks, including those admittedly imitating
Rails, started popping up quickly.

CakePHP was the first in 2005, and it was soon followed by Symfony, CodeIgniter,
Zend Framework, and Kohana (a CodeIgniter fork). Yii arrived in 2008, and Aura
and Slim in 2010. 2011 brought FuelPHP and Laravel, both of which were not quite
CodeIgniter offshoots, but instead proposed as alternatives.

It was in 2010 that Taylor Otwell, Laravel’s creator,
became dissatisfied enough with CodeIgniter that he set off to write his own framework.
The first beta of Laravel 1 was released in June 2011, and it was written completely
from scratch. It featured a custom ORM (Eloquent); closure-based routing (inspired
by Ruby Sinatra); a module system for extension; and helpers for forms, validation,
authentication, and more.

Early Laravel development moved quickly, and Laravel 2 and 3 were released in
November 2011 and February 2012, respectively. They introduced controllers, unit
testing, a command-line tool, an inversion of control (IoC) container, Eloquent relationships,
and migrations.

With Laravel 4, Taylor rewrote the entire framework from the ground up. By this
point Composer, PHP’s now-ubiquitous package manager, was showing signs of
becoming an industry standard and Taylor saw the value of rewriting the framework
as a collection of components, distributed and bundled together by Composer.
Laravel 4 also introduced queues, a mail component, facades, and database seeding.

Laravel 4.3 was scheduled to release in November 2014, but as development progressed,
it became clear that the significance of its changes merited a major release,
and Laravel 5 was released in February 2015. Laravel 5 featured a revamped directory structure, removal of the form and HTML
helpers, the introduction of the contract interfaces, a spate of new views, Socialite for
social media authentication, Elixir for asset compilation, Scheduler to simplify cron,
dotenv for simplified environment management, form requests, and a brand new
REPL (read–evaluate–print loop).

Laravel is, at its core, about equipping and enabling developers. Its goal is to provide
clear, simple, and beautiful code and features that help developers quickly learn, start,
and develop, and write code that’s simple, clear, and will last.

Laravel is a rapid application development framework. That means it focuses on
a shallow (easy) learning curve and on minimizing the steps between starting a new
app and publishing it. All of the most common tasks in building web applications,
from database interactions to authentication to queues to email to caching, are made
simpler by the components Laravel provides.

Laravel provides an entire ecosystem
of tools for building and launching applications. You have Homestead and Valet for
local development, Forge for server management, and Envoyer for advanced deployment.
And there’s a suite of add-on packages: Cashier for payments and subscriptions, 
Echo for WebSockets, Scout for search, Passport for API authentication,
Socialite for social login, and Spark to bootstrap your SaaS. Laravel is trying to take
the repetitive work out of developers’ jobs so they can do something unique.

Next, Laravel focuses on “convention over configuration”—meaning that if you’re
willing to use Laravel’s defaults, you’ll have to do much less work than with other
frameworks that require you to declare all of your settings even if you’re using the
recommended configuration. Projects built on Laravel take less time than those built
on most other PHP frameworks.

Laravel also focuses deeply on simplicity. It’s possible to use dependency injection and
mocking and the Data Mapper pattern and repositories and Command Query
Responsibility Segregation and all sorts of other more complex architectural patterns
with Laravel, if you want. But while other frameworks might suggest using those tools
and structures on every project, Laravel and its documentation and community lean
toward starting with the simplest possible implementation—a global function here, a
facade there, ActiveRecord over there. This allows developers to create the simplest
possible application to solve for their needs.
