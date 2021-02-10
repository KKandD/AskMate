# AskMate (sprint 3)

## Story

Last week you made a very good progress to improve your web application.
We need some more features to make it more usable and more appealing to users.

Users requested new features like ability to register and login.
There are a few other feature requests which you can find in the user stories.

The management would like you to separate the already working features from
the upcoming ones so your development team need to **start use branching
workflow and open new branches for the features you start in this sprint**.
As last week the ownership is in your hand so there is no compulsory stories
but of course the best case according to them if all of the stories are implemented.
So first, choose the stories and after that ask a mentor to validate it.

As last week you have a **prioritized list** of new user stories that you should
add to the unfinished stories from last weeks on your product backlog. Try to
estimate these new stories as well and based on the estimations decide how many
your team can finish until the demo. As the order is important, you should choose
from the beginning of the list as much as you can.

## What are you going to learn?

- Web routing and redirects,
- Gitflow workflow
- Advanced SQL commands (`JOIN`, `GROUP BY`, and aggregate functions)
- User authentication with sessions
- Hashed passwords
- HTML and the Jinja2 templating engine

## Tasks

1. As you will work in a new repository but you need the code from the previous sprint, add the `ask-mate-3` repository as a new remote to the previous sprint's repository, then pull (merge) and push your changes into it.
    - There is a merge commit in the project's repository that contains code from the previous sprint

2. As a user I would like to have the possibility to register a new account into the system.
    - There is a `/registration` page
    - The page is linked from the front page
    - Theres is a form on the `/registration` page when a request is issued with `GET` method
    - The form ask for username (email address), password and issues a `POST` request to `/registration` on submit
    - After submitting you are redirected back to the main page and the new user account is saved in the database
    - For a user account we store the email as username a password hash and the date of the registration

3. As a registered user, I'd like to be able to login to the system with my previously saved username and password.
    - There is a `/login` page
    - The page is linked from the front page
    - Theres is a form on the `/login` page when a request is issued with `GET` method
    - The form ask for username (email address), password and issues a `POST` request to `/login` on submit
    - After submitting you are redirected back to the main page and the given user is logged in
    - It is only possible to ask or answer a question if the user is logged in

4. There should be a page where I can list all the registered users with all their attributes.
    - There is a `/users` page
    - The page is linked from the front page when I'm logged in
    - The page is not accessible when I'm not logged in
    - Theres is a `<table>` with user data in it. The table should have these details of a user:
  - User name (link to user page if implemented)
  - Registration date
  - Count of asked questions (if binding implemented)
  - Count of answers (if binding implemented)
  - Count of comments (if binding implemented)
  - Reputation (if implemented)

5. As a user when I add a new question I would like to be saved as the user who creates the new question.
    - The user id of the currently logged in user is saved when a new question is saved

6. As a user when I add a new answer I would like to be saved as the user who creates the new answer.
    - The user id of the currently logged in user is saved when a new answer is saved

7. As a user when I add a new comment I would like to be saved as the user who creates the new comment.
    - The user id of the currently logged in user is saved when a new comment is saved

8. There should be a page where we can see all details and activities of a user.
    - There is a `/user/<user_id>` page
    - The user page of a logged in user is linked from the front page
    - The page of every user is linked from the users list page
    - Theres is a list with these deatils about the user:
  - User id
  - User name (link to user page if implemented)
  - Registration date
  - Count of asked questions (if binding implemented)
  - Count of answers (if binding implemented)
  - Count of comments (if binding implemented)
  - Reputation (if implemented)
    - There is a separate table where every **question** is listed that the user created. The related question is linked in every line.
    - There is a separate table where every **answer** is listed that the user created. The related question is linked in every line.
    - There is a separate table where every **comment** is listed that the user created. The related question is linked in every line.

9. As a user I would like to have the possibility to mark an answer as accepted.
    - On a question's page for every answer there is a clickable element that can be used to mark an answer as accepted
    - When there is an accepted answer there is an option to remove the accepted state
    - Only the user who asked the question can change the accepted state of answers
    - An accpted answer has a visual distinction from other answers

10. As a user I would like to see a reputation system to strengthen the community. Reputation is a rough measurement
 of how much the community trusts a user.
    - **A user gains reputation when:**
- her/his question is voted up: +5
- her/his answer is voted up: +10
- her/his answer is marked "accepted": +15

