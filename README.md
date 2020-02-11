[![VSCode Marketplace Badge](https://img.shields.io/vscode-marketplace/v/malvahq.dartsass.svg?label=VSCode%20Marketplace&style=flat-square)](https://marketplace.visualstudio.com/items?itemName=malvahq.dartsass) [![Total Downloads](https://img.shields.io/visual-studio-marketplace/d/malvahq.dartsass.svg?style=flat-square)](https://marketplace.visualstudio.com/items?itemName=malvahq.dartsass) [![Average Rating Badge](https://img.shields.io/vscode-marketplace/r/malvahq.dartsass.svg?style=flat-square)](https://marketplace.visualstudio.com/items?itemName=malvahq.dartsass) [![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](https://github.com/malvahq/vscode-plugin-dartsass/)


VSCode plugin (Visual Studio Code plugin) to compile scss files using [Dart SASS Compiler](https://sass-lang.com/dart-sass).



* [Usage](#usage)
* [Install](#install)
    * [Inside VSCode](#inside-vscode)
    * [Marketplace](#marketplace)
* [Activation](#activation)
* [Configuration](#configuration)
    * [Menus](#menus)
      * [DartSass: Sass Watch](#dartsass-sass-watch)
      * [DartSass: Sass Unwatch](#dartsass-sass-unwatch)
    * [Commands](#commands)
      * [QuikSass: Compile Current File](#quiksass-compile-current-file)
      * [QuikSass: Sass Compiler Version](#quiksass-sass-compiler-version)
      * [QuikSass: View Watcher List](#quiksass-view-watcher-list)
      * [QuikSass: Clear All Watchers](#quiksass-clear-all-watchers)
    * [Properties](#properties)
* [Features](#features)
    * [Pure Javascript SASS](#pure-javascript-sass)
    * [Customize Directory](#customize-directory)
* [FAQ](#faq)
* [License](#license)
* [ChangeLog](#changelog)
* [Todo](#todo)
* [Contributing](#contributing)
* [Credits](#credits)
* [Share](#share)


## Usage

<img src="https://github.com/malvahq/vscode-plugin-dartsass/raw/master/images/how_to_use_it.gif" width="600"/>

It uses the Dart/JS Sass Compiler to generate the .css and .min.css files automatically for the given .scss file in the editor.

## Install

### Inside VSCode

You can install it from inside VSCode by using the following command

`
ext install malvahq.dartsass
`

### Marketplace

You can install [malvahq.dartsass](https://marketplace.visualstudio.com/items?itemName=malvahq.dartsass) from the VSCode Marketplace.

**Like it , then feel free to share**
<a href="https://www.twitter.com/home?status=Just%20discovered%20this%20on%20the%20%23VSMarketplace%3A%20https%3A%2F%2Fmarketplace.visualstudio.com%2Fitems%3FitemName%3Dmalvahq.dartsass" aria-label="share extension on twitter" target="_blank">                                    <img alt="" src="https://cdn.vsassets.io/v/M162_20200107.6/_content/icon-social-twitter.png" class="social-link share-twitter-button">                            </a>

## Activation

The plugin gets activated when .scss files are opened.

By default, with every save of .scss file - the plugin uses the built-in Sass Compiler to compile the scss files

## Configuration

More details of the plugin can be found at [vscode-plugin-dartsass Page](https://malvahq.github.io/vscode-plugin-dartsass/).

### Menus

#### DartSass: Sass Watch

  In the file explorer on the left hand side, when we right-click on a directory, we get a menuitem `DartSass: Sass Watch` .
  This option appears only in the case of a directory and not in case of individual files.


  This command `watches` the directory using the option `sass --watch input:output` .

  ```
  Important: For this menu / feature to work, the sassBinPath
  property must point to an external sass binary.
  Otherwise it will indicate an error.
  ```

  After the directory is successfully watched, an entry is added to the statusbar on the lower right bottom - `Sass Watchers: 1` (or any number as appropriate).

  When the IDE is closed the subprocesses launched for watching get killed automatically.

  To view the list of watched processes / directories, use the command: `DartSass: View Sass Watchers` and then check the `Output` under `DartJS Sass`.

  It will list all the watched source directories and the pid (tested in unix) for those processes.

#### DartSass: Sass Unwatch

  In the file explorer on the left hand side, when we right-click on a directory, we get a menuitem `DartSass: Sass UnWatch` .
  This option appears only in the case of a directory and not in case of individual files.

  If a directory was watched before, this kills the process used to watch the directory.

  In case the directory was not watched before, a warning message appears indicating that no watcher exists for that directory.

### Commands

#### QuikSass: Compile Current File

Compiles the current scss file in the active editor to .css and .min.css file as appropriate.

#### QuikSass: Sass Compiler Version

Prints out the current sass compiler version being used.

#### QuikSass: View Watcher List

Views the list of watchers by this sass plugin

#### QuikSass: Clear All Watchers

Clears all existing sass watchers without trying to figure out all the existing watchers and unwatching them individually.
Useful in case we want to do a quick project watcher reset.

### Properties

This extension contributes the following properties:

  1. `dartsass.includePath`: Default: [ ]. Set of directories to be specified as includePath for sass compilation. <b>Important:</b> Currently we do not support spaces in `includePath` given the quirks associated with that. So ensure that you do not have spaces in the same.
  1. `dartsass.disableMinifiedFileGeneration`: Default: False. Flag to disable minified file generation. Minified files are generated by default.
  1. `dartsass.disableSourceMap`: Default: False. Flag to disable source maps file generation (*.map). Source Maps are generated by default though.
  1. `dartsass.disableCompileOnSave`: Default: False. This disables a compilation with every save.
  1. `dartsass.pauseInterval`: Default: 10. Pause Interval (in seconds) before kicking off another scss compilation to not compile frequently and hog resources.
  1. `dartsass.enableStartWithUnderscores`: Default: false. Enables compilation of files that start with underscores.
  1. `dartsass.disableAutoPrefixer`: Default: false. Disables postcss processing using autoprefixer library.
  1. `dartsass.autoPrefixBrowsersList`: Default: `["> 1%", "last 2 versions"]`. List of browsers to be specified for autoprefixer. See https://github.com/browserslist/browserslist#readme for more details.
  1. `dartsass.targetDirectory`: Default: Empty. The target directory to write the generated css files.

     This can be an absolute directory or a directory, relative to project root.
  1. `dartsass.targetMinifiedDirectory`: Default: Empty. The target directory to write the generated minified css files.

      This can be an absolute directory or a directory, relative to project root.

      If this property is empty, then the value defaults to `dartsass.targetDirectory` . If `dartsass.targetDirectory` is also empty, then this value defaults to the same directory as that of the source files.
   1. `dartsass.sassBinPath`: Default: Empty.

       Eg: `/usr/local/bin/sass` PATH of global sass compiler binary to compile sass / scss files.

       (If not available globally sass compiler can be installed globally as `npm install -g sass@1.25.0`.

        To determine the path of global sass , do `which sass` on Linux / other posix based systems ).

       This can also can be a relative path to the root of the current project, after installing it locally (say, `npm install sass@1.25.0`)

       After installation, you can set the property to , say

       `node_modules/.bin/sass` ( Linux ) - or

       `node_modules/.bin/sass.cmd` ( Windows ), as appropriate

       By default, the property is empty and in that case, the plugin uses the `sass` npm package built along with this plugin.
   1. <strike> `dartsass.watchDirectories`: Default: `[]` - Empty Array of strings.

      When vsce restarts, the `watchDirectories` are watched again by the native sass compiler. The sass cmd-line processes are respawned again automatically so there is no need to watch the directories again.

      There is no need to set this property manually in the workspace. When the user selects "DartSass: Watch Directory" ( or "DartSass: Unwatch Directory" ) from the context menu of a directory this property is automatically modified to reflect the list of directories being watched.

      So for all practical purposes, this property is used as a pseudo-persistent store across vsce sessions by the plugin itself and the user need not bother to modify it directly. </strike>.

      `dartsass.watchDirectories` option has been removed entirely from the plugin as it is confusing to the user , given that the user is not supposed to manipulate them manually.

      If you were using this option earlier - you should delete them manually from .vscode/settings.json and "rewatch" the directories again ( using "DartSass: Watch Directory" menuitem that appears ).

      The functionality of persistent sass watchers is still available, so this is a 1-time change for the user as part of migration. See [Issue #21](https://github.com/malvahq/vscode-plugin-dartsass/issues/21) for more details.

      Configuration property deprecated / updated since 0.4.1+ .

   1. `dartsass.debug`: Default: false. Best applicable for developers of this extension only.

## Features

### Pure Javascript SASS

This VSCode plugin directly depends on the native pure-javascript `sass` implementation.

Check [Dart implementation of SASS](https://sass-lang.com/dart-sass) for more details.

It does not depend on `node-sass` (or indirectly the platform-specific `libcss` either !).

### Customize Directory

By default, it looks for packages in `package.json` in the root directory of the current project. ( and hence, the packages in `node_modules`)

To customize the same, check `dartsass.sassWorkingDirectory`. More details below in extension settings.

## FAQ

 1. **Does this plugin come pre-built with Sass Compiler ?**

    Yes. by default - the plugin comes pre-built with one of the more recent releases of sass compiler. So - you would not need to install sass compiler locally in your system for the plugin to be active.

 1. **I already have Sass compiler installed in my system in PATH or would like to try a sass compiler installed in a specific path ? How can I configure the same ?**

    By default - the plugin uses the built-in sass compiler used internally. To use an external binary, see option `sassBinPath` mentioned above. Point `sassBinPath` to the binary (say, `/usr/local/bin/sass` ) in User / Workspace for vscode and then start saving the files. Now the plugin will use the external sass binary as opposed to the built-in sass library for the compilation.

 1. **I don't have a global sass installation / I don't have the write permission to write to the global files / I don't want to have a single global sass binary. What are my options to set `sassBinPath` now ?**

    In your project `package.json` , under `devDependencies`, add an entry for `sass` (version 1.19.0 - say)

    `
    "devDependencies": {
        "sass" : "1.19.0"
    }
    `

    Install the packages as `npm i --no-optional`

    Modify the property `dartsass:sassBinPath: "node_modules/.bin/sass"` at the workspace level ( and *not at the user level*). This can also be done through "File -> Settings -> search for "DartSass" under workspace tab".

    This should help install a local sass binary in your project under your project tree, and can be used for `watching` Sass directories, if you don't have a global sass installation.

1. Can I use `node-sass` package in place of `sass` in step 3) above ?**

    The plugin has been written for `sass` package only and does not support `node-sass`. Not to mention , `node-sass` is platform dependent and deprecated as well. Hence we do not support the same.


1. **I have scss files that contain import statements that begin with "~" and used to work fine , until I had upgraded the plugin to v0.1.0+ ? What gives  ?**

    So earlier, we used to support the "~" prefix in import statements by using an importer called `node-sass-package-importer` . Hence it used to work.

    Starting from v0.1.0 though, support for `node-sass-package-importer` has been removed since then. So now your import statement becomes as follows.

    Earlier - `@import "~/bootstrap/scss/functions.scss"`

    would now be rewritten without the prefix "~/" as below:

    `@import "bootstrap/scss/functions.scss"`

    Also - you would want to set the `includePath` property (list of strings) as below:

    `"dartsass.includePath": ["node_modules"]`

    assuming the node_modules is in the root of the project under discussion. Else modify the above property accordingly.

    Changing the import statements and adding to `includePath` property should fix any changes broken by the upgrade.

    It is also better because eventually when the css files get packed /minified for distribution, they can be passed the conventional parameter `sass -I includeDir ..` to be compiled so avoiding any non-standard prefixes like **~** in the files helps that case.

 1. **The autocompile (of sass) files that comes predefined with the plugin is too aggressive and is killing the CPU. What can I do ?**

    By default, the Dart/JS compiler gets activated with every save of the current editor file.
If that is too aggressive, see `pauseInterval` configuration option above ( in seconds ). It can be used to configure the pause interval between successive compilations to use resources less aggressively.


 1. **I would like to use Autoprefixer for my compilation. Does this plugin support the same ?**

    The plugin comes built-in with autoprefixer support. See `autoPrefixBrowsersList` option to configure the browserslist for which autoprefixer needs to generate code (using postcss).

 1.  **I would like to compile a directory of .scss files everytime the files in the directory are changed. How do we do that ?**

     The plugin has an option called "Watch Directory" that goes with the context menu associated with a directory in the file explorer panel.

     This option launches a separate sass watch command in the background to implement the same.

1. **When I launch a "Watch Directory" , I get an error saying - "Directory watcher is not supported.". What could be going wrong ?**

   The directory watch functionality depends on the sass command line binary (platform-specific). So you need to install sass binary separately and then specify the binary using `sassBinPath` plugin configuration property ( See above ).

1. **I have watched a directory. Now I would like to unwatch the same and kill external processes that are watching as well.**

    Right click on a directory that is being watched already. Click "DartSass: Unwatch directory". This will `unwatch` the directory and kill the sass watch external process, if any.

    If the directory was not being watched , a warning message will popup indicating that the directory was not being previously watched.

## License

This VSCode extension is released under [MIT license](LICENSE).

## ChangeLog

See [CHANGELOG](CHANGELOG.md) for more details.

## Todo


  1. The list of directory watchers need to be better visualized than the naive output in the console.


## Contributing

The code of this plugin is published under MIT License.

So if you are contributing to this plugin / extension, it is important that the source code is distributed under MIT license.

Almost all the heavy-lifing of this plugin (say, interacting with sass library or using sass command line) is done by the common library -
[DartSass Plugin Common](https://github.com/heronci/dartsass-plugin-common).

So if you are looking for a bug / feature, check the dartsass-plugin-comon repository for the code that does most of the heavy-lifting.

## Credits

  1. [ TOC Credit: [ekalinin/github-markdown-toc](https://github.com/ekalinin/github-markdown-toc) ]

## Share

**Like it , then feel free to share**
<a href="https://www.twitter.com/home?status=Just%20discovered%20this%20on%20the%20%23VSMarketplace%3A%20https%3A%2F%2Fmarketplace.visualstudio.com%2Fitems%3FitemName%3Dmalvahq.dartsass" aria-label="share extension on twitter" target="_blank">                                    <img alt="" src="https://cdn.vsassets.io/v/M162_20200107.6/_content/icon-social-twitter.png" class="social-link share-twitter-button">                            </a>

