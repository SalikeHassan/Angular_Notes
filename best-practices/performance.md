# Angular Application Bundling: Architecting for Performance

## Ahead-of-Time (AOT) Compilation

AOT Compilation is a process that compiles Angular templates during build time, rather than at runtime. With AOT, the compiler converts Angular HTML templates and TypeScript code into JavaScript code before the browser loads. This provides several performance benefits:

### Benefits of AOT Compilation

- **Faster Rendering**: Since the compilation is done before the app is delivered, the browser doesn’t have to wait for the Angular compiler at runtime.
- **Smaller Application Size**: AOT compilation removes unnecessary parts of Angular code, reducing the overall bundle size.
- **Early Detection of Errors**: Errors in templates are caught at build time, improving code reliability.

### Example: Enabling AOT Compilation

In Angular CLI, AOT compilation is enabled by default for production builds. You can enable it manually using the `--aot` flag:

```bash
ng build --aot
```
### Alternatively, set it in angular.json under the production configuration:

```json
"configurations": {
  "production": {
    "aot": true
  }
}
```

## Server-Side Rendering (SSR) with Angular Universal

Server-Side Rendering (SSR) is a technique where Angular pre-renders the HTML of each page on the server before sending it to the client. This approach provides significant performance and SEO benefits:

### Benefits of SSR

- **Improved SEO**: Since search engines receive fully rendered HTML, SSR helps improve indexing for Angular applications.
- **Faster Initial Load**: The server provides fully rendered pages, so users can see content faster, especially over slower connections.
- **Better Performance for Low-powered Devices**: SSR offloads the initial rendering work to the server, making it easier for low-powered devices to load the app.

### Setting Up SSR with Angular Universal

To set up SSR in your Angular application, follow these steps:

### Step 1: Add Angular Universal to Your Project

```bash
ng add @nguniversal/express-engine
```
### Build and Serve the SSR Application
```bash
npm run build:ssr
```
```bash
npm run serve:ssr
```
#### The app will now serve rendered HTML content, improving the initial page load speed and supporting SEO.

## Pre-rendering with Angular Static Builds

Pre-rendering is a technique where Angular generates static HTML for specific routes during the build process. Unlike SSR, which renders pages on each request, pre-rendering creates static files that are served directly, resulting in extremely fast load times.

### Benefits of Pre-rendering

- **High Performance**: Since pre-rendered pages are served as static files, they load almost instantly.
- **SEO-friendly**: Just like SSR, search engines can index the static HTML.
- **Cost-effective and Scalable**: No server-side rendering is required, allowing pre-rendered sites to be hosted on CDNs, making them highly scalable and cost-efficient.

### Setting Up Pre-rendering with Angular

### Add Angular Universal to Your Project

To enable pre-rendering, you first need to set up Angular Universal:

```bash
ng add @nguniversal/express-engine
```
### Configure Routes to Pre-render: Edit angular.json to specify routes to pre-render
```json
"architect": {
  "prerender": {
    "builder": "@nguniversal/builders:prerender",
    "options": {
      "routes": [
        "/",
        "/about",
        "/contact"
      ]
    }
  }
}
```

### Run Pre-rendering
```bash
npm run prerender
```

## Build for Performance

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

# Summary of Approaches to Optimize Angular Applications

| Approach                         | Benefit                                                                                 |
|----------------------------------|-----------------------------------------------------------------------------------------|
| **AOT Compilation**              | Reduces bundle size, speeds up initial load, and catches errors early.                   |
| **Server-Side Rendering (SSR)**  | Improves SEO, speeds up initial load, and enhances performance on low-powered devices.   |
| **Pre-rendering**                | Serves static HTML for fast loading and scalability, especially for non-dynamic content. |
| **Lazy Loading Modules**         | Loads only necessary code, reducing initial load size.                                   |
| **Tree Shaking**                 | Removes unused code, optimizing bundle size.                                             |
| **Code Splitting**               | Breaks app into smaller chunks, improving load times.                                    |
| **Minification and Compression** | Reduces file sizes, speeding up download times.                                          |
| **Smaller Polyfills**            | Avoids unnecessary code for unsupported browser features.                                |
| **HTTP/2 and CDN**               | Speeds up asset delivery through multiplexing and caching on edge servers.               |
| **Web Workers**                  | Offloads heavy computations, improving app responsiveness.                               |
| **Vite**                         | Uses esbuild for faster bundling and modern ES module support, enhancing performance.    |


