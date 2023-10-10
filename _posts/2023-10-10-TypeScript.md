---
title: Docker and Kubernetes
date: 2023-10-10 21:31:00 +/-0530
categories: [Development, Frontend]
tags: [ts, notes]     # TAG names should always be lowercase
math: true
---

### The Basics  
To install the typescript compiler globally `npm install -g typescript`  

**Emitting with Errors**, even <mark>tsc</mark> reports errors it still emits js files to stop it run `tsc --noEmitOnError hello.ts`

**Erased Types**, after processing ts files with tsc, type annotations are erased, it can also downlevel the js code to  ES3  version by default. we can set the target using this command `tsc --target es2015 hello.ts`

### Strictness
**noImplicitAny** Turning on the noImplicitAny flag will issue an error on any variables whose type is implicitly inferred as any.  

**strictNullChecks** By default, values like null and undefined are assignable to any other type  
