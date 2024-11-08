# Angular Application Bundling: Architecting for Performance

When deploying an Angular application to production, efficient bundling is crucial to ensure optimized performance and faster load times. Angular traditionally used **Webpack** as its primary build tool, but with the release of **Angular 18**, a new Vite-based builder using **esbuild** has been introduced.

## What is Bundling?

Bundling refers to the process of combining all your application’s assets (JavaScript, CSS, HTML) into optimized bundles that can be efficiently delivered to the browser. This is a key step in generating production builds.

## Traditional Bundling with Webpack

Previously, Angular applications relied on the **Angular DevKit builder** powered by Webpack for production builds. Webpack is a robust tool with extensive plugin support but can sometimes be slow, especially for large-scale applications.

### Limitations of Webpack

- **Slower build times**: As applications grow, Webpack builds can become slower, impacting developer productivity.
- **Higher resource consumption**: Builds with Webpack can consume significant CPU and memory resources, especially in CI/CD environments.

## Introducing Vite and esbuild

### What is Vite?

- **Vite** is a modern frontend build tool that leverages **esbuild** for super-fast bundling.
- It’s designed to offer a faster, more efficient alternative to Webpack by using the latest advancements in JavaScript tooling.
- Vite includes server-side rendering (SSR) capabilities, which can be beneficial for SEO and performance in large-scale applications.

### What is esbuild?

- **Esbuild** is an extremely fast JavaScript bundler and minifier written in **Go**.
- It outperforms traditional bundlers by using parallel compilation, resulting in dramatically reduced build times.

### Performance Comparison

Esbuild demonstrates significantly faster build times than Webpack, especially in large projects:
- Esbuild can build **10 copies of a large library** like three.js in less than a second, while other bundlers might take several seconds.

## Transitioning to Vite in Angular 18

The demo application showcased in the course was converted from the traditional Angular DevKit Webpack builder to the new **Vite-based builder**. Here’s how you can do it in your own Angular projects.

### Steps to Switch to Vite

1. **Upgrade to Angular 18** to access the new Vite builder.
2. **Install the Vite builder** as a development dependency:

    ```bash
    npm install @angular/vite-builder --save-dev
    ```
### Update the angular.json configuration file to replace the old Webpack builder with the Vite builder.
## Example Configuration for Using Vite in `angular.json`

To switch your Angular project to use the Vite-based builder, update the `angular.json` file as shown below:

```json
"architect": {
  "build": {
    "builder": "@angular-devkit/vite-builder:build",
    "options": {
      "outputPath": "dist",
      "index": "src/index.html",
      "main": "src/main.ts",
      "polyfills": "src/polyfills.ts",
      "tsConfig": "tsconfig.app.json"
    }
  },
  "serve": {
    "builder": "@angular-devkit/vite-builder:serve",
    "options": {
      "proxyConfig": "src/proxy.conf.json"
    }
  }
}
```
## Running the Vite Build & Serve Commands

With Vite configured, you can now run the Angular build and serve commands:

### Build the Application

To create a production build using Vite:

```bash
ng build --configuration production
```
serve
```bash
ng serve
```
### Key Advantages of Using Vite and esbuild

| Feature                        | Benefit                                                                          |
|--------------------------------|----------------------------------------------------------------------------------|
| **Faster Build Times**         | Reduces wait times during development and CI/CD.                                  |
| **Modern ES Module Support**   | Enables better module interoperability.                                           |
| **Server-Side Rendering (SSR)**| Built-in SSR support for improved SEO and performance.                            |
| **Lower Resource Usage**       | Reduces CPU/memory consumption, saving cloud costs.                               |
| **Optimized for Large Projects**| Significant performance gains in enterprise-scale applications.                   |

