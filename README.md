# LiveScript Node.js Module Bootstrap

I like using [LiveScript](http://livescript.net/), so I decided to write this little bootstrap to make life simpler when it comes to writing Node.js modules with it.

## How to use it

Put all your LiveScript code to a directory called `src`. The default entry point for the application is `index.js`, so the source file for that should be called `index.ls`.

The makefile exists to compile your LiveScript code to JavaScript when the user installs your module via npm. Your code is compiled to the `lib` folder, so if for example you have the following source code structure:

```
src/index.ls
src/main/parser.ls
src/main/linter.ls
```

The files would be compiled to

```
lib/index.js
lib/main/parser.js
lib/main/linter.js
```

Due to this, you should make sure to not use file extensions when using `require` to load your submodules, so in your index.ls, you should have `require './main/parser'`, **not** `require './main/parser.ls'`.

## Important bits of package.json

Here are the important things that your package.json should have:

```json
  "dependencies": {
    "LiveScript": "~1.2.0",
    "shelljs": "~0.2.6"
  },
```

`LiveScript` and `shelljs` are used for the compilation.

```json
  "scripts": {
    "postinstall": "lsc make"
  },
```

This is responsible for running the compilation to JS on install.