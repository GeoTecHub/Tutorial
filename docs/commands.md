# Commands used in freaquently 
1. Gnenerating a  components
```bash
ng g c components/home
```
2. Generating  a service
```bash
ng g s services/openlayers
```
# Comamads for the webGIS mapping
## setup new libraries

1. Turf.js library 
setup the library service
```bash
npm install --save-dev @types/turf //same for other libraries such as proj4
or 
```
2. Decalre the library service
reate a custom declaration file: 
Create **src/turf.d.ts** and add:

```typescript

declare module 'turf';
```

Update **tsconfig.json** if using the custom declaration file:
```json

{
  "compilerOptions": {
    ...
  },
  "include": [
    "src/**/*.ts",
    "src/turf.d.ts"
  ]
}
```
