
# WebGIS Project Tutorial



Welcome to this tutorial on creating a WebGIS project. In this guide, you will learn how to set up, develop, and deploy a WebGIS application using Angular and OpenLayers.

## Table of Contents

1. [Introduction](#introduction)
2. [Getting Started]()
3. [Step 1: Setting Up the Development Environment](#step-1-setting-up-the-development-environment)
4. [Step 2: Creating the Angular Project](####_Step_2)
5. [Step 3: Integrating OpenLayers](#step-3-integrating-openlayers)
6. [Step 4: Adding Vector and Raster Editing Tools](#step-4-adding-vector-and-raster-editing-tools)
7. [Step 5: Deploying the WebGIS Application](#step-5-deploying-the-webgis-application)
8. [Conclusion](#conclusion)

# introduction 
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
#### Step 2 
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
# Setting the  environment for the WebGIS project
## Step 1:Set Up Angular Project

1. Install Angular CLI (if not already installed):  
```bash  
npm install -g @angular/cli
```
1. Create a new Angular project:  
```bash
ng new webgis-project
cd webgis-project
```
## Step 2: Install Openlayers and Turj.js
1. Install Openlayers
```bash
npm install ol
```
2. install Turf.js  
```bash
npm install @turf/turf

```
## Step 3: Add Openlayers and Turf.js to the project
1. Create a new component for the map:
```bash
ng generate component map

```
2. Modify the map.component.html to include a div for the map:  
```html
<div id="map" class="map"></div>
```
3. Add styles for the map in map.component.css:
```css
.map {
  width: 100%;
  height: 100vh;
}

```

4. Import OpenLayers and Turf.js in map.component.ts and initialize the map:

```typescript
import { Component, OnInit } from '@angular/core';
import Map from 'ol/Map';
import View from 'ol/View';
import TileLayer from 'ol/layer/Tile';
import OSM from 'ol/source/OSM';
import * as turf from '@turf/turf';

@Component({
  selector: 'app-map',
  templateUrl: './map.component.html',
  styleUrls: ['./map.component.css']
})
export class MapComponent implements OnInit {

  map!: Map;

  ngOnInit(): void {
    this.map = new Map({
      target: 'map',
      layers: [
        new TileLayer({
          source: new OSM()
        })
      ],
      view: new View({
        center: [0, 0],
        zoom: 2
      })
    });

    // Example of using Turf.js to create a random point
    const point = turf.randomPoint(1);
    console.log(point);
  }
}

```
## Step 4: Integrate the Map Component
1. Update app.component.html to include the map component:
```html
<app-map></app-map>

```
## Step 5: Run the Angular Application 
1. Start the Angular development server:

```bash
Copy code
ng serve
```
2. Open the browser and navigate to http://localhost:4200 to see the map.

Additional Tips:  
`*` Adding More Layers and Interactions: Explore OpenLayers documentation to add more functionalities like vector layers, overlays, interactions, etc.  

`*` Using Turf.js: Turf.js provides numerous spatial analysis functions like buffering, intersecting, and more. You can use these functions within your component to perform geospatial operations.   

## Example: Adding a Vector Layer with Turf.js  

1. Add vector layer and Turf.js feature in map.component.ts:
```typescript
Copy code
import VectorLayer from 'ol/layer/Vector';
import VectorSource from 'ol/source/Vector';
import GeoJSON from 'ol/format/GeoJSON';
import { Feature } from 'ol';
import { Point } from 'ol/geom';
import { Style, Fill, Stroke, Circle as CircleStyle } from 'ol/style';

ngOnInit(): void {
  // Initialize map as before

  // Create a random point using Turf.js
  const point = turf.randomPoint(1);
  const geojson = new GeoJSON().readFeatures(point, {
    featureProjection: 'EPSG:3857'
  });

  // Create vector source and layer
  const vectorSource = new VectorSource({
    features: geojson
  });

  const vectorLayer = new VectorLayer({
    source: vectorSource,
    style: new Style({
      image: new CircleStyle({
        radius: 5,
        fill: new Fill({ color: 'red' }),
        stroke: new Stroke({ color: 'black', width: 1 })
      })
    })
  });

  // Add the vector layer to the map
  this.map.addLayer(vectorLayer);
}
```


