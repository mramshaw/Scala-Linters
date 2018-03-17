# Scala Linters

Some notes on installing ___code linters___ for Scala.

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

Then you can check your code with the `scalastyle` command (at the command line, NOT inside `sbt`):

    $ sbt scalastyle

This produces a list of errors on the console, as well as an XML result file
`target/scalastyle-result.xml` (CheckStyle compatible format).

Some of the warnings may not serve a purpose in a development environment, in which case they can
easily be set to `false`.

## wartremover

Instructions copied from:

    http://www.wartremover.org/doc/install-setup.html

#### Setup

Add the following to `project/plugins.sbt`:

    addSbtPlugin("org.wartremover" % "sbt-wartremover" % "2.2.1")

Add the following to `build.sbt`:

    wartremoverErrors ++= Warts.unsafe

#### Usage

Just use `sbt` normally, the `run` command will trigger __wartremover__ if everything compiles.

## Versions

All versions current as of March, 2018.
