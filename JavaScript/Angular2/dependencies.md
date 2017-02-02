## Defining Dependencies
To define Angular 2 dependencies create a package.json file:
```json
{
    "name": "angular2-skeleton",
    "version": "1.0.0",
    "description": "Vlad's Demo App",
    "scripts": {
        "start": "tsc && concurrently \"tsc -w\" \"lite-server\" ",
        "lite": "lite-server",
        "tsc": "tsc",
        "tsc:w": "tsc -w"
    },
    "license": "UNLICENSED",
    "repository":dencies
        "type": "git",
        "url": ""
    },
    "dependencies": {
        "@angular/common": "2.1.2",
        "@angular/compiler": "2.1.2",
        "@angular/core": "2.1.2",
        "@angular/forms": "2.1.2",
        "@angular/http": "2.1.2",
        "@angular/platform-browser": "2.1.2",
        "@angular/platform-browser-dynamic": "2.1.2",
        "@angular/router": "3.1.2",  
        "angular-in-memory-web-api": "0.1.13",
        "bootstrap": "4.0.0-alpha.5",
        "core-js": "2.4.1",
        "reflect-metadata": "0.1.8",
        "rxjs": "5.0.0-beta.12",
        "systemjs": "0.19.40",
        "zone.js": "0.6.26"                    
    },
    "devDependencies": {
        "@types/core-js": "0.9.34",
        "@types/node": "6.0.46",
        "concurrently": "3.1.0",
        "lite-server": "2.2.2",
        "typescript": "2.0.6"
    }
}
```
Dependencies are npm (Node Package Manager) packages that were created by other developers. 
- name - name of the application
- version - version of the application
- description - simple description of your application
- scripts (an object itself) - npm scripts for tsc (TypeScript compiler) to compile and run the application
- license - type of license of the application
- repository (an object itself) - what type of repositoy it is
- dependencies (an object itself) - declaration of all modules
- devDependencies (an object itself) - declaration only development modules
 
