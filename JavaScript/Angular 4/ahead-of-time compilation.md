## Ahead-of-Time Compilation

Engage Ahead-of-Time compilation. It will allow:
1. Faster Startup since Parsing and Compilation doesn't happen in Browser
2. Templates get checked during Development
3. Smaller File Size as unused Features can be stripped out and the Compiler itsef isn't shipped

![aot](https://github.com/vgorbic1/Tutorials/blob/master/JavaScript/Angular%204/images/aot.jpg)

To run a Build normally enter this in CLI:
```
ng build
```
Add `--prod` to Build the code for Production to minify and optimize the code

Add `--aot` to use Ahead-of-Time compilation. So it should look like:
```
ng build --prod --aot
```
