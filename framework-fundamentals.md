# `angular.json`

The `angular.json` file is the main configuration file for Angular CLI projects, defining project structure, build settings, and configurations for development, testing, and production. Key sections include:

## Key Sections

1. **Projects**: Lists all projects (apps and libraries) in the workspace and their specific configurations, like build, test, and serve options.

2. **Architect Configurations**:
   - **Build Options** (`projects.<project-name>.architect.build`):
     - `outputPath`: Specifies the folder for built files.
     - `index`: Main HTML file (`src/index.html`).
     - `main`: Main TypeScript file (`src/main.ts`).
     - `tsConfig`: TypeScript configuration file (e.g., `tsconfig.app.json`).
     - `styles` and `scripts`: Defines global styles and scripts (e.g., `styles.css`, external libraries like Bootstrap).
   - **Serve Options**: Sets up how the app is served, including port and proxy settings.
   - **Test Options**: Configures testing with tools like Karma and Jasmine.
   - **Lint Options**: Sets up linting for code quality.

3. **File Replacement**: Allows file replacements for different environments (e.g., replacing `environment.ts` with `environment.prod.ts` in production).

4. **Assets**: Defines paths for static assets (images, fonts) that are copied to the `outputPath` during the build.

## Example

To add Bootstrap globally, include `"node_modules/bootstrap/dist/css/bootstrap.min.css"` in the `styles` array.

# `styles.css`

The `styles.css` (or `styles.scss`) file is the global stylesheet for the Angular app, affecting all components unless overridden.

## Key Uses

1. **Global Styles**: Apply styles that affect the entire application. Useful for defining global fonts, colors, spacing, or CSS variables shared across components.

2. **Third-Party CSS Imports**: You can import external stylesheets, such as Google Fonts or CSS frameworks, for consistent design across the app.

```css
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

body {
  font-family: 'Roboto', sans-serif;
}
```
3.	Application-wide Themes and Resets: Define themes, color schemes, or CSS resets to maintain style consistency across the app.
Example:

```css
:root {
  --primary-color: #007bff;
  --secondary-color: #6c757d;
  --background-color: #f8f9fa;
}

body {
  background-color: var(--background-color);
}

.btn-primary {
  background-color: var(--primary-color);
  color: white;
}
```
## Summary

- **`angular.json`**: Configures the Angular project, including build settings, global styles/scripts, asset management, and environment-specific file replacements.
- **`styles.css`**: The main global stylesheet, used to define application-wide styles like fonts, themes, and layout settings.

# `Build`
## Angular Build Options

| Build Option              | Purpose                                                                            | Command(s)                                                                                                       |
|---------------------------|------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------|
| **Angular CLI (`ng build`)** | Standard build commands for development and production builds.                    | `ng build`<br>`ng build --configuration production`                                                              |
| **Custom Configurations** | Define custom builds in `angular.json` for different environments (e.g., staging, QA). | `ng build --configuration <environment>`<br>e.g., `ng build --configuration staging`                            |
| **Angular Universal (SSR)** | Server-side rendering for improved SEO and faster initial load times.            | `ng add @nguniversal/express-engine`<br>`npm run build:ssr`<br>`npm run serve:ssr`                               |
| **ng-packagr**            | Builds Angular libraries for reusability and distribution (not applications).      | `ng generate library <library-name>`<br>`ng build <library-name>`                                                |
| **Pre-rendering**         | Generates static HTML files, beneficial for SEO and performance.                   | `ng run <project-name>:prerender`<br>or `npm run prerender` (after setting up SSR)                              |
| **Dockerized Build**      | Creates a Docker image to run the Angular app in a containerized environment.      | `docker build -t angular-app .`<br>`docker run -p 80:80 angular-app`                                             |
| **Firebase Hosting**      | Build and deploy directly to Firebase Hosting, utilizing a CDN with SSL.           | `npm install -g firebase-tools`<br>`firebase login`<br>`firebase init`<br>`firebase deploy`                      |
| **Azure App Service**     | Build and deploy the Angular app to Azure’s cloud platform, utilizing Azure’s global network for scalability and availability. | `npm install -g azure-cli`<br>`az login`<br>`ng build --configuration production`<br>`az webapp up --name <app-name> --resource-group <resource-group> --location <location>` |


### Configuration-Specific Builds in `angular.json`

The `angular.json` file defines multiple build configurations, allowing you to customize builds for different environments, such as development, production, or staging. You can specify configurations directly or create custom configurations.

### Example of Custom Configuration in `angular.json`

```json
"configurations": {
  "production": {
    "fileReplacements": [
      {
        "replace": "src/environments/environment.ts",
        "with": "src/environments/environment.prod.ts"
      }
    ],
    "optimization": true,
    "outputHashing": "all",
    "sourceMap": false,
    "extractCss": true,
    "namedChunks": false,
    "aot": true,
    "extractLicenses": true,
    "vendorChunk": false,
    "buildOptimizer": true
  },
  "staging": {
    "fileReplacements": [
      {
        "replace": "src/environments/environment.ts",
        "with": "src/environments/environment.staging.ts"
      }
    ],
    "optimization": true,
    "sourceMap": true,
    "namedChunks": true,
    "aot": true
  }
}
```
### Ahead-of-Time (AOT) Compilation

AOT Compilation is a process that compiles Angular templates during the build time, rather than at runtime. With AOT, the compiler converts the Angular HTML templates and TypeScript code into JavaScript code before the browser loads. This provides several performance benefits:

- **Faster Rendering**: Since the compilation is done before the app is delivered, the browser doesn’t have to wait for the Angular compiler at runtime.
- **Smaller Application Size**: AOT compilation removes unnecessary parts of Angular code, reducing the overall bundle size.
- **Early Detection of Errors**: Errors in templates are caught at build time, improving code reliability.

### Example: Enabling AOT Compilation

In Angular CLI, AOT compilation is enabled by default for production builds. You can enable it manually using the `--aot` flag:

```bash
ng build --aot
```
To build the Angular project with Ahead-of-Time (AOT) compilation for production, use the following command:

```bash
ng build --configuration production --aot
```

# Summary of Approaches to Optimize Angular Applications

| Approach                          | Benefit                                                                                       |
|-----------------------------------|-----------------------------------------------------------------------------------------------|
| **AOT Compilation**               | Reduces bundle size, speeds up initial load, and catches errors early.                         |
| **Server-Side Rendering (SSR)**   | Improves SEO, speeds up initial load, and enhances performance on low-powered devices.         |
| **Pre-rendering**                 | Serves static HTML for fast loading and scalability, especially for non-dynamic content.       |
| **Lazy Loading Modules**          | Loads only necessary code, reducing initial load size.                                         |
| **Tree Shaking**                  | Removes unused code, optimizing bundle size.                                                   |
| **Code Splitting**                | Breaks app into smaller chunks, improving load times.                                          |
| **Minification and Compression**  | Reduces file sizes, speeding up download times.                                                |
| **Smaller Polyfills**             | Avoids unnecessary code for unsupported browser features.                                      |
| **HTTP/2 and CDN**                | Speeds up asset delivery through multiplexing and caching on edge servers.                     |
| **Web Workers**                   | Offloads heavy computations, improving app responsiveness.                                     |






