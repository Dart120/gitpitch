# Submission

## I assume we're allowed to submit extra JSON files with the submission, if for example we are saving IDs in a JSON file which make requests as specific parameters to an API?

Yes no problem

# Client-side functionality

## Can I use react to build our web-site?

Yes (this is a client-side framework). Similar frameworks include
angular and vue. They won't be taught though, and you need to be
sure that your HTML code is compliant, and that is is unmistakably
clear how to build the code.

## Is using fetch to manage the http requests mandatory? Or can I use another javascript library for sending requests such as JQuery AJEX or Axios?

You want people to be able to understand your code, and I expect
everybody to understand the use of fetch. jQuery and Axios are
external libraries, fetch is core to the language, and inspired by the
developments that jQuery has made. I used to teach jQuery as the best
way to do this, but have moved to fetch instead as that is the way
that people are moving across the industry. jQuery has been a very
important part of the ecosystem for a long time, but it is waning -
[Bootstrap 5 will remove jQuery as a
dependency](https://news.ycombinator.com/item?id=19147466).

Axios has some advantages over fetch, mainly for tracking the progress
of large uploads. Other benefits of axios are diminishing as the core
language develops. If you look at examples with Axios they tend not to
use async/await, which is the new way of doing things. External
libraries increase page load time, particularly on the client side, so
should be avoided where there are core language alternatives. By the time you are looking for a job most likely fetch will be the way everybody does things.

## If I were to include an interactive calendar in my website, would I have to create one from scratch or could I use one that already exists online? It would be properly credited of course.

It’s more than fine to use an existing one - it’s a good idea.

## Are we allowed to use template engines such as pug to transform a template into a HTML file?

In principle templating is OK, but remember that updates to the page should take place in-page via AJAX, rather than by reloading the whole page. So basically it needs to be for partial pages, and to work on the client side, not the server side: the server should be sending JSON, not HTML.

# Client-side quality criteria

# Server-side functionality criteria

## How are the two entities related? E.g. can the same thing be done for both entities separately, or should they be related/connected in some way?

For each entity you should provide a endpoint to list/search, get
details and add. You should also be able to find how one entity object
relates to another, e.g. who posted a photo, which tags are related
to which recipe etc. This could either be through the get details GET
request, and/or through search and/or through another web service
endpoint.

## Is something like Google Firebase be allowable?

Firebase provides a server-side database as an external service.

The assignment specification says that 

> Local installation must not use database: use in-memory model

This is because you can’t require everybody to install and configure
local databases. Also, if you want to use an external database and you
want people to run your code to test it, you will have to provide them
with your credentials, which would almost certainly break the Ts&Cs
for Firebase.

In real-world development a common way to do this is to use ‘mocking’,
where you build a pretend database (typically an in-memory model) that
is part of the test setup and mock functions that the test runner
calls instead of accessing the real database. This helps in terms of
performance of running the tests, and also that your live database
isn’t affected by test operations. 

So if you want to use firebug (which is a good idea in general) then you should

1. have a mocking system in place for local testing
2. keep your credentials secret, by having a local configuration file which you don’t share. You could then give a link to the working cloud-deployment of the website for review purposes.

## What if when marking peer reviewers use the daily quota for an API request? I assume we would send this back as a response

You should make sure that your client has a way of handling and reporting this. Also make clear in the README.md any restrictions that you are aware of in terms of number of accesses.

## Are we supposed to require access tokens for the client side accessing our server through specific GET/ POST methods??

Yes for POST methods, no for GET methods

## Can I use a database like  SQLite which just works on top of a .sqlite file rather than requiring a database process to run on the host machine?

There are two points about databases here:

1. It is not reasonable to expect peer assessors to have to install and configure up to four local databases
2. We have not discussed SQL in the course, so it is not reasonable to expect a peer assessor to review SQL code

So while sqlite may not go against point 1) it does not go against point 2). And given that it has been explicitly stated that a local database should not be used, it would not be unreasonable for somebody to mark you down if you did (I would). This applies to the assignment as a whole - there must be a locally deployable non-database implementation that a peer assessor can execute and evaluate.

# Server-side quality


## I can't find much/any info on content-type and correct usage of this

Your web service should be sending JSON. If you use the standard express `res.send` or `res.json` functions then the correct content-type will be set for you. The [example test cases](https://github.com/stevenaeola/gitpitch/blob/master/prog/nodejs_testing/app.test.js) include a test for the correct content-type.

## How do I make sure I am using the right HTTP codes

In normal operation, express will set the correct response code. If you want to set an error code then use e.g. `res.status(400)`. The [example test cases](https://github.com/stevenaeola/gitpitch/blob/master/prog/nodejs_testing/app.test.js) include test for the correct http response code.

## The marking criteria says that eslint should run with the command "npm pretest". However, npm won't let me run that as it's not recognised as a command

Any script that you include in the pretest script of your `package.json` will be executed before the test script if you execute `npm test`. To run pretest by itself with `npm run pretest`.

## How do I mock an external API call?

I've updated the potatoes example on github to

* check a login function in the post method
* put the login in a separate module
* mock the login functionality with JEST

# Extensions

# General

## What if we have certain bugs after submitting which aren't related to our code? For example today it was highlighted that Youtube wasn't able to sort requests by date (both on their website and the API)

If such a bug has always been there it is down to you as the developer to deal with it e.g. by sorting restuls on the client side. If a site is temporarily down or having problems then you should be reporting problems to the user, maybe encouraging them to try again later.


