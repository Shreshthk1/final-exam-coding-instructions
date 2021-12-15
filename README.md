# COMP3512 - Fall 2021 - Final Exam (Coding Portion)

**2021-12-15 (W)**

**WEIGHT: 35% of final exam mark**

## Overview

This portion of the final exam has 5 tasks. They are somewhat independent, so you can try them in any order you wish.

## Grading

Your grade on this portion of the final will depend on how many tasks you can sufficiently complete:

| # tasks sufficiently completed | mark | range  |
| :----------------------------: | ---- | ------ |
|               0                | F    | 0      |
|               1                | F+   | 25-49  |
|               2                | D+   | 55-59  |
|               3                | C+   | 67-69  |
|               4                | A-   | 80-84  |
|               5                | A+   | 95-100 |

I say "sufficiently" complete, because if you're pretty close to completion (based on my judgement), I'll squint and say "good enough under pressure".

## The Finished Product

A working version of the "site" can be found here: http://f2012-3512-final-exam-coding.herokuapp.com/public/

**You do NOT have to get things to this point to receive a reasonable mark.** If you skip some tasks - WHICH IS PERFECTLY FINE - then some things won't work. Whoop de doo. I'm just providing this completed product because it's nice to have a target to shoot for.


---

### Task: Create an API

#### Goal

When a user visits `api/cheese-api.php` **without** using a query string, they should get a **JSON response** that consists of an array with the names of all cheeses in the `cheese` table of the database. (There are 9 names.)

If a user visits the API **with** a query string, they should get a **JSON response** that consists of an empty array.

#### Files You Will Be Using

- `api/cheese-api.php`
- `helpers/query_string_helpers.php`
- `database/QueryBuilder.php`

**Don't touch any other files.**

#### What You'll Need To Do

- Add a method to `QueryBuilder.php` that returns the names of the cheeses in the `cheese` table. Give the method an expressive name.

- There is a `validApiQueryString` method in `query_string_helpers.php`; to get full marks, you should complete it and use it in your code in `cheese-api.php`.

- Add code under the `//TODO` in `cheese-api.php`, using the methods you added/completed, so that the goal of this task is reached.
  
--- 

### Task: Allow Users to Log In

#### Goal

When a user visits `public/index.php`, they are presented with a login form.

If they sign in with a valid username and password, they should be redirected to `dashboard.php?storeid=1`. Otherwise, they should be redirected back to `index.php` page.

If the user checks the 'Darkcheese?' checkbox, a persistent cookie that expires on the next National Cheese Day should be saved to the browser for domain "/".

#### Files You Will Be Using

- `partials/login-form.inc.php`
- `public/login-handler.php`
- `helpers/cookie_helpers.php`
- `database/QueryBuilder.php`

**Don't touch any other files.**

#### What You'll Need To Do

- Examine `login-form.inc.php` **but do not alter it** - it works fine. Pay close attention to the form inputs.

- There is a `fetchPassword` method in `QueryBuilder.php` that works...but is vulnerable to SQL Injection attack. For full marks, fix that. You might want to leave it alone if you're pressed for time - you can always come back to it.

- There is a `storeDarkcheesePreference` function in `cookie_helpers.php`; to get full marks, you should complete it and use it in your final result.

- Add code under the `//TODO` in `login-handler.php`, using the methods you modified/completed, so that the goal of this task is reached.

---

### Task: Use a Cookie to Style the Site with Darkcheese Mode

#### Goal

If the cookie mentioned in the previous task exists in the current session, then the site will be displayed in "Darkcheese Mode" - the page will be a dark color instead of white.

> _I had further, humourous, aspirations for this. Alas, time was my enemy._

#### Files You Will Be Using

- `partials/head.inc.php`

**Don't touch any other files.**

#### What You'll Need To Do

- If the cookie is present in the current session, add the CSS class "dark" to the `<body>` tag in this file. (Yes, that's all.)

---

### Task: Complete a Dashboard Page

#### Goal

When a user visits `public/dashboard.php?storeid=x`, they are presented with a dashboard that provides information about the current stock levels of cheeses in the store with id `x`. (The store ids can be found in the store table.) 

> _For example, if the query string is storeid=1, then stock information for the Calgary store will be displayed._

Also, the name of each cheese displayed links to a page with details about that page - that page is another task.

Finally, if a user tries to visit this page without a query string, the page will redirect to `dashboard.php?storeid=1`.

If a user tries to use any query string other than `storeid=1`, `storeid=2`, or `storeid=3`, the page will redirect to `dashboard.php?storeid=1`. There's no escaping Calgary....

#### Files You Will Be Using

- `public/dashboard.php`
- `partials/dashboard.inc.php`
- `database/QueryBuilder.php`
- `helpers/query_string_helpers.php`

**Don't touch any other files.**

#### What You'll Need To Do

- There is a `validDashboardQueryString` method in `query_string_helpers.php`; to get full marks, you should complete it and use it in your code in `dashboard.php` to handle the redirects described in the Goal.

- Add a method to `QueryBuilder.php` that returns the data you need to create the list described next. Give the method an expressive name.

- Create a well-named function in `dashboard.php` that generates an unordered list of inventory in the currently selected store. The `<li>` elements in this `<ul>` have this format:

    ```html
    <li>
      <span class="cheese-name">
        <a href="cheese-detail.php?cheeseid=5">Jarlsberg</a>
      </span>
      <span class="stock">1</span>
    </li>
    ```

- Use the previous function in `dashboard.inc.php` to display the list. I've marked where it should go with a `//TODO`.


---

### Task: Complete a Details Page

#### Goal

When a user visits `public/cheese-detail.php?cheeseid=x`, they are presented with an informational page for the cheese with the given id. (The cheese ids can be found in the cheese table.) 

> _For example, if the query string is cheeseid=4, then information about Stracchino cheese will be displayed._

Unlike `cheese-api.php` and `dashboard.php`, there is no query string checking here - if an invalid query string is provided, things are gonna bust. That's ok.

#### Files You Will Be Using

- `helpers/Cheese_Factory.php`
- `partials/detail.inc.php`
- `helpers/Cheese.php`

**Don't touch any other files.**

#### What You'll Need To Do

- Examine `Cheese_Factory.php` **but do not alter it** - it works fine. Pay close attention to the SELECT portion of the query you find there.

- Examine `detail.inc.php`. Pay close attention to how `$cheese` is used in the html. Initialize `$cheese` as described in the `// TODO`.

- Complete the `Cheese.php` class so that the call to `new Cheese($result)` in `Cheese_Factory.php` will work **and** the uses of `$cheese` in `detail.inc.php` will also work. Do not worry about any kind of error handling for the constructor.


## Submission

Submit as we've done with tutorials throughout the semester, by pushing to GitHub.

Only work submitted by the exam deadline will be marked.

Save frequently, push often.

