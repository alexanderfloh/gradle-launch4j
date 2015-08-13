
Introduction
============

The gradle-launch4j plugin uses [launch4j](http://launch4j.sourceforge.net/) to create windows .exe files for java applications.

Tasks
-----
There are 8 tasks:

  * generateXmlConfig - Creates XML configuration file used by launch4j.
  * copyL4jLib - Copies the project dependency jars in the lib directory.
  * copyL4jBinLib - Copies the launch4j jars in the bin and bin/lib directories.
  * unzipL4jBin - Unzips the launch4j working binaries in the bin directory.
  * createExeWithBin - Runs the launch4j binary to generate an .exe file.
  * createExeWithJar - Runs the launch4j jar to generate an .exe file.
  * createExe - Placeholder task to run launch4j to generate an .exe file.
  * launch4j - Placeholder task that depends on the above.

Launch4j must not be installed separately anymore, but can be used from the *PATH* with the configuration parameter `externalLaunch4j = true`.

Configuration
-------------

The configuration follows the structure of the launch4j xml file. See the launch4j documentation for the meanings. The gradle-launch4j plugin tries to pick sensible defaults based on the project. The only required
value is the mainClassName.

An example configuration within your build.gradle for use in all Gradle versions might look like:

    buildscript {
      repositories {
        maven {
          url "https://plugins.gradle.org/m2/"
        }
      }
      dependencies {
        classpath "gradle.plugin.edu.sc.seis.gradle:launch4j:1.3.0"
      }
    }

    repositories {
      mavenCentral()
    }

    apply plugin: "edu.sc.seis.launch4j"

    launch4j {
      mainClassName = "com.example.myapp.Start"
      icon = 'icons/myApp.ico'
    }

The same script snippet for new, incubating, plugin mechanism introduced in Gradle 2.1:

    plugins {
      id "edu.sc.seis.launch4j" version "1.3.0"
    }

    launch4j {
      mainClassName = "com.example.myapp.Start"
      icon = 'icons/myApp.ico'
    }

See the [Gradle User guide](http://gradle.org/docs/current/userguide/custom_plugins.html#customPluginStandalone) for more information on how to use a custom plugin.

The values configurable within the launch4j extension along with their defaults are:

 *    String launch4jCmd = "launch4j"
 *    boolean externalLaunch4j = false
 *    String outputDir = "launch4j"
 *    String xmlFileName = "launch4j.xml"
 *    String mainClassName
 *    boolean dontWrapJar = false
 *    String headerType = "gui"
 *    String jar = "lib/"+project.tasks[JavaPlugin.JAR_TASK_NAME].archiveName or "", if the JavaPlugin is not loaded
 *    String outfile = project.name+'.exe'
 *    String errTitle = ""
 *    String cmdLine = ""
 *    String chdir = '.'
 *    String priority = 'normal'
 *    String downloadUrl = "http://java.com/download"
 *    String supportUrl = ""
 *    boolean stayAlive = false
 *    boolean restartOnCrash = false
 *    String manifest = ""
 *    String icon = ""
 *    String version = project.version
 *    String textVersion = project.version
 *    String copyright = "unknown"
 *    String companyName = ""
 *    String description = project.name
 *    String productName = project.name
 *    String internalName = project.name
 *    String opt = ""
 *    String bundledJrePath
 *    boolean bundledJre64Bit = false
 *    boolean bundledJreAsFallback = false
 *    String jreMinVersion = project.targetCompatibility or the current java version, if the property is not set
 *    String jreMaxVersion
 *    String jdkPreference = "preferJre"
 *    String jreRuntimeBits = "64/32"
 *    String mutexName
 *    String windowTitle
 *    String messagesStartupError
 *    String messagesBundledJreError
 *    String messagesJreVersionError
 *    String messagesLauncherError
 *    Integer initialHeapSize
 *    Integer initialHeapPercent
 *    Integer maxHeapSize
 *    Integer maxHeapPercent
 *    String splashFileName
 *    boolean splashWaitForWindows = true
 *    Integer splashTimeout = 60
 *    boolean splashTimeoutError = true

 Take a look at the [Launch4j documentation](http://launch4j.sourceforge.net/docs.html#Configuration_file) for valid options.
