---
title: What is Node
---

NodeJS is an asynchronous event-driven JavaScript runtime, designed to build scalable networks. What this means is NodeJS is designed to handle multiple concurrent requests without blocking.

This allows NodeJS to handle thousands of concurrent requests making it very performant. It does this by using asynchronous function calls to complete tasks that would normally block the thread e.g. reading / writing to disk, making database calls etc. Node issues a call to a disk write function and carries on its own processing, when the activity completes node is notified via a call back function and resumes processing of the original request.

Node is written in JavaScript allowing the same developer who works on the frontend to also work on the backend without having to learn a whole new language. 

There are multiple plugin libraries for NodeJS saving the developer time.


