# learning-journal

An informal blog I am creating to track my journey becoming more hands on again having been in largely management and leadership heavy roles the past 15 years.  However, the tide is changing and it's time to make sure I have my trunks on when it goes back out.


## Sept 10-11, 2025 - Pluralsight - Typescript 5 Fundamentals

This was a pretty great course.  The examples were a bit simplistic, but the instructor really goes through Typescript language conventions and capabilities concisely. Thus far I'd been using Javascript, but after watching this video I can see how much TS brings the capabilities of OO languages like Java to the Javascript/Node universe.  Types, Classes, Interfaces, Abstract classes, Generics, you name it.  This stuff is bread and butter of what I cut my teeth on as a programmer and it will be nice to leverage it.  The other thing I then did was convert my book api entirely to typescript and get it to run.  In terms of the actual code conversion, I heavily relied on ChatGPT but had to troubleshoot it a lot with prompts.  I was able to get the book api to run again, including tests.  I also kept the old js files around but renamed them to _old.js.  


## Sept 9, 2025 - Pluralsight - Asynchronous Programming in JavaScript

Great course.  I have already worked with callbacks, promises and async/await but this course looked really good so I focused on more advanced topics I haven't really delived into yet.  Promise queuing was very cool, using Promise.all to wait for multiple simultaenous asynchronous calls to be settled before continuing, and Promise.allSettled which means that the code will wait until all are completed even if some completed in error.  This is an alternative to a catch block.  There is also Promise.any which just waits until the first promise returns or all are rejected. This would make sense if you have to call multiple external services as different alternatives and are just waiting for the first result to return.  There is also Promise.race() that just returns the first settled promise.

The create promises section clearly laid out how there are three states for promises - pending, fulfilled (resolved) or rejected.  What was interesting here was how he showed you could still have an infinite loop executing even if a promise is resolved.  He showed this with setInterval, since it would continue executing even though the promise had been fulfilled. I played around with this a bit because setInterval could be useful for heartbeat logging.  I also learned how to kill off a setInterval thread by calling clearInterval on its intervalId.

I then learned how to do concurrent processing using async/await.  Pretty cool.  Since promises return a value, you await the value getting set instead of the call to the promise itself.  This way you can write your own logic around which asynchronous calls need to be returned before you continue processing.  Neat.  It also shows how to do parallel requests using a combination of the Promise and async/await syntax.  Noting this all here so I can refer back to it as needed.

## Sept 8, 2025 - Pluralsight - Javascript Networking

I did the basic lessons on this course around using fetch and axios.  I just built a simple reverse proxy for the agify.io web service which is free to use.  I mucked around with creating .env files for changing the port the app is running on so I could use the sample app they built in the course.


## Sept 8, 2025 - O'Reilly - API Design Patterns and Designing APIs with Swagger and Open API

I didn't reaad these books cover to cover but scanned through them. I'll quickly go over where each was useful:

### API Design Patterns

I've built a lot of APIs over the years with my teams so this was good to formalize some terminology and concepts, and solidify some approaches I would like to use regularly in the future.  For example, field masks were what I used for the PATCH methods on the Book API spec but it's good to know that's what it's called.

I also liked the custom method concept.  This is where you have a resource like an email, but you want to do something like send the email after it's been saved in a draft state.  So the send call is a custom method, like: /api/email/1/send, which would send email with id=1.  I could see this being good way to deal with things like cart and ordering workflows.

LROs covered callbacks and polling, both of which are mechanisms I've used in the past.  I was thinking of implementing some simple implementations of these on the Book API, but I may hold off on that until I start building my own project.

There were a lot of other other topics covered, from jobs, to pagination, to filtering.  These are all things I've been involved in the design stages of, and I didn't get bogged down in the details covered as in reality you have to be pretty flexible and creative in how you approach this to handle business requirements.  I did like the coverage of many to many style relationships, but even here it's always a decision between making the many to many definitions a custom method of a resource, or a separate resource unto itself. To me, it all comes down to good domain modelling.

### Designing APIs with Swagger and Open API

I started going through this book, but it deals with a hypothetical implementation of an API.  These are not hard concepts to understand.  This feels like stuff I can easily tell ChatGPT to model for me in terms of syntax as long as I give it effective prompts. I don't need to become and expert in API syntax.  But I did the first few chapters for creating the minimal API structure, then adding paths. I also got the swagger editor running locally on my mac via a docker image and playing around with it as well as the redocly extension in vs code.  So when I build something fairly soon, I will start employing the concepts then.

## Sept 6, 7 2025 Pluralsight - Getting Started with Swagger 2 Tools

