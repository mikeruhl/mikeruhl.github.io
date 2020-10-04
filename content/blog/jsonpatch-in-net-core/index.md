---
title: "JsonPatch in .NET Core"
date: 2019-02-22
description: import from previous blog.
---
## A brief Overview

[JsonPatch](https://tools.ietf.org/html/rfc6902) is a way to patch a remote resource using a standard that can be universally applied to any resource. In .NET, if you were to send a PATCH request with your class being serialized upon the method's entry, you'd get default values for any property you didn't specify. Well, for a `PATCH` that's awfully ambiguous. Did the caller mean to set that property to null or just omit it since this is a `PATCH`?

Well, there's a simple solution to this: JSonPatch. A JsonPatch request can be super-simple. It composes 3 parts:



