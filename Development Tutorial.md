(Partially copied from [http://source.android.com/source/downloading.html](http://source.android.com/source/downloading.html))

You want to help us developing Mirakel? Great! We changed our development process a bit to improve our code quality and to support the old android versions furthermore.

## Short story

Now we have lot of repos. That has the advantage that we can integrate our own libraries much better, but there are some changes in the development process.

To maintain all these repos we use the great tool [repo](https://code.google.com/p/git-repo/) developed by Google to manage the Android source code.

## Clone our repos


1. Make sure you have a bin/ directory in your home directory and that it is included in your path:
```sh
$ mkdir ~/bin
$ PATH=~/bin:$PATH
```
2. Download the Repo tool and ensure that it is executable:
```sh
$ curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
$ chmod a+x ~/bin/repo
```
3. Initialize a Repo client
Please add the following lines to your `~/.ssh/config`:
```sh
Host gerrit.azapps.de
	IdentityFile ~/.ssh/[YOUR KEY-FILE]
	User [YOUR GERRIT-USERNAME]
```

Please create an account on our [gerrit instance](https://gerrit.azapps.de/r/), add your [public key](https://gerrit.azapps.de/r/#/settings/ssh-keys) and init repo with the following command:
```sh
$ mkdir mirakel-android
$ cd mirakel-android
$ repo init -u ssh://[username]@gerrit.azapps.de:29418/mirakel-android
```
Replace [username] by your user name.
4. Downloading the source
```sh
$ repo sync
```

That's it. You should now have a fully working Mirakel-environment and you can start developing!

## Using Android Studio
Get the Android SDK and Android Studio from [here](http://developer.android.com/sdk/index.html)

`File` → `Import Project`

Start developing ;)


## Using Eclipse

Do not use Eclipse. We do not support Eclipse anymore

## Using Gradle

The simplest way to build Mirakel using Gradle(Version 2.1 is recommend) is:
```sh
$ gradle build
```
Of course there are some more tasks you can do:
```sh
$ gradle tasks
```
Now you should see all the possible tasks. Just select one and build it with `gradle [taskname]`


##  Using repo/git

If you fix stuff or want to implement features please use own topic branches. That help us to organize the source code better and maintain the changes better.

```sh
$ repo start BRANCH_NAME
```

Or if you want only to edit stuff in one library:

```sh
$ repo start BRANCH_NAME PROJECT
```

### Staging files

Yeah, just the old, plain `git add` command ;)

### Committing

`git commit`

### Uploading changes

Here comes the difference. First you need register an account on our gerrit page: [https://gerrit.azapps.de/r/](https://gerrit.azapps.de/r/) (that's fast, just ten seconds and you do not need enter a password).

Add your public key on the gerrit page and then you can just execute

```sh
repo sync # Update your repo
repo upload # Upload your changes
```
If repo asks you to install a git-hook, do this and ammend all commits.

That's all! More information you can find [here](http://source.android.com/source/developing.html) or just ask us!

**Happy hacking!**

## Developing

### Code structure

This part could be not up to date. Last change: 2014-06-01

We have structured our code in the following projects:

#### Helper libraries


This stuff you mostly do not need to touch. It is working fine.

* [*/acra/*](http://acra.ch/) Acra is a tool to report crashes
* */changelog/* Show the changelog on startup after an update.
* [*/colorpicker/*](https://github.com/LarsWerkman/HoloColorPicker)
* */colorpickerpreference/* The colorpicker for using in the preferences.
* [*/date-time-picker/*](https://github.com/flavienlaurent/datetimepicker) A modified picker for pick a date and a time simultaneously
* [*/donationslib/*](https://github.com/dschuermann/android-donations-lib) Donation library supporting Paypal, Flattr and Google Play
* [*/drag-sort-listview/*](https://github.com/bauerca/drag-sort-listview) The Library providing nice drag and drop functionality for listviews
* [*/ilovefs-android/*](https://github.com/azapps/ilovefs-android) An information dialog displayed on the I love FS day
* [*/progresswheel/*](https://github.com/Todd-Davies/ProgressWheel) The progresswheel shown in the Tasksfragment

#### Mirakel aka main
This is the main library including all others. Here we defined the main activities and fragments of the app.

* *main_activity* This is the main activity in Mirakel. You see it when you start the App
* * *list_fragment* All the stuff for the Navigation Drawer
* * *task_fragment* The fragment for the list of the tasks
* * *tasks_fragment* The fragment with the task details
* *static_activities* 
* * *SplashScreenActivity* The activity which is shown at startup (The Logo on black background)

#### Model
Here you can find our models. They are responsible for communicating with the database and represents our data structures.

### New_ui

Here is the experiential new ui of mirakel

#### Custom_views
This are the views we are using in the TaskFragment.

* *adapter* This are the [Adapters](http://developer.android.com/reference/android/widget/Adapter.html) we are using for the custom views
* *custom_views* This are Classes represententing special views. We use them in the TaskFragment
* *helper* Some helper classes for the views

#### tw_sync
Everything which has something to do with the taskwarrior sync.

#### Settings
Everything which has something to do with the settings part of mirakel.

#### Tests
Some tests are generated automatically. Just run `build/create_tests.py` in the main directory.

In Eclipse you can run the tests by right click → run → Android tests.
You could also use gradle to start all tests: 
```sh
$ gradle connectedAndroidTest
```

The Package structure represents the package structure in the other libraries.

More Informations for the tests you can find [here](https://github.com/MirakelX/mirakel-android/wiki/Tests).

#### Widget
Everything for the widget. Because Android < 3 has bad support for widgets there are some hacks needed.

#### Helper
Here is everything which we may need in other places. It would be nice to restructure this library.

Third party stuff:

* [*au.com.bytecode.opencsv*](http://opencsv.sourceforge.net/) The OpenCSV library for parsing CSV Files
* [*org.dmfs.provider.tasks*](https://github.com/dmfs/task-provider) The tasks provider used for the CalDAV sync

* *de.azapps.tools*
* * *FileUtils* Stuff for working with files
* * *Log* A wrapper for the Android Log class. Supports writing Logs to files. Use this class when you want to log something.
* *de.azapps.mirakel.helper*
* * *error* Classes for improved error handling
* * *\*.java* specialized helper classes for different purposes

### Tools
Tools we use for developing:

Suggestions for more/better tools are welcome!

* [*Android Studio*](https://developer.android.com/sdk/installing/studio.html) We use Android Studio, because it will be the future of android developing.
* [*Gradle*](http://www.gradle.org/) For building Mirakel
* [*Repo*](https://code.google.com/p/git-repo/) For managing our git repositories
* [*Gerrit*](https://code.google.com/p/gerrit/) For Code review. Our gerrit instance you can find here: [https://gerrit.azapps.de/r/](https://gerrit.azapps.de/r/)
* [*Sonar*](http://www.sonarqube.org/) For Metrics and code quality measurement
* [*Github*](https://github.com/MirakelX/mirakel-android/) For publishing the source code and Issue tracker
