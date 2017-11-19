## Sass Installation

When creatig a new project, add a Sass preprocessor to it. After installing necessary packages:
```
npm install
```
Install the sass loader because we are going to use the sass preprocessor to style our application:
```
npm install sass-loader node-sass --save-dev
```
If webpack is used, use this instead:
```
npm install sass-loader node-sass webpack --save-dev
```
Finally, we are ready to run it:
```
npm run dev
```
### Notes
In your .vue files `<style lang="sass">` uses the indented syntax, if you want the CSS-superset syntax, use `lang="scss"`.

[sass-loader](https://github.com/webpack-contrib/sass-loader)
