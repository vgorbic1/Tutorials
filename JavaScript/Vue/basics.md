## Getting started

### Including directly in script
You can use Vue.js by just downloading it and including it within the <script> tag.

### CDN
If you don't want to bother downloading and managing Vue versions yourself, you can simply use the CDN version. 
```
<script src="https://unpkg.com/vue"></script>
```
### NPM
You can simply add an npm dependency to your package.json file. Just run npm install on your project's root:
```
npm install vue --save
```
### Vue-cli
First of all, you must install vue-cli:
```
npm install --global vue-cli
```
Now, you can start a fresh new project using the Vue command-line interface.
It is possible to setup a project using different templates—starting from a simple single HTML page project and going 
to a complex webpack project setup. The command that should be used for scaffolding a Vue project is as follows:
```
vue init <template> <project-name>
```
The following templates are available:
- webpack: This is a full-featured webpack setup with vue-loader. It supports hot reload, linting, testing, all kind of pre-processors, and so on.
- webpack-simple: This is a simple webpack setup that is useful for quick prototyping.
- browserify: This is a full-featured browserify setup with vueify that also supports hot reload, linting, and unit testing.
- browserify-simple: This is a simple browserify setup with vueify that can be used for quick prototyping.
- simple: This generates a simple HTML page that includes Vue.js. It is perfect for quick feature exploration.
