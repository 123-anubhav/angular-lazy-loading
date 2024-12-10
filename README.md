# angular-lazy-loading
angular-lazy-loading-interview-purspective

---

# 🚀 Angular Lazy Loading Example

Welcome to the **Angular Lazy Loading Example**! This repository demonstrates how lazy loading works in Angular using modules and routing to optimize performance by loading parts of the application only when required.

---

## 📜 **Table of Contents**

1. [Overview](#overview)  
2. [What is Lazy Loading?](#what-is-lazy-loading)  
3. [Why Use Lazy Loading?](#why-use-lazy-loading)  
4. [When and Where to Use Lazy Loading](#when-and-where-to-use-lazy-loading)  
5. [How to Implement Lazy Loading](#how-to-implement-lazy-loading)  
6. [Advantages of Lazy Loading](#advantages-of-lazy-loading)  
7. [Notes & Tips](#notes--tips)  
8. [Sample Code](#sample-code)

---

## 🖋️ **Overview**

Lazy loading in Angular allows you to split the application into feature modules and only load the modules when needed. This approach ensures that only necessary components and modules are loaded, speeding up application startup time.

---

## 💡 **What is Lazy Loading?**

Lazy loading is a design pattern in Angular where modules are loaded **only when the user navigates to a specific route**, instead of loading everything upfront. This reduces the initial payload for the application, improving performance and scalability.

---

## ✅ **Why Use Lazy Loading?**

Lazy loading is beneficial because:

- ⚡ **Faster Initial Load Time**: The app loads quickly without loading all features at startup.
- 💼 **Improved Scalability**: Only the necessary modules are loaded when a user interacts with specific parts of the app.
- 🛠️ **Efficient Code Splitting**: Keeps large chunks of code isolated to relevant use cases.
- 🌍 **Optimized Bandwidth**: Only relevant features are sent over the network.
- 🖥️ **Improved User Experience**: Users can begin interacting with the app sooner.

---

## 🕒 **When and Where to Use Lazy Loading**

Lazy Loading is ideal when:

- Your application has **feature-heavy pages** (e.g., products, customer details, dashboards, reports).
- You have routes that don’t need to be initialized upfront.
- You want to reduce the **bundle size** of the initial app load.

Typical scenarios to implement lazy loading:
- Features like **e-commerce catalogs** with a large number of products.
- Administrative dashboards or reporting pages.
- Modules with optional user actions that aren't always required.

---

## 🛠️ **How to Implement Lazy Loading**

Lazy loading is implemented by splitting modules and setting up routes with `loadChildren`. Here’s how it’s done:

---

### 1️⃣ **Define Routes in `app-routing.module.ts`**

Lazy loading is configured by setting up the `loadChildren` property with a module dynamically imported.

```typescript
import { Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';

export const routes: Routes = [
  { path: 'home', component: HomeComponent },
  { path: '', redirectTo: 'home', pathMatch: 'full' },
  { path: 'about', component: AboutComponent },
  {
    path: 'lazy',
    loadChildren: () => import('./loading-lazy/loading-lazy.module').then(m => m.LoadingLazyModule)
  }
];
```

---

### 2️⃣ **Define the Feature Module with Routes**

Use the `RouterModule.forChild()` to configure routes for lazy-loaded features.

**`loading-lazy.module.ts`**

```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { RouterModule, Routes } from '@angular/router';
import { ProductComponent } from '../product/product.component';
import { CustomerComponent } from '../customer/customer.component';

const routes: Routes = [
  { path: 'products', component: ProductComponent },
  { path: 'customers', component: CustomerComponent }
];

@NgModule({
  imports: [
    CommonModule,
    RouterModule.forChild(routes) 
  ],
  exports: [RouterModule]
})
export class LoadingLazyModule {
  constructor() {
    console.log('LoadingLazyModule constructor executed');
  }
}
```

---

### 3️⃣ **Set Up Components**

Define feature-specific components, e.g., `ProductComponent` & `CustomerComponent`.

#### **`product.component.ts`**

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-product',
  standalone: true,
  imports: [],
  templateUrl: './product.component.html',
  styleUrls: ['./product.component.css']
})
export class ProductComponent implements OnInit {
  ngOnInit() {
    console.log('ProductComponent initialized');
  }
}
```

---

#### **`customer.component.ts`**

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-customer',
  standalone: true,
  imports: [],
  templateUrl: './customer.component.html',
  styleUrls: ['./customer.component.css']
})
export class CustomerComponent implements OnInit {
  ngOnInit() {
    console.log('CustomerComponent initialized');
  }
}
```

---

### 4️⃣ **Add Router Links to Navigation**

Use `routerLink` with lazy-loaded routes.

```html
<div class="container">
  <h3 class="text-danger">Angular Lazy Loading Examples</h3>
  <nav class="navbar navbar-light bg-light">
    <a class="navbar-brand" routerLink="/home" routerLinkActive="active">Home</a>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <a class="navbar-brand" routerLink="/lazy/products" routerLinkActive="active">Products</a>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <a class="navbar-brand" routerLink="/lazy/customers" routerLinkActive="active">Customers</a>
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
    <a class="navbar-brand" routerLink="/about" routerLinkActive="active">About</a>     
  </nav>    
</div>
<router-outlet />
```

---

## 📈 **Advantages of Lazy Loading**

1. ⚡ **Fast Startup Time**: Only loads modules when needed.
2. 🔄 **Modular Codebase**: Code becomes modular and maintainable.
3. 📊 **Reduced Memory Consumption**: Non-used features are not loaded into memory until they are required.
4. 🌎 **Improved Network Performance**: Users only download what they need.
5. 💻 **Scalable Features**: Perfect for growing apps with many distinct features.

---

## 📝 **Notes & Tips**

<div style="color: red;">
  <h2>🚀 Use <b>Incognito Mode</b> or press <b>CTRL+F5</b> to clear cache and refresh your app.</h2>
</div>

Sometimes changes may not take effect due to caching. Always perform a hard refresh to ensure lazy loading changes are visible.

---

## 🎉 **Final Words**

Lazy loading in Angular optimizes performance, ensures scalability, and leads to a better user experience. Use it thoughtfully for routes or modules that aren't always needed upfront.

---

Happy Coding! 🚀
