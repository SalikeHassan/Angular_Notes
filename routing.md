![image](https://github.com/user-attachments/assets/c2293862-cd5e-4b74-a553-8a7564f12863)
![image](https://github.com/user-attachments/assets/5847c4dc-be2a-43c9-baf3-7935a46b0343)
![image](https://github.com/user-attachments/assets/002ae71e-40fc-4d4b-8064-357e4dfcc520)
![image](https://github.com/user-attachments/assets/7dbd54a8-30f4-459d-9ddf-5fc33f41e9af)
![image](https://github.com/user-attachments/assets/b091b08d-2010-4d55-acf3-af9ab6f16c1c)
![image](https://github.com/user-attachments/assets/c166928c-05e5-41e0-9347-82c64b9e63dd)
![image](https://github.com/user-attachments/assets/f446a227-892f-48fe-bdad-a38ab20d44ea)
![image](https://github.com/user-attachments/assets/2d5b04e0-c72f-49da-8046-ec130ce75921)
![image](https://github.com/user-attachments/assets/4784cd58-ee19-418b-9b85-281760caf09f)
![image](https://github.com/user-attachments/assets/96f39629-2d94-4f70-8cb1-d7d443b2f85a)
![image](https://github.com/user-attachments/assets/34abd78f-2659-4801-86c5-6eee12ef909e)

## Configuration Options for provideRouter
# Configuration Options in Angular Router

| Configuration Option                    | Description                                                               | Usage Example                                      | Use Case                                                                                             |
|-----------------------------------------|---------------------------------------------------------------------------|----------------------------------------------------|------------------------------------------------------------------------------------------------------|
| **withComponentInputBinding()**         | Binds route parameters directly to component inputs.                      | `withComponentInputBinding()`                      | Useful when you want to simplify the way route parameters are passed to components.                  |
| **withPreloading()**                    | Enables lazy-loading of modules using preloading strategy.                | `withPreloading(PreloadAllModules)`                | Optimizes load time by preloading lazy-loaded modules after initial load.                            |
| **withDebugTracing()**                  | Enables detailed router event logging for debugging.                      | `withDebugTracing()`                               | Useful during development to debug route changes and router events in the console.                   |
| **withRouterConfig()**                  | Allows setting advanced router configurations.                            | `withRouterConfig({ onSameUrlNavigation: 'reload' })` | Configure router behavior such as reloading components when navigating to the same URL.           |
| **withEnabledBlockingInitialNavigation()** | Ensures initial navigation is completed before the app is rendered.       | `withEnabledBlockingInitialNavigation()`           | Useful when initial route data needs to be fully loaded before rendering the main application.       |
| **withHashLocation()**                  | Enables hash-based routing (/#/path).                                     | `withHashLocation()`                               | Useful for deploying apps on servers that don’t support deep linking.                                |
| **withInMemoryScrolling()**             | Enables in-memory scrolling behavior between navigations.                 | `withInMemoryScrolling({ anchorScrolling: 'enabled' })` | Useful for handling anchor link navigation smoothly.                                    |
| **withDisabledInitialNavigation()**     | Disables the initial navigation altogether.                               | `withDisabledInitialNavigation()`                  | Useful in scenarios where you want to delay navigation until after certain conditions are met.       |
| **withRouterLinkActiveOptions()**       | Configures RouterLinkActive directive globally.                           | `withRouterLinkActiveOptions({ exact: true })`     | Ensures active links are matched exactly to the current route.                                       |

![image](https://github.com/user-attachments/assets/9960e94f-e7d4-47b6-8f1d-65e755efc72f)
![image](https://github.com/user-attachments/assets/7682f497-f925-4260-84e3-edfafa203ce4)
![image](https://github.com/user-attachments/assets/fb9a0125-c0e2-4fe7-beed-2e584c9a3e85)
![image](https://github.com/user-attachments/assets/05f4dc6d-abfe-4f19-81d0-119b7e2ec954)
![image](https://github.com/user-attachments/assets/639bc5da-4bfe-4479-a4db-6636e4ab6a30)
