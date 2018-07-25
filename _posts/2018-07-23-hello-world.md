---
title: a config library
tags:
  - config
  - library
---

## goals

1.  **unified definition** (spec)

    no duplication (DRY), e.g. in writing both `--help` output and man page

2.  **consistency** across usage and documentation

    a direct result of the unified definition

3.  **scalability**

    scale from small tools like `app [input]` to multi sub-command tools like git

## unification

programming language agnostic:

- man page generation
  - man1 for all command line tools
  - man5 for all configuration file formats
- shell completion generation

programming language specific:

- command line argument parser generation
  - `--help` output generation
- integration of environment variables
- integration of configuration file parser
- freedesktop.org base directory spec for location of configuration files

## configuration files and precedence

consistent, clear precedence rules, principle of least surprise

1.  default config, e.g. `/etc/xdg/app.conf`

    - contains all defaults
    - built by config spec
    - installed with distro package
    - immutable (root:root, 0444)

2.  system config, e.g. `/etc/app.conf`

    - allows system administrator to define system-specific defaults
    - primary configuration location for system services
    - distro should backup on uninstall

3.  user config file, e.g. `~/.config/app.conf`
4.  environment variables
5.  command line arguments

Wherever it makes sense to split configuration files, instead of `app.conf` think either `app/{a,b}.conf` or `app.d/{a,b}.conf`.

## command line options

- allow short options, e.g. `-r`
- allow long options, e.g. `--help`
- allow merged flags, e.g. `-rni` which is the same as `-r -n -i`
- do not allow long options with a single dash, e.g. `-help`, because this would introduce ambiguity with merged short options

## other features

- deprecated arguments, i.e. when used output deprecation warning
- ignored arguments, i.e. silently ignored, for compatibility with similar tools
