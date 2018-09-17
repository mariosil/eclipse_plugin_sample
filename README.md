# Eclipse_plugin_sample
This is a Hello world Eclipse plug-in example to test building automations with Apache Ant.

## About the com.kwantec.helloworld plugin example.
* I have created an Eclpse-Plugin project called `com.kwantec.helloworld`.
* This project was created by using one of the templates provided by the Eclipse PDE.
* This plugin makes a menu contribution in the main menu of the Eclipse host installation.
    * It adds a simple menu "___Sample Menu___" which contains a unique "___Say hello world___" submenu.
    * This "Say hello world" sub-menu opens an information message dialog with the message "___Hello, Eclipse world___".
* This plugin also contributes with a command 'Ctrl+6' in the window context, so the same information message will opens.
* The build.xml Ant file of this project was originally created with the Ant Plugin tool provided by Eclipse.
    * This build.xml file was modified and reduced to only leave the minimum required task.
    * Once these modification were done, now it's possible to execute the script directly by Ant in command line.

### Required libraries for plugin example
* JRE System Library
    * __JavaSE-1.8__
* Plug-in Dependencies
    * `org.eclipse.ui_3.109.100.v20180426-0903.jar`
    * `org.eclipse.swt_3.107.0.v20180611-0422.jar`
    * `org.eclipse.swt.gtk.linux.x86_64_3.107.0.v20180611-0422.jar`
    * `org.eclipse.jface_3.14.0.v20180423-0714.jar`
    * `org.eclipse.core.commands_3.9.100.v20180404-1234.jar`
    * `org.eclipse.ui.workbench_3.111.0.v20180524-1156.jar`
    * `org.eclipse.e4.ui.workbench3_0.14.100.v20180403-0945.jar`

### Before to run the Ant scripts
1. In the example project, locate file `<workspace>/com.kwantec.helloworld/build.xml` which corresponds to the Ant build script.
2. Then in the `build.xml` file locate a target with name _@dot_. 
    - You may note this target contains a set of _pathelements_ grouped into a `path id="@dot.classpath"`.
    - These _pathelements_ makes reference to the paths where required (_.jar files_) _plug-in dependencies_ are located.
    - It's possible that this references have to be modified in order to point to the right location where the required jars are located in your machine.

### Running the build.xml script by only using Ant
This are the command line instructions to execute the `build.xml` script by using __Ant__ in _Linux (Ubuntu 18.04LTS)_:
```sh
ant -DbuildDirectory /<directory_where_build_occurs> -buildfile /<workspace>/<project_folder>/build.xml <target>
```
* Where `/<directory_where_build_occurs>` it's the path to the folder where the buld will occurs.
* Where `/<workspace>/<project_folder>/` it's the path to our plug-in project folder which contains the `build.xml` file.
* Where `<target>` is one of the tasks included into the `buil.xml` file (eg: _clean_, _build.jars_, _zip.src_).

For this example we are interested on task: __build.update.jar__ as this task creates the `.jar` file that represents the plugin. 
This `.jar` file could be then dropped into the __/dropins__ folder of our Eclipse installation so it be available as installed plugin in our Eclipse IDE after restart it.
By default, the `.jar` file will be created in the same project folder directory (`/<workspace>/<project_folder>/`), with the same nama sa the project. In our case, the name of the `.jar` will be: `com.kwantec.helloworld.1.0.0.<bundle_version>.jar`, where `<bundle_version>` is the date of the date when the file was built.

##### This is how I'm running in my local machine:
Just as example:
```sh
ant -DbuildDirectory /home/msilveira/eclipse-workspace/com.kwantec.helloworld/mybuild -buildfile ~/eclipse-workspace/com.kwantec.helloworld/build.xml build.update.jar
```

### After run _Ant_
After run _Ant_, a new file  `com.kwantec.helloworld.1.0.0.<bundle_version>.jar` will be generated into the same project folder. We can then take this `.jar` file and drop into the `/dropins` folder of our current Eclipse installation like if we were doing a manual plug-in installation. 
Then we have to restart our Eclipse in order to see the plug-in contributions of this example in the main menu. 

Our Eclipse main menu should looks like this: 
![Eclipse main menu contribution Sample Menu]()

On click over ___Sample Menu___->___Sample Command___, a simple message dialog should be displayed:
![Hello world message dialod]()
