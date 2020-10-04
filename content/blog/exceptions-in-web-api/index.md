---
title: "Exceptions in Web API"
date: 2018-02-18
description: import from previous blog.
---
[Reference Repository](https://github.com/mikeruhl/WebApiExceptions)

I was recently asked a technical question about Exception handling in Web API that I didn't have much knowledge in. This is in regards to the wonderful world of Exception Handlers. These beauties are global handlers for your Web API project that can/will/should handle your exceptions globally for you. The application of these is to not only write more predictable code, but it heavily reinforces the DRY principle. I can't tell you how many times I've written the same `return UnAuthorized()` or `return BadRequest()` for several routes just to have to later come back through and refactor them all. By global implementing custom (or included) exceptions, we can get consistent behavior from the application via the exception handler that would normally be left up to the controller.

There are grandients leading up to an exception handler too. There are attribute filters where you can specify exception handling down to the controller or method (depending upon which you decorate). There is also exception logging that can be implemented. I explore all these options in the github respository linked above.

You may notice that the global exception handler gets called for all of the thrown exceptions. Awesome detective work! While it is global to the app, I've coded it to filter based on level 4 exceptions to show an example of gracefully handling the exception.

Final note: By globally logging and handling your exceptions, you're giving better usability to the caller along with better visibility to your developer. I am foaming at the mount at implementing an Exception Logger that shoots that exception over to ElasticSearch. This would be a great way to mock Application Insights: gaining telemetry data on the fly.

This code is provided as-is and is in no way intended for a production environment. It was written for readability and simplicity and does not implement any security checks. Simplicity was favored over design patterns and principles. So use at your own risk!

More information is available in the readme.md file in the repository linked above.



