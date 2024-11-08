# Lazy Loading in Angular

**Lazy Loading** loads a module only when it’s needed (i.e., when a specific route is accessed). This can significantly reduce the initial load time, as only essential modules are loaded upfront. Lazy loading is typically used for **feature modules** that are not critical for the initial application load.

## Benefits of Lazy Loading

- **Faster Initial Load**: Reduces the amount of code loaded at startup, improving the application’s initial load time.
- **Efficient Resource Usage**: Loads modules only when required, reducing memory usage.
- **Improves Scalability**: Helps optimize performance, especially in large, complex applications.

## How to Implement Lazy Loading

To set up lazy loading for a feature module, use Angular's `loadChildren` property in the routing configuration:

### Example

```typescript
const routes: Routes = [
  {
    path: 'feature',
    loadChildren: () => import('./feature/feature.module').then(m => m.FeatureModule)
  }
];
```
#### With lazy loading, the FeatureModule is only loaded when the user navigates to the /feature route.

# Preloading in Angular

**Preloading** is a strategy where Angular loads certain modules in the background after the initial application load. This approach aims to improve performance by preloading modules that users are likely to navigate to, without blocking the initial app load. It balances the benefits of lazy loading with faster subsequent navigation.

## Types of Preloading Strategies

Angular provides built-in preloading strategies that can be configured to control how modules are preloaded:

1. **No Preloading (Default)**: 
   - Modules are only loaded on demand, with no preloading.
  
2. **PreloadAllModules**: 
   - Preloads all lazy-loaded modules after the initial load.
   - Useful for applications where subsequent navigation should be as fast as possible.
  
3. **Custom Preloading Strategy**: 
   - Allows you to selectively preload modules based on custom logic (e.g., user roles, network speed, or specific routes).

## Implementing PreloadAllModules Strategy

To use the `PreloadAllModules` strategy, update your `AppRoutingModule` as follows:

```typescript
import { RouterModule, Routes, PreloadAllModules } from '@angular/router';

const routes: Routes = [
  {
    path: 'feature',
    loadChildren: () => import('./feature/feature.module').then(m => m.FeatureModule)
  },
  {
    path: 'another-feature',
    loadChildren: () => import('./another-feature/another-feature.module').then(m => m.AnotherFeatureModule)
  }
];

@NgModule({
  imports: [RouterModule.forRoot(routes, { preloadingStrategy: PreloadAllModules })],
  exports: [RouterModule]
})
export class AppRoutingModule {}
```

## Custom Preloading Strategy in Angular

A **Custom Preloading Strategy** allows you to control which modules to preload based on specific conditions or logic. For example, you could preload certain modules based on **user roles**, **network connection type**, or **application state**.

## Benefits of Using a Custom Preloading Strategy

- **Optimized Loading**: Load only the necessary modules based on user context, reducing unnecessary data usage.
- **Better User Experience**: Preload modules based on conditions like network speed, ensuring a smoother experience for users on slower connections.
- **Selective Preloading**: Ideal for optimizing performance in large applications by selectively preloading critical modules.

## Example: Implementing a Custom Preloading Strategy

### Step 1: Create a Custom Preloading Strategy

#### Create a new file `custom-preloading.strategy.ts`

```typescript
import { Injectable } from '@angular/core';
import { Route, PreloadingStrategy } from '@angular/router';
import { Observable, of } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class CustomPreloadingStrategy implements PreloadingStrategy {
  preload(route: Route, load: () => Observable<any>): Observable<any> {
    // Preload only if the route has 'data.preload' set to true
    return route.data && route.data['preload'] ? load() : of(null);
  }
}
```
#### Mark Routes for Preloading
```typescript
const routes: Routes = [
  {
    path: 'feature',
    loadChildren: () => import('./feature/feature.module').then(m => m.FeatureModule),
    data: { preload: true } // Preload this module
  },
  {
    path: 'another-feature',
    loadChildren: () => import('./another-feature/another-feature.module').then(m => m.AnotherFeatureModule),
    data: { preload: false } // Do not preload this module
  }
];
```
#### Configure the Custom Strategy in the Router

```typescript
@NgModule({
  imports: [RouterModule.forRoot(routes, { preloadingStrategy: CustomPreloadingStrategy })],
  exports: [RouterModule]
})
export class AppRoutingModule {}
```
### Angular Loading Strategies

| Strategy              | Description                                                            | Use Case                                                                                   |
|-----------------------|-----------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| **Eager Loading**     | Loads modules upfront, typically at startup.                          | Small apps or critical modules that need to be available immediately.                      |
| **Lazy Loading**      | Loads modules only when the associated route is accessed.             | Non-critical feature modules that are not needed immediately.                              |
| **PreloadAllModules** | Preloads all lazy-loaded modules in the background after the initial load. | Medium to large apps where most feature modules are likely to be used, balancing lazy and eager. |
| **Custom Preloading** | Custom strategy to preload modules based on specific conditions (e.g., user role, network speed). | Apps with complex requirements for preloading, selective preload based on user roles or routes. |





