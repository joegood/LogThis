<p align="center">
    <a href="#logthis">
        <img alt="logo" src="logo.png">
    </a>
</p>

# LogThis

[![build](https://ci.appveyor.com/api/projects/status/github/tallesl/LogThis)](https://ci.appveyor.com/project/TallesL/LogThis)
[![nuget package](https://badge.fury.io/nu/LogThis.png)](http://badge.fury.io/nu/LogThis)

A configless .NET file logger.

Most of the time I don't need a really sophisticated file logger. And I also got tired of configuring the same thing for log4net over and over again.

This is *my* take on logging.

## How it works?

First, register your desired formats:

```cs
using LogThis;

Log.Register("Information")
Log.Register("FATAL", "An exception happened. Exception: {0}, message: {1}.")
```

Then, you just use it:

```cs
Log.This("Information", "Some crazy information!!1")
Log.This("FATAL", e.GetType(), e.Message)
```

A file named after today's date (`yyyy-MM-dddd.log`) will be created in a `log\` folder (relative from where the application is running). For instance, `2014-12-16.log`:

```
2014-12-16 19:21:45 Information Some crazy information!!1
2014-12-16 19:21:52 FATAL       An exception happened. Exception: AcmeCompany.WhateverException, Message: Shit happens.
```

## Formatting

[string.Format](http://msdn.microsoft.com/library/system.string.format) is used for formatting. If you don't want any special formatting at all just omit it when registering it.

## Old log files

There's a task, that runs in 2 hour interval, that deletes log files older than 10 days.

10 day is what I normally expect to retain when talking about log files, so I hardcoded it.

This 10 day interval is not configurable right now; if you are using the library and want to use a different interval please open an [issue](https://github.com/tallesl/LogThis/issues) or [make a pull request](https://github.com/tallesl/LogThis/pulls)

## Disabling the logging

Simply unregister all formats:

```cs
Log.UnregisterAll();
```

The library raises no error when an attempt to log with an unregistered format is made (it does nothing and returns `false`).

## .NET version

4.

## I want *this* or *that* different

Maybe you want to restrict the log size? Or log to a database? What about a fancy web interface?

In this cases, this library is not for you. May I suggest you to take a look at:

* [log4net](http://logging.apache.org/log4net);
* [NLog](http://nlog-project.org);
* [ELMAH](https://code.google.com/p/elmah).
