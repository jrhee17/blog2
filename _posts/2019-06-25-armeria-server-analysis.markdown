---
layout: post
title: 'Armeria Server Analysis'
date: '2019-06-25'
categories: armeria
---

ServerBuilder: Create a `ServerConfig` which contains various server related configurations,
 and a `VirtualHost` which contains a list of `ServiceConfig`. 

AnnotatedHttpServiceFactory: Converts `Method` objects to `AnnotatedHttpServiceElement` objects. 

VirtualHostBuilder
- Contains a list of `ServiceConfigBuilder`, each of which contains a `service` and a `route`.
Each of these `ServiceConfigBuilder` later is set additional values such as `requestTimeoutMillis`, `maxRequestLength`, etc. and
is built to a `ServiceConfig` when the enclosing `VirtualHostBuilder` is built.
- `VirtualHostBuilder.build()` is invoked when `ServerBuilder.build()` is invoked
 
  