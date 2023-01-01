---
layout: default
title: Lesson Four - Let me in!
parent: Week 1
has_children: false
nav_order: 4
toc: true
---
# Week 1: Let me in!

Week 1 Step 4 ⬤⬤⬤⬤ | 🕐 Estimated completion: 25-35 minutes

## ✅ Tasks:
- [ ] ***1:*** Add on to the HTTP Trigger in the previous issue to check if the user’s parameter input of “password” equals `letmein`.
    - If it does, output "Access granted."
    - If it doesn’t equal the correct password, output “Access denied.”

## 1: Return from a Function

In the previous step, we received the password (the user's input). Now, we need to return either `Access denied.` or `Access granted.` to the user based on their input. **We can do this by returning it in the body of the request!**

>💡 Recall the `context.res` object we saw in the HTTP Trigger template.

```js
context.res = {
    // status: 200, /* Defaults to 200 */
    body: your_response
};
```

Place your message to the user in `your_response`!


## Test your Work
When you paste your **Function URL** in your browser or make a GET request with **Postman** with a `password` parameter of "letmein", you should get a response of “Access granted.“. Otherwise, your function should output “Access denied.“.

> Make sure you follow the *exact* responses we provided. `Access denied.` and `Access granted.`

## Walkthrough Video
[![walkthrough video](https://img.youtube.com/vi/rdAUUm3XwKE/0.jpg)](https://www.youtube.com/watch?v=rdAUUm3XwKE)