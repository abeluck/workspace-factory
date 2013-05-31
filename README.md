# Android Workspace Factory

The Android build system sucks, particularly Eclipse+ADT's interaction with library projects.

(Not convinced? See larger discussion [in our mailing
list](https://lists.mayfirst.org/pipermail/guardian-dev/2013-April/001530.html))


There is a semi-sane way to juggle Eclipse, ADT, and Ant for projects with
multiple library projects. The answer is to use per-app workspaces. Managing
Eclipse workspaces is a PITA though. Keeping settings synch between them is a
real bitch.

**Android Workspace Factory** can help make your life easier. It is essentially
a glorified `cp` command to help create new eclipse workspaces from a
pre-configured template.  ## Features

The included `android-workspace` is preconfigured with the following settings:

* Official Android Java Code Formatter settings
* Official Android Save Actions w/ Import Organizing
* 1.6 as the default Java compiler

## Usage

**REQUIREs ECLIPSE JUNO**

1. Clone this baby:

    ```bash
        git clone https://github.com/abeluck/workspace-factory.git
    ```

2. Create your own workspace template:

    ```bash
        cd workspace-factory/
        cp  android-workspace my-workspace
    ```

3. Configure your workspace template by opening eclipse and changing the workspace to `my-workspace`.

    Change any global settings you want: Android SDK location,
    code formatter, compiler settings, save actions, etc.

    Close eclipse when you're finished.

4. Deploy a workspace

    ```bash
        ./workspace-deploy my-workspace ~/src/new/project/path/
    ```

## Recommended Android Project Layout

This is for Android projects that use multiple external Android library
projects.

1. One workspace per application
2. Git repo root is your workspace
3. Android library projects go in /external
4. Application itself goes in /app

Example project structure with multiple apps

    ~/src                     (contains your git checkouts)
    -----/FooBarApp           (the cloned git repo & workspace!)
    ---------------/app       (App source code)
    ---------------/external  (dependency submodules)
    ------------------------/ActionBarSherlock
    -----/PineappleFiestaApp
    ---------------/app
    ---------------/external

Example projects using this layout:

* [StoryMaker](https://github.com/guardianproject/mrapp)
* [PixelKnot](https://github.com/guardianproject/PixelKnot)

From a fresh git clone, follow this procedure to setup eclipse:

1. Create new workspace in eclipse at the root of the git repo
2. For each library project in external/
       Import "Existing Android Code Into Workspace"
3. For the app/ project
       Import "Existing Projects into Workspace" (the non-Android one under the General section)
4. Happy dance

### Reasoning

1. Per-project workspace allows apps to use different versions of the
same libraries
2. Eclipse projects can be easily imported from included .project files
3. ADT requires projects exist in the workspace for relative library
project referencing to work
4. Developers don't have to juggle local changes to the
project.properties file

### What this doesn't solve

All the problems with conflicting jars, multiple android-support library
versions still exist, but oh well. At least we can hate Eclipse a little
less.


## Credits

Based on workspace copying script by Tomas Kramar <kramar.tomas@gmail.com> 2008

## Issues

Found a bug? Please create an issue here on GitHub!

https://github.com/abeluck/workspace-factory/issues
