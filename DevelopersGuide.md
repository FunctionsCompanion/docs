---
layout: default
title: Developers Guide
nav_order: 6
---
# Functions Companion Developers Guide

Functions Companion requires that functions be invoked via an Apex class that 'wraps' function invocations and logs invocation data. The Apex Class gets installed along with a Lightning App during Functions Companion [installation](https://functionscompanion.github.io/InstallAndConfig/). When a function is invoked via this wrapper, it is recorded though the invocation of an Apex Syslog logger function, `apexsyslogjs`, which must be installed into your project. 

The functions themselves must also be instrumented with a function logger to capture memory consumtion and execution times. For this, there are 2 function loggers, one for JavaScript functions, the other for Java Functions. 

The [JavaScript_Tests](https://github.com/FunctionsCompanion/JavaScript_Tests)
and [Java_Tests](https://github.com/FunctionsCompanion/Java_Tests) repos include several examples of how to instrument functions. The follwing sections describes how each logger should be built in to your functions.

## Apex Logger

The Functions Companion Package installs a wrapper class in the target org that logs Apex activity by invoking a JavaScript function called `apexsyslogjs`. This function forwards Apex invocation activitity and org status to the Function Companion platform. 

1. Install `apexsyslogjs` in your Project along with your other functions. There is no Java implemention, but it can still be installed in Projects that have Java functions. 

![Image: image8.png](/assets/images/image8.png)

You can copy the apexsyslogjs function [source](https://github.com/FunctionsCompanion/JavaScript_Tests/tree/main/functions/apexsyslogjs) from the [JavaScript_Tests](https://github.com/FunctionsCompanion/JavaScript_Tests) repo. 

2. The `apexsyslogjs` functions uses the `sf-fc-logger` npm module and needs to be added as a dependency to your `package.json`.

```
"dependencies": {
    "sf-fc-logger": "^1.3.0"
  },
```

## Instrument your functions

Once you have added the Apex logger function, you then must instrument each of your functions to log data. 

### JavaScript Functions

```
import { fc } from 'sf-fc-logger';
export default await fc(async (event, context, logger) => {
// Your function Javascript here...
});
```

Functions must be invoked via new the methods `FCFunction.getAndInvoke()` and `FCFunction.getAndQueue()`which combines the `.get()` and `invoke()` methods for functions into one call as shown:

Sync
 * `FCFunction.getAndInvoke('FC_Test_Project1.qna', Jsonpayload);`

Async
 * `FCFunction.getAndQueue('FC_Test_Project1.irisclassifier', Jsonpayload1, 'FCCallback' );`

Functions Companion puts asynchronus invocations on an internal queue where they are invoked using a rate limiting throttle to prevent overrunning org API limits. Dashboard stats show how long an asynchronous invocation remains in the queue before the function executes.

## Java Functions

There are examples of how to instrument your Java function in the [Java_Tests](https://github.com/FunctionsCompanion/Java_Tests/blob/main/functions/01_Intro_ProcessLargeData_Java/src/main/java/com/salesforce/functions/recipes/ProcessLargeDataFunction.java#L35) repo.

