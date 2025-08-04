---
title: A summary on DI in NestJS
source: https://gemini.google.com/app/013561c0d4917302
author: []
published: 
created: 2025-08-04
description: 
tags:
  - clippings
---
## The Core Idea: Modules and Providers 🧩

NestJS organizes your application into **Modules**. Think of each module as a self-contained "toolbox." The tools inside this box are your **Providers**.

- **Providers (`@Injectable()`):** A provider is any class marked with the `@Injectable()` decorator. This includes services, repositories, validators, etc. It's a class that NestJS will manage (create an instance of) and can inject as a dependency into other classes.
- **Injection:** The act of "giving" a class an instance of a provider it needs. This happens automatically through the class `constructor`.

---
## The `@Module` Decorator: A Quick Reference

The `@Module()` decorator tells NestJS how a toolbox is organized. Each array inside it has a specific purpose.
- **`providers: [ ]`**
	- **WHAT GOES IN:** Your injectable classes (`ErrorService`, `SimilarProductValidator`).
	- **PURPOSE:** Registers the class with the module's internal container. This makes the provider available for injection into any other class *within this same module*.
- **`controllers: [ ]`**
	- **WHAT GOES IN:** Your controller classes (`SimilarProductsController`).
	- **PURPOSE:** Maps incoming HTTP requests to methods. Controllers are the primary *consumers* of providers.
- **`imports: [ ]`**
	- **WHAT GOES IN:** **Other modules only** (`ErrorsModule`, `WarningsModule`).
	- **PURPOSE:** To gain access to the *exported* providers from another module.
	- **RULE:** **NEVER** put a provider/service directly in this array.
- **`exports: [ ]`**
	- **WHAT GOES IN:** Providers from the current module's `providers` array (`ErrorService`).
	- **PURPOSE:** To make a provider "public" so other modules that import this module can use it. By default, providers are private to their own module.

---
## The Cross-Module Workflow

To use a service from one module (e.g., `ErrorService` from `ErrorsModule`) in another (`SimilarProductsModule`), you must:
1. **In the Source Module (`ErrorsModule`):**
	- List `ErrorService` in the `providers` array.
	- List `ErrorService` in the `exports` array to make it public.
2. **In the Consuming Module (`SimilarProductsModule`):**
	- Add `ErrorsModule` to the `imports` array.
3. **In the Consuming Class (`SimilarProductsController`):**
	- Use a regular `import { ErrorService } ...` (not `import type`).
	- Inject it into the `constructor`.