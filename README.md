[![VSCode Marketplace Badge](https://img.shields.io/vscode-marketplace/v/malvahq.dartsass.svg?label=VSCode%20Marketplace&style=flat-square)](https://marketplace.visualstudio.com/items?itemName=malvahq.dartsass) [![Total Install](https://img.shields.io/vscode-marketplace/d/malvahq.dartsass.svg?style=flat-square)](https://marketplace.visualstudio.com/items?itemName=malvahq.dartsass) [![Avarage Rating Badge](https://img.shields.io/vscode-marketplace/r/malvahq.dartsass.svg?style=flat-square)](https://marketplace.visualstudio.com/items?itemName=malvahq.dartsass) [![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square)](https://github.com/malvahq/vscode-plugin-dartsass/)


Compiles .scss files using [Dart SASS Compiler](https://sass-lang.com/dart-sass) to css and minified css.

## Install

You can install it from inside VSCode by using the following command

`
ext install malvahq.dartsass
`


## Usage

The plugin gets activated when .scss files are opened and saved.

It uses the Dart/JS Sass Compiler to generate the .css and .min.css files automatically for the given .scss file in the editor.

By default, the Dart/JS compiler gets activated with every save of the current editor file.
If that is too aggressive, see `dartsass.pauseInterval` below.

## Menu

### DartSass: Sass Compiler Watch

  In the file explorer on the left hand side, when we right-click on a directory, we get a menuitem `DartSass: Sass Compiler Watch` .
  This option appears only in the case of a directory and not in case of individual files.


  This command `watches` the directory using the option `sass --watch input:output` .

  ```
  Important: For this menu to work, an external sass binary should be set for `sassBinPath` property. Otherwise it will indicate an error.
  ```

  After the directory is successfully watched, an entry is added to the statusbar on the lower right bottom - `Sass Watchers: 1` (or any number as appropriate).

  When the IDE is closed the subprocesses launched for watching get killed automatically.

  To view the list of watched processes / directories, use the command: `DartSass: View Sass Watchers` and then check the `Output` under `DartJS Sass`.

  It will list all the watched source directories and the pid (tested in unix) for those processes.

  ```
  TODO: 1) Right now, there is no way to kill / unwatch the directories from inside the IDE individually one at a time.

  Although all the processes eventually get killed when we close the IDE though.

  2) Also the list of watchers need to be better visualized than the naive output in the console.
  ```

## Commands

### QuikSass: Compile Current File

( Shortcut: <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>L</kbd> )

Compiles the current scss file in the active editor to .css and .min.css file as appropriate.

### QuikSass: Sass Compiler Version

( Shortcut: <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>Q</kbd> )

Prints out the current sass compiler version being used.

### QuikSass: Which Sass PATH

( Shortcut: <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>P</kbd> )

Prints out the PATH to the sass compiler being used.


## Properties

This extension contributes the following properties:

* `dartsass.includePath`: Default: [ ]. Set of directories to be specified as includePath for sass compilation.
* `dartsass.sassWorkingDirectory`: Default: Project Root. The working directory from which to run the sass compiler to be used by `node-sass-package-importer`.

  This can be an absolute directory or a directory, relative to project root.
* `dartsass.disableMinifiedFileGeneration`: Default: False. Flag to disable minified file generation. Minified files are generated by default.
* `dartsass.disableCompileOnSave`: Default: False. This disables a compilation with every save.
* `dartsass.pauseInterval`: Default: 10. Pause Interval (in seconds) before kicking off another scss compilation to not compile frequently and hog resources.
* `dartsass.enableStartWithUnderscores`: Default: false. Enables compilation of files that start with underscores.
* `dartsass.disableAutoPrefixer`: Default: false. Disables postcss processing using autoprefixer library.
* `dartsass.autoPrefixBrowsersList`: Default: ["last 2 version"]. List of browsers to be specified for autoprefixer. See https://github.com/browserslist/browserslist#readme for more details.
* `dartsass.targetDirectory`: Default: Empty. The target directory to write the generated css files.

  This can be an absolute directory or a directory, relative to project root.
* `dartsass.targetMinifiedDirectory`: Default: Empty. The target directory to write the generated minified css files.

  This can be an absolute directory or a directory, relative to project root.

  If this property is empty, then the value defaults to `dartsass.targetDirectory` . If `dartsass.targetDirectory` is also empty, then this value defaults to the same directory as that of the source files.
* `dartsass.debug`: Default: false. Best applicable for developers of this extension only.
* `dartsass.sassBinPath`: Default: Empty.

  Eg: `/usr/local/bin/sass` PATH of sass binary to be used to compile. [ `Beta` yet. ]

  By default, the property is empty and in that case, the plugin uses the `sass` npm package built along with this plugin.

## Features

### Pure Javascript SASS

This VSCode plugin directly depends on the native pure-javascript `sass` implementation.

Check [Dart implementation of SASS](https://sass-lang.com/dart-sass) for more details.

It does not depend on `node-sass` (or indirectly the platform-specific `libcss` either !).

### Smart Imports

It automatically imports [node-sass-package-importer](https://github.com/maoberlehner/node-sass-magic-importer/tree/master/packages/node-sass-package-importer) as well.


So it is possible to use the following the import notation in the scss files.


Eg:

Assume, we define a dependency in package.json as below (say, sass-mq).

`package.json`
```json
"dependencies": {
    "sass-mq": "~5.2.1",
}
```

We should pull the npm modules in the `node_modules` directory as below.

```
$ npm i
```
The above command will pull the node modules from npm to `node_modules` directory at the same level as package.json.

Then, we can import the package, `sass-mq` in our scss file using a shorthand notation starting with `~` as below.

`app.scss`
```scss
@import '~sass-mq/mq';
```

The plugin will include the modules defined in `package.json` (and hence, the generated modules present in the `node_modules` directory) when transpiling the .scss files inline.

#### Customize Directory

By default, it looks for packages in `package.json` in the root directory of the current project. ( and hence, the packages in `node_modules`)

To customize the same, check `dartsass.sassWorkingDirectory`. More details below in extension settings.

## Install

You can install [malvahq.dartsass](https://marketplace.visualstudio.com/items?itemName=malvahq.dartsass) from the VSCode Marketplace as appropriate.

## License

This VSCode extension is released under [MIT license](LICENSE).



## Requirements



## Release Notes

See [CHANGELOG](CHANGELOG.md) for more details.
