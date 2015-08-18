# Introduction #

This project it meant to simplify and decouple integration between a view level class and the Hibernate calls that power the page. This is one of those things that should have been in Hibernate since at one point in time, almost all developers need this functionality but its not supplied by Hibernate itself.


# Details #

Core features and goals:
  * Easy to use and extend
  * The view code should never have to know any database specifics
  * The Database DAO's should never have to know magic names of the front end logic.


# Examples #

  * [Filter Example Page](Easy.md) - Quick example of code that must be written
  * [Table Filter Example Page](Multi.md) - A much more advanced example, involving table join lookups.
  * [Sort Example Page](Easy.md) - Quick example of code that must be written
  * [Table Sort Example Page](Multi.md) - A much more advanced example, involving table join lookups.
  * [Example Page](Pagination.md) - Quick example of code that must be written