11. As a user I would like to see a small drop in reputation when a user's question or answer is voted down.
    - **A user loses reputation when:**
- her/his question is voted down: −2
- her/his answer is voted down: −2

12. There should be a page where I can list all the existing tags and that how many questions are marked with the given tags
    - There is a `/tags` page
    - The page is linked from the front page and a question's page
    - The page is accessible when I'm not logged in

## General requirements

- Use gitflow workflow from now on in your team projects.

## Hints

- As you have became familiar with the `CREATE` statement the management
  hasn't prepared the data model. They trust in you and they are certain
  about you can design this small extension for the current database.
  To change the already existing tables you will need to use the
  `ALTER TABLE` statement. For this you can find some help
  [here](https://www.w3schools.com/sql/sql_alter.asp).
  (Do not forget to setup the foreign keys if those are necessary)
- It's important that if the database table has a timestamp column
  then you cannot insert a UNIX timestamp value directly into that
  table, you should use:
    - either strings in the following format `'1999-01-08 04:05:06'`,
    - or if you use `psycopg2` and the `datetime` module, you can pass
      a `datetime` object to the SQL query as a parameter (you'll find
      details about Date/Time handling in psycopg2 in the background materials).
- Pay attention on the order of inserting data into the tables, because you may
  violate foreign key constraints (that means e.g. if you insert data into the
  question_tag before you insert into the tag table the corresponding tag id
  you want to refer to then it won't exist yet)! Especially it is important
  after you change the database structure with new foreign keys. Maybe it's
  worth to modify the sample data based on your changes.
- Because you have learnt about how to write complex queries and join multiple
  tables in one select maybe you should spend some time to optimise your
  previously created queries where it's applicable.
- Pay attention that some user stories have prerequisites!

## Background materials

### Git

- <i class="far fa-exclamation"></i> [Working with the `git remote` command](https://git-scm.com/docs/git-remote)
- <i class="far fa-book-open"></i> [Merge vs rebase](project/curriculum/materials/pages/git/merge-vs-rebase.md)
- <i class="far fa-book-open"></i> [Mastering git](project/curriculum/materials/pages/git/mastering-git.md)

### SQL

- <i class="far fa-exclamation"></i> [Working with more complex data](project/curriculum/materials/pages/sql/sql-working-with-data.md)
- [SQL injection](project/curriculum/materials/pages/web-security/sql-injection.md)
- [Best practices for Python/Psycopg/Postgres](project/curriculum/materials/pages/python/tips-python-psycopg-postgres.md)
- [Date/Time handling in psycopg2](https://www.psycopg.org/docs/usage.html?highlight=gunpoint#date-time-objects-adaptation)
- <i class="far fa-book-open"></i> [PostgreSQL documentation page on Queries](https://www.postgresql.org/docs/current/queries.html)
- <i class="far fa-book-open"></i> [PostgreSQL documentation page Data Manipulation](https://www.postgresql.org/docs/current/dml.html)
- [Database glossary](project/curriculum/materials/pages/sql/database-glossary.md)

### Workflow

- <i class="far fa-exclamation"></i> [Gitflow workflow](project/curriculum/materials/pages/git/git-branching.md)

### Web basics (Sessions/Flask)

- <i class="far fa-exclamation"></i> [Sessions](project/curriculum/materials/pages/web/authentication-sessions.md)
- <i class="far fa-exclamation"></i> [Salted password hashing](project/curriculum/materials/pages/web-security/salted-password-hashing.md)
- <i class="far fa-exclamation"></i> [Flask documentation](http://flask.palletsprojects.com/) (especially the quickstart#the-request-object and quickstart#sessions part)
- [Flask/Jinja Tips & Tricks](project/curriculum/materials/pages/web/web-with-python-tips.md)
- [Passing data from browser](project/curriculum/materials/pages/web/passing-data-from-browser.md)
- <i class="far fa-book-open"></i> [HTTP is stateless](project/curriculum/materials/pages/web/authentication-http-stateless.md)
- <i class="far fa-book-open"></i> [Cookies](project/curriculum/materials/pages/web/authentication-cookies.md)
- <i class="far fa-book-open"></i> [Jinja2 documentation](https://jinja.palletsprojects.com/en/2.10.x/templates/)
- <i class="far fa-book-open"></i> [Collection of web resources](project/curriculum/materials/pages/web/resources.md)
