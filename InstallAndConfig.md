---
layout: default
title: Installation and Configuration
nav_order: 3
---

# Installation and Configuration

Functions Companion is an observability, performance and cost management solution for Salesfore Functions. It consists of
a Lightning App that gets installed into your org, along with a logging library that the developer uses to instrument
their functions source code.

The Lightning App includes Apex Classes that the developer uses to 'wrap' their function invocations to gather
operational and performance data. Functions Companion also includes an invocation queue and throttle mechanism that
enables rate control for asynchronous functions. Data is forwarded to the (external) Functions Companion log processing
platform for display in the Functions Companion Lightning Dashboards.

Installation scripts are included in the [JavaScript_Tests](https://github.com/FunctionsCompanion/JavaScript_Tests)
and [Java_Tests](https://github.com/FunctionsCompanion/Java_Tests) repos. Choose whichever language you prefer and
clone it to your local development envrionment.

* [JavaScript_Test](https://github.com/FunctionsCompanion/JavaScript_Tests)
* [Java_Test](https://github.com/FunctionsCompanion/Java_Tests)

1. Begin by authorizing to a DevHub that is enabled for Functions. From there you will create a scratch org, install
   Functions Companion and deploy your functions.

   `sfdx force:auth:web:login --setdefaultdevhubusername`

   When the login page appears, log in to your DevHub.

2. If you do not already have a target org for Functions Companion, you can create one using the included `buildit.sh`
   script, which creates a scratch org for testing. If you run this script, be sure to note the scratch org username
   since you will need is for subsequent setup steps.

```
$ ./buildit.sh
Enter a name for the new Scratch org. Make a note of the username. It will be needed to set up the Functions Companion
test envrionment. Scratch org Name:JS_TEST_ORG
{
  "status": 0,
  "result": {
    "orgId": "00DR0000002JvLvMAK",
    "username": "<your-test-org-username>"
  }
}
sfdx force:org:create -f config/project-scratch-def.json --setalias JS_TEST_ORG --durationdays 30 --setdefaultusername --json --loglevel fatal
```

When complete and successful, you should be able to run `sf env list --all` and see the Dev Hub org and the new Scratch
Org.

```
$ sf env list --all
Salesforce Orgs
===============================================================================================
| Aliases Username       Org ID             Instance Url                     Auth Method Config 
| ─────── ────────────── ────────────────── ──────────────────────────────── ─────────── ────── 
|         fcdemo@fc.com 00D8c000006eGl0EAE https://fcdemo.my.salesforce.com web                

Scratch Orgs
=======================================================================================================================================
| Aliases     Username                      Org ID             Instance Url                                          Auth Method Config 
| ─────────── ───────────────────────────── ────────────────── ───────────────────────────────────────────────────── ─────────── ────── 
| JS_TEST_ORG <your-test-org-username> 00DR0000002JvLvMAK https://speed-computing-6920-dev-ed.my.salesforce.com web   
```

3. For Functions Companion to access the target the org, it needs to auth as a Connected App. The current release
   requires auth via username and password. Scratch orgs do not enable this by defailt so you will need to enable
   password access and get password via the follwing command:

`$ sfdx force:user:password:generate --targetusername <your-test-org-username>`

```
$ sfdx force:user:password:generate --targetusername <your-test-org-username>
WARNING: The --targetdevhubusername flag is deprecated and will be removed in v57 or later.
Successfully set the password "rmtw$9Equngkv" for user <your-test-org-username>.
You can see the password again by running "sfdx force:user:display -u <your-test-org-username>".
```

Make a note of the username and password. You will need it in the next step when you configure the Connected App. You
will also need this username when you run the test scripts.

4. Now that you have a scratch org for testing, you can install Functions Companion.
   The `install.sh` [script](https://github.com/FunctionsCompanion/JavaScript_Tests/blob/setup/install.sh) will install
   the latest version of Functions Companion and configure it. From the repo's directory, run `install.sh` and when
   prompted provide username. 

```
$ ./install.sh                      
Please provide the username for the target org you wish to install Functions Companion.
username:<your-test-org-username>
Installing v1.20 of Functions Companion
sfdx force:package:install --wait 10 --package 04t8c000001AHeq -u <your-test-org-username>
Waiting for the package install request to complete. Status = IN_PROGRESS
Waiting for the package install request to complete. Status = IN_PROGRESS
Successfully installed package [04t8c000001AHeq]

Configuring the package and installing a dummy API key: XXXXXXX-XXXXXXX-XXXXXXX-XXXXXXX.
Be sure to update with a valide API key after you create your Connected App.
sfdx force:data:tree:import -p ./data/FC_Settings__c-plan.json -u <your-test-org-username>
=== Import Results

 Reference ID       Type           ID                 
 ────────────────── ────────────── ────────────────── 
 FC_Settings__cRef1 FC_Settings__c a00R000000H2NHhIAN 
sfdx force:data:tree:import -p ./data/fcConfig__c-plan.json -u <your-test-org-username>
=== Import Results

 Reference ID    Type        ID                 
 ─────────────── ─────────── ────────────────── 
 fcConfig__cRef1 fcConfig__c a01R000000GZHtNIAX 
```

Functions Companion is now installed and configured in your org and ready for connecting to the Functions Companion
logging platform.

See [Getting Started](GettingStarted.md) for details on setting up Functions Companion as a Connected App to your org.
