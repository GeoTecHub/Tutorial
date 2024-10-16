# Configure the path in Router
``` javascript
import { Routes } from '@angular/router';
import { provideRouter, RouterModule } from '@angular/router';
import { StandaloneComponent } from './standalone-component/standalone-component.component';

const routes: Routes = [
  { path: 'standalone', component: StandaloneComponent },
  { path: '', redirectTo: '/standalone', pathMatch: 'full' },
  { path: '**', redirectTo: '/standalone' }
];

export const AppRoutingModule = RouterModule.forRoot(routes);

```


#  Update the Main Application Module

``` javascript
import { bootstrapApplication } from '@angular/platform-browser';
import { provideRouter } from '@angular/router';
import { AppComponent } from './app.component';
import { AppRoutingModule } from './app-routing.module';

bootstrapApplication(AppComponent, {
  providers: [
    provideRouter(AppRoutingModule)
  ]
});

```
#  Add Router Outlet in the Main Template
In order to display routed components, you need to add a <router-outlet> directive in your main application template (app.component.html):

``` html 

<div>
  <nav>
    <a routerLink="/standalone">Standalone Component</a>
  </nav>
  <router-outlet></router-outlet>
</div>
```

Note: 
1. Path for the Standalone Component
```typescript
Copy code
{ path: 'standalone', component: StandaloneComponent }

```
This route definition specifies that when the user navigates to /standalone, the StandaloneComponent should be displayed. This is the primary route to access the standalone component.

2. Redirect Root Path to Standalone Component
```typescript
Copy code
{ path: '', redirectTo: '/standalone', pathMatch: 'full' }
```
This route definition handles the root path (/). When the user navigates to the root of your application (i.e., http://localhost:4200/), they will be redirected to /standalone.

path: '': This matches the root path.
redirectTo: '/standalone': This specifies that the user should be redirected to /standalone.
pathMatch: 'full': This ensures that the entire URL path is matched before the redirect is applied. Without this, partial matches could cause unexpected redirects.

3. Wildcard Route for Unmatched Paths
```typescript
Copy code
{ path: '**', redirectTo: '/standalone' }
```
This route definition acts as a catch-all for any paths that do not match any of the other routes defined in your application. It helps in handling 404 errors or undefined routes by redirecting the user to a specific route, in this case, /standalone.

path: '**': This matches any URL that hasn't been matched by previous routes.
redirectTo: '/standalone': This redirects any unmatched paths to /standalone.

# Display one component output in another component

