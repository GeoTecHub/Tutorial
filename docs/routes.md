# Routing in Angular

## Key Concepts
1. Router: The Angular Router is a library that provides navigation and URL manipulation capabilities.

2. Routes: Routes define the mapping between URLs and components. Each route consists of a path and the component that should be displayed when the URL matches that path.

3. RouterModule: This module provides the necessary services and directives for navigating within the application. It includes directives like RouterOutlet and routerLink.

4. RouterOutlet: This directive acts as a placeholder in the template where the matched component's template will be displayed.

5. RouterLink: This directive is used to navigate to different routes in your application. 

## Steps to Set Up Routing in Angular
1. Define Routes: Create an array of route objects that define the mapping between URLs and components.

2. Import RouterModule: Import the RouterModule and configure it with the routes in your application's main module or a dedicated routing module.

3. Add RouterOutlet: Add the RouterOutlet directive in the main template where you want the routed components to be displayed.

4. Use RouterLink: Use the routerLink directive to create navigation links within your application.
###Example: Setting Up Routing
Let's walk through a simple example to set up routing in an Angular application.

Step 1: Define Routes  
Create a file called **app.routes.ts** to define your routes:

```typescript

import { Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';  // Adjust the path as needed
import { AboutComponent } from './about/about.component';  // Another example component

export const routes: Routes = [
  { path: '', redirectTo: '/home', pathMatch: 'full' },  // Redirect to home by default
  { path: 'home', component: HomeComponent },
  { path: 'about', component: AboutComponent }
];
```
Step 2: Import RouterModule  
If you are using standalone components, set up routing in your **main.ts** and **app.config.ts**. Here’s how you can do it:
**app.config.ts**
```typescript

import { ApplicationConfig, provideZoneChangeDetection } from '@angular/core';
import { provideRouter } from '@angular/router';
import { routes } from './app.routes';
import { provideClientHydration } from '@angular/platform-browser';

export const appConfig: ApplicationConfig = {
  providers: [
    provideZoneChangeDetection({ eventCoalescing: true }),
    provideRouter(routes),
    provideClientHydration()
  ]
};
```
**main.ts**
```typescript

import { bootstrapApplication } from '@angular/platform-browser';
import { appConfig } from './app/app.config';
import { AppComponent } from './app/app.component';

bootstrapApplication(AppComponent, appConfig)
  .catch((err) => console.error(err));
```
Step 3: Add RouterOutlet   
Add the RouterOutlet directive to your main component’s template:  
**app.component.html**
```html
<router-outlet></router-outlet>

```
Ensure your AppComponent is set up to use the RouterOutlet:

**app.component.ts**
```typescript
import { Component } from '@angular/core';
import { RouterOutlet } from '@angular/router';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [RouterOutlet],
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']  // Corrected 'styleUrl' to 'styleUrls'
})
export class AppComponent {
  title = 'webgis-project';
}
```
Step 4: Use RouterLink
Use the routerLink directive to create navigation links in your application. For example, in your app.component.html, you might add navigation links:  

**app.component.html**
```html

<nav>
  <a routerLink="/home">Home</a>
  <a routerLink="/about">About</a>
</nav>
<router-outlet></router-outlet>
```

## Example Components  
Ensure you have the components defined for your routes, such as HomeComponent and AboutComponent.  

home.component.ts  
```typescript

import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { RouterOutlet } from '@angular/router';

@Component({
  selector: 'app-home',
  standalone: true,
  imports: [CommonModule, RouterOutlet],
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent {
  title = 'Home Page';
}
```
about.component.ts
````typescript
import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';

@Component({
  selector: 'app-about',
  standalone: true,
  imports: [CommonModule],
  templateUrl: './about.component.html',
  styleUrls: ['./about.component.css']
})
export class AboutComponent {
  title = 'About Page';
}
```
####Conclusion  
By following these steps, you can set up routing in your Angular application. The RouterModule and its directives (RouterOutlet and routerLink) enable you to navigate between different components and views seamlessly. The provideRouter function is used to configure the routes and bootstrap the application with the correct routing configuration. This setup ensures that your application can handle navigation and URL changes effectively.