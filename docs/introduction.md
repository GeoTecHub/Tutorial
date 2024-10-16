# Introductnion to setup
## Setup issues
### Tips to resolved turf.js issues
#### Step 1: Update tsconfig.json  


Ensure the allowSyntheticDefaultImports flag is set to true in your tsconfig.json file: 
```
{
  
  "compileOnSave": false,  
  "compilerOptions": {  
    "forceConsistentCasingInFileNames": true,  
    "typeRoots": ["node_modules/@types"],  
    "types": ["node"],  
    "outDir": "./dist/out-tsc",  
    "strict": true,  
    "noImplicitOverride": true,  
    "noPropertyAccessFromIndexSignature": true,  
    "noImplicitReturns": true,  
    "noFallthroughCasesInSwitch": true,  
    "skipLibCheck": true,  
    "esModuleInterop": true,  
    "allowSyntheticDefaultImports": true,  
    "sourceMap": true,  
    "declaration": false,  
    "experimentalDecorators": true,  
    "moduleResolution": "bundler",  
    "importHelpers": true,  
    "target": "ES2022",  
    "module": "ES2022",  
    "useDefineForClassFields": false,  
    "lib": [  
      "ES2022",  
      "dom"  
    ]  
  },  
  "include": ["src/**/*.ts", "src/turf.d.ts"],  
  "angularCompilerOptions": {  
    "enableI18nLegacyMessageIdFormat": false,  
    "strictInjectionParameters": true,  
    "strictInputAccessModifiers": true,  
    "strictTemplates": true  
  }  
}  
```
#### Step 2: Create or Update turf.d.ts  
Create or update the src/turf.d.ts file with the following content to ensure that the module can be correctly imported:  
declare module 

```
'@turf/turf' {   
  const turf: typeof import('@turf/turf');  
  export default turf;  
}  
```
#### Step 3: Correct Import Syntax in Your Code
Ensure you import @turf/turf correctly in your TypeScript files. Use the default import syntax:S   
```
import turf from '@turf/turf';  
```
// Example usage  
const point = turf.point([0, 0]);  

#### Step 04: Check package.json Dependencies  
```
{<span style="color: blue;">
  "name": "info-bhoomi-pro",  
  "version": "0.0.0",   
  "scripts": {  
    "ng": "ng",  
    "start": "ng serve",  
    "build": "ng build",  
    "watch": "ng build --watch --configuration development",  
    "test": "ng test",  
    "serve:ssr:InfoBhoomiPro": "node dist/info-bhoomi-pro/server/server.mjs"  
  },  
  "private": true,  
  "dependencies": {  
    "@angular/animations": "^18.0.0",  
    "@angular/common": "^18.0.0",  
    "@angular/compiler": "^18.0.0",  
    "@angular/core": "^18.0.0",  
    "@angular/forms": "^18.0.0",  
    "@angular/platform-browser": "^18.0.0",  
    "@angular/platform-browser-dynamic": "^18.0.0",  
    "@angular/platform-server": "^18.0.0",  
    "@angular/router": "^18.0.0",  
    "@angular/ssr": "^18.0.1",  
    "express": "^4.18.2",  
    "rxjs": "~7.8.0",  
    "tslib": "^2.3.0",  
    "zone.js": "~0.14.3",  
    "proj4": "^2.10.0",  
    "@turf/turf": "^6.5.0",  
    "ol": "9.2.4"  
  },  
  "devDependencies": {  
    "@angular-devkit/build-angular": "^18.0.1",  
    "@angular/cli": "^18.0.1",  
    "@angular/compiler-cli": "^18.0.0",  
    "@types/express": "^4.17.17",  
    "@types/jasmine": "~5.1.0",  
    "@types/node": "^18.18.0",  
    "jasmine-core": "~5.1.0",  
    "@types/proj4": "^2.5.5",  
    "karma": "~6.4.0",  
    "karma-chrome-launcher": "~3.2.0",  
    "karma-coverage": "~2.2.0",  
    "karma-jasmine": "~5.1.0",  
    "karma-jasmine-html-reporter": "~2.1.0",  
    "typescript": "~5.4.2",  
    "vite": "^5.1.3"  
  }  
}  
```
