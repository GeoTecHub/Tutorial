# Seeting the the environment for the WebGIS project
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


