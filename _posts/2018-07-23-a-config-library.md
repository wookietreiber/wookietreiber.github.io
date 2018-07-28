---
title: a config library
tags:
  - config
  - library
---


I write command line tools, both at work and for fun. I prefer to use the
command line as my main interface. I have long been wishing for a configuration
library that does a little more than just parse command line arguments. Here is
what I have in mind.


## goals

1.  **unified definition**

    Have a single place where to define the configuration and its
    documentation. This avoids duplication and keeps us DRY.

    I never would want to write both command line `--help` and a man page.
    Seems like duplicated effort.

2.  **consistency across usage and documentation**

    This is a direct benefit of the first goal, the unified definition. When we
    define everything in a single place, it's harder to introduce
    inconsistencies.

3.  **scalability**

    I want to be able to scale from small tools of a usage like `app [input]`
    to multi sub-command tools like git. The configuration definition should be
    able to be freely mixed together in different tools. A small tool should be
    easy to define while a larger tool or set of tools should be able to be put
    together without duplication.


## capabilities

From the unified definition we should be able to do the following fulling
automatically:

**programming language agnostic:**

- generate man pages
  - **man1** for all command line tools
  - **man5** for all configuration files
- generate shell auto-completion

**programming language specific:**

- generate the command line argument parser
- generate the `--help` output
- integrate handling of environment variables
- integrate configuration file parser
- integrate configuration file locator (freedesktop.org base directory
  specification)

Since we have the unified definition elsewhere, from the source code of an app
only minor snippets of code should be required:

```scala
object myapp extends App {
  val conf = Config.parse(args)

  // do some actual work
}
```


## configuration files and precedence

I would like to have clear precedence rules:

1.  **default configuration file**, e.g. `/etc/xdg/app.conf`

    - contains all defaults and serves as a reference
    - automatically generated
    - installed with distro package
    - immutable (root:root, 0444)

2.  **system configuration file**, e.g. `/etc/app.conf`

    - allows system administrator to define system-specific defaults
    - primary configuration location for system services
    - distro should backup on uninstall

3.  **user configuration file**, e.g. `~/.config/app.conf`
4.  **environment variables**
5.  **command line arguments**

Wherever it makes sense to split configuration files, instead of `app.conf`
think either `app/{a,b}.conf` or `app.d/{a,b}.conf`.


## command line options

- allow short options, e.g. `-r`
- allow long options, e.g. `--help`
- allow merged flags, e.g. `-rni` which is the same as `-r -n -i`
- do not allow long options with a single dash, e.g. `-help`, because this
  would introduce ambiguity with merged short options


## other features

- deprecated arguments, i.e. when used output deprecation warning
- ignored arguments, i.e. silently ignored, for compatibility with similar
  tools