I've reviewed APIs using Swagger as a manager, but I want to roll up my sleeves and get more into the trenches around API design and defining a spec.  This is a good introductory course on just the tooling part.  It demonstrates openapi spec creation using a Customer object.  

While following along with the course, I decided to apply what I was learning to the simple Book API from the RESTful web services course.  I just used ChatGPT to generate the entire openapi.yaml spec for me based on the content of the controller.  This didn't turn out as well as I would have hoped. 

The overall structure was covered and a path was created for each route processed by my controller. However, what ChatGPT did was create a separate object for each path method, when in fact they all just required the Book object, ie: PUT, PATCH, POST all ended up with a separate object in the schema.  I ended up simplifying it into two objects - one that is used on the GET and has all fields, and one that is used for all the INSERT/UPDATE operations, since the ID is not specified in those.

## Sept 6, 2025 Pluralsight - JavaScript Unit Testing with Jest

[Course Link](https://app.pluralsight.com/library/courses/javascript-unit-testing-jest)

Short course and it gave me an overview of Jest. I was definitely experiencing a bit of syntax overload, so what I did was take the Book API from the previous course and convert the Sinon/Mocha/Should tests to Jest using ChatGPT prompts.  This was pretty straightforward to do, and the main challenge was converting from commonjs to ES modules, which required me to iterate through a set of prompts.

As another challenge, I added another test to the Book Controller that required a more invasive use of mock objects that replaced objects referenced internally within the code and not just passed in.  Again, for this I used ChatGPT and then I asked ChatGPT to explain the code it generated for me.

I was able to get the tests to run successfully and also learn how to use the tooling to measure overall code coverage based on some simple configurations in the `jest.config` file.


## Sept 5-6, 2025 Pluralsight - RESTful Web Services with Node.js and Express

[Course Link](https://www.pluralsight.com/courses/node-js-express-rest-web-services-update)

Let me start by saying that I love Pluralsight courses.  They seem to have the right vibe for me.  They get to the point, explain concepts clearly.  When the author tells you how to do something like build a post route on a web service, he gets to the point and is well organized.  Although I don't have access to all Pluralsight courses, I do have access to a good amount through the ACM membership learning add on, which also gives me O'Reilly and ByteCast.

In any case, this was a much better experience than the previous course.  Some of the content is dated, but because he is concise in how he covers it, I can quickly try it out, see it's dated and easily find modern remediations without difficulty.  Just flowed great. I built out a simple book api and then used this as a baseline for a few more courses.  I also spent time playing with eslint rules and understanding the framework.

I also tweaked a few things in my implementation.  For example, I used named exports for controller implementations and I used ES Modules instead of CommonJS.  This required me to tweak his approach somewhat, but it was a good learning opportunity.  I also used Mongoose as the author demonstrated.

The one part I glossed over was testing, because they are using older frameworks like Sinon, Should and Mocha and my dev teams always used Jest, which ChatGPT seemed to confirm is much more common.  I figured, why not implement the tests in Jest instead then as a next step.

## August 22 to Sept 4, 2025 Udemy - Master Node JS & Deno.js, build REST APIs with Node.js, GraphQL APIs, add Authentication, use MongoDB, SQL & much more!

[Course Link](https://www.udemy.com/share/1013ho3@VkuJHvvInYP5jasPuesST0AKyvGP5OpAG_Foxs61YK-u1PfH5Ns9m67oVJ2-bWVn/)

This was the popular Max S course for Node Beginners so I gave it a shot.  It was good for getting my feet wet with Node.js, but I didn't do all 40 hours of the videos - probably about 70% of that.  As it really caters to people who are beginners, I found it best to move onto Pluralsight courses which are more professional level.

Still, this was a good introduction to basic Node/Express concepts like Asynchronous programming, Middleware, Routers and Controllers.  However, building a web application using Express feels pretty useless in 2025 and the first 24 chapters are based on this paradigm, which was grating.  And even with REST, it would be great if it included things like following OpenAPI spec best practices, but it doesn't go into any of that so I decided to move on.

I glossed over chapters like GraphQL and Socket.io as the implementations were very rudimentary and I would rather try some Pluralsight courses that cover these topics with more of a professional lens.  One thing I did do was tweak the lessons to implement using postgres instead of mysql, just to see how easy it was to do.  That was satisfying.

What I found especially frustrating with this course is how much time the author goes through explaining syntax and concepts, only to hit Save and then realize the syntax was wrong and have to correct it.  At least for me, watching a huge amount of content in a relatively short period of time - I found this jarring.  There would also be overlays at times which say the content is out of date and to use other syntax, etc.  Honestly, when spending so much time on syntax it feels wasteful when the syntax itself is wrong.
