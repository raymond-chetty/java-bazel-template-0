Java Bazel Template 0
=====================

** This project was originally developed on replit. https://replit.com/@raymond-chetty/JavaBazelTemplate0 This is a port to github with some modifications. Updates pending.

** DUE TO ISSUES WITH REPLIT THIS PROJECT **HAS NOT** BEEN TESTED.

A 0 dependency replit template project for java using the bazel build system.

Documentation about java and bazel can be found at the bazel website

  * https://bazel.build/docs/bazel-and-java
  * https://bazel.build/start/java
  * https://bazel.build/docs/external#external-packages

Documentation about the java programming language is available on the oracle
website.

  * https://docs.oracle.com/en/java/javase/19/
  * https://docs.oracle.com/javase/specs/jls/se19/html/index.html

JAVA, BAZEL, & BAZELISK Versions
================================

This project uses three main software components, Java, Bazel, and bazelisk.
The supported versions for this template is as follows:

### JAVA: 19.0.1
This version is configured in a few places:

* `remote_oraclejdk_linux.bzl` contains the rules and macros that are added to
  the `BUILD` and `WORKSPACE` in order to download and use oracle java. It is
  possible to switch to JAVA 17.0.5 (LTS) by changing `DEFAULT_JAVA_VERSION=17`
  in this file. The default value is `19`.

  TODO: Document oracle java configuration

* `.bazelrc` configures the default behavior for the `build`, `test`, and `run`
  bazel commands. It sets the java version for runtime, compilation, and
  testing.

These above configurations define what version of JAVA is used to run a java
binary or to compile your java source code using bazel and bazelisk. This is
different from the java version used to run `java` and `javac` at the
commandline. This project uses `replit.nix` to provision java for use on the
command line within replit. bazel and bazelisk use this version as a
`@local_jdk` and it seems to be required for proper functionality.

The default java installed within replit is JAVA 11.0.15 from OpenJDK using
`pkgs.jdk11_headless` as the package.

    https://search.nixos.org/packages?query=jdk11_headless

### BAZEL: 5.3.2
This version is defined in the `.bazeliskrc` file.

Bazelisk downloads and aliases the defined version bazel that is configured
in `.bazeliskrc` using the variable `USE_BAZEL_VERSION`.

### BAZELISK: 1.11.0
This version is defined in the `replit.nix` file.

    https://search.nixos.org/packages?query=bazelisk

All versions listed are the current latests available on the platforms provided
by replit, nixOS, bazel, and oracle. The nixOS package versions are defined by
the nixOS 22.05 release.

    https://nixos.org/blog/announcements.html#nixos-22.05

Changes to the versions of any of these pieces of software may break certain
functionality of the build. Due to how replit provisions the environments,
using nixOS, it is possible that the bazelisk and openJDK11 versions will
change when upgrading. That said, the BAZEL version is defined in the build
configurations and should be stable over time.

REPLIT
======

The .replit file defines the 'compile' and 'run' commands that power the green
"Run" button. Due to some unkown reason bazel isn't able to run on occasion,
every other run. So it may become necessary to kill the running bazel process
or cancel the stalled build command from the command line. It is suggeted that
you only initiate builds or runs from the command line.

To run bazel in a replit container

    $ bazel run @//:Main 

To get verbose output when running use the following

    $ bazel run @//:Main --verbose_failures

If the build stalls at the command line with no output press CTRL-C three times.

Java Dependencies
=================
This project is configured to use pinned dependency versions of its java
artifacts which are retrieved from maven repositories. Bazel uses 
'rules_jvm_external' to configure repositories and declare dependencies, this
configuration can be found in the 'WORKSPACE' file. The 'BUILD' file defines
which dependencies are used during the build process.

The pinned dependency versions are stored in 'maven_install.json' and must be
updated after configuration changes in order to successfully run the build with
bazel.

To update maven_install.json, run this command to re-pin the unpinned repository:

    $ bazel run @unpinned_maven//:pin

The initial file was created with the following:

    $ bazel run @maven//:pin

For additional information about 'rules_jvm_external' see the project on github.
https://github.com/bazelbuild/rules_jvm_external#pinning-artifacts-and-integration-with-bazels-downloader


There is a new dependency management system for bazel, bzlmod, which doesn't
appear to have many available java packages currently. This template doesn't
use bzlmod. bzlmod dependencies can be found in 'MODULE.bazel'. Additional
information about bzlmod and dependencies generally can be found at the bazel
website.

  * https://bazel.build/basics/dependencies
  * https://bazel.build/build/bzlmod
  * https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html

## Included Dependencies

### JUnit5

  * https://junit.org/junit5/
