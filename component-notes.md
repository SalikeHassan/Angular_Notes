# Angular Component

An Angular component is a fundamental building block in Angular, defining a specific view of the application.

## Key Elements of an Angular Component

- **Template**: An HTML fragment representing the UI, defining what is rendered. It uses Angular bindings and directives to make the view dynamic.
- **Class**: Written in TypeScript, this holds the data (properties) and functions (methods) that support the view’s logic.
  - **Example**: Define a title as a class property to display it in the view. Create methods for actions like showing/hiding an image.
- **Metadata**: Provides additional details about the component, marking it as an Angular component through a decorator.
- **Decorator**: A function adding metadata to classes, members, or arguments, making the class an Angular component.

## Component Breakdown

1. **Imports**: Required Angular members.
2. **Component Decorator**: Contains metadata, such as the component’s template and selector.
3. **Class**: Defines properties (data) and methods (functions) required by the view.

## Code Example

Here’s a simple Angular component in TypeScript:

```typescript
// Import necessary Angular core members
import { Component } from '@angular/core';

// Component decorator defining metadata
@Component({
  selector: 'app-sample', // Defines how to use the component in HTML: <app-sample></app-sample>
  template: `
    <h1>{{ title }}</h1>
    <button (click)="toggleImage()">Toggle Image</button>
    <img *ngIf="showImage" src="path-to-image.jpg" alt="Sample Image">
  `
})
// Component class with properties and methods
export class SampleComponent {
  title: string = 'Welcome to Angular'; // Property for title in the view
  showImage: boolean = true; // Property to control image visibility

  // Method to toggle image visibility
  toggleImage() {
    this.showImage = !this.showImage;
  }
}
```

## Understanding Metadata in Angular

In Angular, **metadata** is information attached to a class that Angular uses to understand how that class should function within the application. This metadata tells Angular that a specific class is a component, directive, service, or other feature and defines how it interacts with the rest of the app. It is specified using **decorators**, which are special functions added to the class.

### Key Points about Metadata in Angular

- **Purpose**: Metadata provides Angular with essential details about a class, such as whether it’s a component and what it should do.
- **Decorator**: Metadata is applied using decorators like `@Component`, `@Directive`, or `@Injectable`, which are prefixed by `@` and placed above the class definition.
- **Common Metadata Properties in Components**:
  - **selector**: Specifies the HTML tag for the component, like `<app-root>`, so Angular knows where to render it.
  - **template or templateUrl**: Defines the HTML content or link to the HTML file that makes up the component’s view.
  - **styleUrls**: Links to CSS files to style the component’s view.
  - **providers**: Allows the component to have its own set of services, if specified.

### Example of Metadata in a Component

In a component, metadata defines properties like the HTML template and selector, informing Angular about how and where to use this component.

```typescript
import { Component } from '@angular/core';

// Metadata is defined within the @Component decorator
@Component({
  selector: 'app-hello-world', // The tag name to use this component in HTML
  template: `<h1>{{ greeting }}</h1>`, // Inline HTML template for the component
  styleUrls: ['./hello-world.component.css'] // External CSS file for styling
})
export class HelloWorldComponent {
  greeting: string = 'Hello, Angular!'; // Class property accessible in the template
}
```

