# Scala Linters

Some notes on installing a ___formatter___ and ___code linters___ for Scala.

[The following are in alphabetical order.]

1. [scalafix](#scalafix)
2. [scalafmt](#scalafmt)
3. [scalastyle](#scalastyle)
4. [wartremover](#wartremover)

[I had good success with `scalastyle` and `wartremover` but could not get `scalafix` to work.]

## scalafix

Instructions copied from:

    https://scalacenter.github.io/scalafix/docs/users/installation

#### Setup

Add the following to `project/plugins.sbt`:

    addSbtPlugin("ch.epfl.scala" % "sbt-scalafix" % "0.5.10")

Add the following to `build.sbt`:

    // These settings must appear after scalacOptions and libraryDependencies.
    scalafixSettings
    scalafixConfigure(Compile, Test, IntegrationTest)

#### Verify Setup

To verify the installation, check that `scalacOptions` and `libraryDependencies` contain the values below.

[Note that these commands must be typed INSIDE `sbt`.]

    > show scalacOptions
    [info] * -Yrangepos                   // required
    [info] * -Xplugin-require:semanticdb  // recommended
    [info] * -P:semanticdb:sourceroot:/x  // recommended
    > show libraryDependencies
    [info] * org.scalameta:semanticdb-scalac:2.1.7:plugin->default(compile)

#### Usage

Just use `sbt` normally, the `run` command will trigger __scalafix__ if everything compiles.

## scalafmt

[This is a ___formatter___ rather than a ___linter___, but still useful.]

Instructions copied from:

    http://scalameta.org/scalafmt/#sbt-scalafmt

#### Setup

Add the following to `project/plugins.sbt`:

    addSbtPlugin("com.geirsson" % "sbt-scalafmt" % "1.4.0")

#### Usage

Creating a configuration file is optional (the defaults seem fine).

At the command line:

    $ sbt scalafmt

Once it completes it will report on the number of files reformatted:

    ...
    [info] Reformatted 3 Scala sources
    [success] Total time: 1 s, completed 20-Mar-2018 5:37:27 PM
    $

## scalastyle

Instructions copied from:

    http://www.scalastyle.org/sbt.html

#### Setup

Add the following to `project/plugins.sbt`:

    addSbtPlugin("org.scalastyle" %% "scalastyle-sbt-plugin" % "1.0.0")

#### Usage

You will need a configuration file. The easiest way to get one is to use the `scalastyleGenerateConfig`
command (at the command line, NOT inside `sbt`):

    $ sbt scalastyleGenerateConfig

This will create a `scalastyle-config.xml` in the current directory, with the default settings.

Then you can check your code with the `scalastyle` command.

At the command line:

    $ sbt scalastyle

Or inside `sbt`:

    > scalastyle

This produces a list of errors - broken down by source file - on the console, as well as an
XML result file `target/scalastyle-result.xml` (CheckStyle compatible format).

Some of the warnings may not serve a purpose in a development environment, in which case they can
easily be set to `false`.

## wartremover

Instructions copied from:

    http://www.wartremover.org/doc/install-setup.html

#### Setup

Add the following to `project/plugins.sbt`:

    addSbtPlugin("org.wartremover" % "sbt-wartremover" % "2.2.1")

Add the following to `build.sbt` (at the end seems to work):

    wartremoverErrors ++= Warts.unsafe

#### Usage

Just use `sbt` normally, the `run` command will trigger __wartremover__ if everything compiles.

## Versions

All versions current as of March, 2018.

## To Do

- [x] Add a formatter 
- [ ] Investigate why `scalastyle` generates stack traces
