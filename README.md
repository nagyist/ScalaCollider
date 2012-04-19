## ScalaCollider

### statement

ScalaCollider is a SuperCollider client for the Scala language. It is (C)opyright 2008-2012 by Hanns Holger Rutz. All rights reserved. ScalaCollider is released under the [GNU General Public License](http://github.com/Sciss/ScalaCollider/blob/master/licenses/ScalaCollider-License.txt) and comes with absolutely no warranties. To contact the author, send an email to `contact at sciss.de`

### requirements / installation

ScalaCollider currently builds with xsbt (sbt 0.11) against Scala 2.9.2. It requires Java 1.6 and SuperCollider 3.5 or higher. It depends on [ScalaOSC](http://github.com/Sciss/ScalaOSC) and [ScalaAudioFile](http://github.com/Sciss/ScalaAudioFile).

Targets for sbt:

* `clean` &ndash; removes previous build artefacts
* `compile` &ndash; compiles classes into target/scala-version/classes
* `doc` &ndash; generates api in target/scala-version/api/index.html
* `package` &ndash; packages jar in target/scala-version
* `console` &ndash; opens a Scala REPL with ScalaCollider on the classpath

Running `sbt update` should download all the dependencies from scala-tools.org (In the course of the next half year, we will migrate to Sonatype).

### starting a SuperCollider server

The following short example illustrates how a server can be launched and a synth played:

```scala
    
    import de.sciss.synth._
    import ugen._
    
    val cfg = Server.Config()
    cfg.programPath = "/path/to/scsynth"
    // runs a server and executes the function
    // when the server is booted, with the
    // server as its argument 
    Server.run( cfg ) { s =>
       // play is imported from package de.sciss.synth.
       // it provides a convenience method for wrapping
       // a synth graph function in an `Out` element
       // and playing it back.
       play {
          val f = LFSaw.kr( 0.4 ).madd( 24, LFSaw.kr( Seq( 8, 7.23 )).madd( 3, 80 )).midicps
          CombN.ar( SinOsc.ar( f ) * 0.04, 0.2, 0.2, 4 )
       }
    }
    
```

You might omit to set the `programPath` of the server's configuration, as ScalaCollider will by default read the system property `SC_HOME`, and if that is not set, the environment variable `SC_HOME`. Environment variables are stored depending on your operating system. On OS X, if you use the app-bundle of ScalaCollider-Swing, you can access them from the terminal:

    $ touch ~/.MacOSX/environment.plist
    $ open ~/.MacOSX/environment.plist

On the other hand, if you run ScalaCollider from a Bash terminal, you instead edit `~/.bash_profile`. The entry is something like `export SC_HOME=/path/to/folder-of-scsynth`. On linux, the environment variables probably go in `~/.profile`.

For more sound examples, see `ExampleCmd.txt`. There is also an introductory video for the [Swing frontend](http://github.com/Sciss/ScalaColliderSwing) at [www.screencast.com/t/YjUwNDZjMT](http://www.screencast.com/t/YjUwNDZjMT).

### creating an IntelliJ IDEA project

If you want to develop the sources of ScalaCollider, the recommended way is to use IntelliJ IDEA. To create the project files, proceed as follows. If you have not installed the sbt-idea plugin yet, create the following contents in `~/.sbt/plugins/build.sbt`:

    resolvers += "sbt-idea-repo" at "http://mpeltonen.github.com/maven/"

    addSbtPlugin("com.github.mpeltonen" % "sbt-idea" % "1.0.0")

Then to create the IDEA project, run the following two commands from the xsbt shell:

    > set ideaProjectName := "ScalaCollider"
    > gen-idea

### download and resources

The current version can be downloaded from [github.com/Sciss/ScalaCollider](http://github.com/Sciss/ScalaCollider).

More information is available from the wiki at [github.com/Sciss/ScalaCollider/wiki](http://github.com/Sciss/ScalaCollider/wiki).

A mailing list is available at [groups.google.com/group/scalacollider](http://groups.google.com/group/scalacollider).
