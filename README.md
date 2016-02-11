# Steps to init a jspm and TypeScript project

This readme file explains briefly how to setup a basic project with jspm and TypeScript. This is nor a seed nor a
full tutorial. Some commands may vary in the near future, as everything is still quite experimental.

__Sources:__
+ [jspm-cli getting started](https://github.com/jspm/jspm-cli/blob/master/docs/getting-started.md)
+ [TypeScript definitions](http://definitelytyped.org/tsd/)
+ [TypeScript configuration](https://github.com/Microsoft/TypeScript/wiki/tsconfig.json)
+ [ES6 imports syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import)

## Install jspm, tsc and tsd globally

If jspm, tsc or tsd are __not__ yet installed: 

```shell
$ npm install -g jspm tsc tsd
```

## Init the project with npm

This creates the `package.json` file. Fill it as you wish.

```shell
$ npm init
```

## Install jspm locally

It is advised to have a version of jspm locally. Install it!

```shell
$ npm install jspm --save-dev
```

## Configurate the project for jspm usage

Like npm, jspm has an `init` command.
Fill the answers as you wish, but the `config.js` default config file name is too common and can lead to conflicts.
Feel free to modify it as you want. 

```shell
$ jspm init
```

## Install your third-party packages

Many solutions. Some examples below. See the documentation for more.

```shell
$ jspm install npm:lodash-node
$ jspm install github:components/jquery
$ jspm install jquery
$ jspm install myname=npm:underscore
```
	
## For each third-party package, add the TypeScript definitions

They can be found [here](http://definitelytyped.org/tsd/).

```
tsd install lodash
```

## Configurate `tsconfig.json`

You want to compile your TypeScript into pure JS, don't you? This options (that you're free to change) are required or convenient.
 
```JSON
{
	"compilerOptions": {
		"target": "es5",
		"module": "system",
		"moduleResolution": "node",
		"sourceMap": true,
		"emitDecoratorMetadata": true,
		"experimentalDecorators": true,
		"removeComments": false,
		"noImplicitAny": false
	},
	"exclude": [
		"node_modules", "jspm_packages"
	]
}
```

## Configurate your HTML entry point

Add the jspm scripts, the polyfill is optional depending on your app browsers support.

```HTML
<script src="jspm_packages/system.js"></script>
<script src="jspm_packages/system-polyfill.js"></script>
<script src="jspmconfig.js"></script>
```

Then, in a `<script>` tag, link your main JS file.

```JavaScript
System.import('app/main').then(null, console.error.bind(console));
```

## You are now ready to write TypeScript files and link third party libraries

Don't forget to compile your TypeScript files into JS ones.

```shell
$ tsc -w -p .
```

A live reload server could be useful for development. Have a glance on [lite-server](https://github.com/johnpapa/lite-server)!

```shell
$ lite-server .
```

## Here you are!

Every command may of course be decorated with numerous options. Read man and help files! Have fun!
