# gogitvers

## What is this?

__A tool to extract version info from Git repo at build time__

Freely inspired from https://github.com/jeromerg/NGitVersion
but I wanted something that could be a standalone binary without any dependency, and easy to integrate in any build workflow, including the terrible MSVC++.

Go was the perfect language for that.

## How does it work

Just run the *gogitvers* binary as part of you build script and it will generate a header file that you can include in your C/C++ project.
> ./gogitvers ../gpghelper > version.h

When a fatal error occurs (e.g. not a git repo), gogitvers will issue an *#error* statement.
(exception: when cleanliness cannot be probed, just a *//WARNING* log is dropped).
You can disable this behavior using -f option, no error will be issued but you will get unknown fields.
> ./gogitvers ../gpghelper -f > version.h

## What will I get

Something like this:
```C
/**
* gogitvers.h: file containing version identification constants
*
* THIS FILE HAS BEEN AUTOMATICALLY GENERATED, PLEASE DO NOT MODIFY
* Generated by gogitvers, visit https://github.com/thew44/gogitvers
* Mathieu ALLORY (c) 2020, Under MIT license.
*/

// Generated on: 2020-01-26 22:27:36.3642555 +0100 CET m=+0.010994101
// Source repository path: gpghelper/

#define GGVERS_HASH            "d45ee76b"
#define GVGERS_COMMIT_ID       8
#define GVGERS_ISDIRTY         0

#if defined(_DEBUG) || defined (QT_DEBUG)
# define GVGERS_DEBUG        1
# define GGVERS_FULL_VERSION    "Commit 8, Hash d45ee76b, State:Clean,DEBUG"
#else
# define GVGERS_DEBUG        0
# define GGVERS_FULL_VERSION    "Commit 8, Hash d45ee76b, State:Clean"
#endif
```