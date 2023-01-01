---
layout: default
title: Lesson Three - Building our first function
parent: Week 1
has_children: false
nav_order: 3
toc: true
---
# Week 1: Building our first function

Week 1 Step 2 ⬤⬤⬤◯ | 🕐 Estimated completion: 35-45 minutes

# Building our first function ⚡[HackerVoice]

> Managing a server is pretty complicated. As a student, mastering serverless functions can help you to build projects that solve real-world problems by integrating APIs, constructing user interfaces, and analysing data without worrying about managing servers.
>
> [⚡️ 10 Ways to Use Serverless Functions](https://dev.to/aws/10-ways-to-use-serverless-functions-bme)

## ✅  Tasks:
- [ ] ***1:*** Create an Azure account
- [ ] ***2:*** Set up Azure locally on VS Code
- [ ] ***3:*** Create an HTTP trigger Azure function that gets content from a request parameter called `password` and returns it in the function's body
- [ ] ***4:*** Test your function locally with Postman and, when you confirm that it works, deploy your function


## 1: Create an Azure Account

Azure is Microsoft's cloud computing platform (similar to Google Cloud Platform and Amazon Web Services).

1. To create an Azure account, go to [Microsoft Azure](https://azure.microsoft.com/en-us/free/) and press **Start Free**.
2. After signing in with your Microsoft account and filling in your personal details, you will be asked to add a credit card.
  - This is only for security purposes (preventing multiple free accounts per person).
  - **You won't be charged** unless you choose to buy a premium account, which we do not need for this course.

## 2: Set Up Azure Locally on VS Code

1. Confirm if you have installed the Azure Tools extension on VS Code
2. [Create your local project](https://docs.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-csharp#create-an-azure-functions-project)
  - ‼️ When prompted to set the language, choose **JAVASCRIPT** not C#)
  - ‼️ When prompted for the Authorization level, **always** choose `Function`
4. [Run the function locally](https://docs.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-csharp#run-the-function-locally)
5. [Publish the project to Azure](https://docs.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-csharp#publish-the-project-to-azure)
6. Get your function url the Azure Portal
7. Test the function on Postman


### What should running the function look like?

Start the debugger by going to index.js and then pressing the F5 key.
> Having trouble with Azure Tools? Try installing it [this way](https://docs.microsoft.com/en-us/azure/azure-functions/functions-run-local?tabs=macos%2Ccsharp%2Cbash#install-the-azure-functions-core-tools)
<br>
<img src="https://media.giphy.com/media/2pETiGAEpifm4a24IP/giphy.gif" width=600/>
<br>

Once you receive the localhost link in the terminal, follow it and notice the terminal log "Executing 'Functions.[Name of your function]'" indicating that you made a request to the function.

![local](https://user-images.githubusercontent.com/28051494/122473796-2d1f0e80-cf77-11eb-9f31-476a041be64c.png)

<br>
<img src="https://media.giphy.com/media/efbultCFHf13YK0Isw/giphy.gif" width=600/>
<br>

If the request is successfully made in Postman this is what it should look like:

![Postman](https://user-images.githubusercontent.com/15052690/125126350-f85f2c80-e0c8-11eb-8796-8839a11752d0.png)

Once you deploy/publish the code to Azure successfully, you will get the function url in the Output of VS Code:

![output](https://user-images.githubusercontent.com/28051494/122473793-2c867800-cf77-11eb-9897-6f6f7472e710.png)


## 3: Create your own HTTP Trigger Function
*You should see the HTTP Trigger Function template code Microsoft Azure starts you with when you first create your trigger.*

### What is happening in index.js?

- Start of function definition: `module.exports = async function`
- Print comment in Azure Console anytime the function is triggered: `context.log()`
- Get parameter from request body: `const name`
- Conditional (ternary) operator to print message if parameter exists (else print error message):
  ```javascript
  //condition: if name exists
  name
  //? is chosen if the condition evaluates to true
  ? "Hello, " + name + ". This HTTP triggered function executed successfully."
  //: is chosen if the condition evaluates to false
  : "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response.";
  ```
- Results of that conditional ternary statement are assigned to `responseMessage` which is returned in the function body

**Now, let's begin coding by modifying that template.** First, you will need to retrieve content from a request parameter named `password`. Recall that parameters look like this in a full URL:
```
www.mywebsite.com/api/endpoint?param1=hi&param2=hi
```

### How to get content from a request parameter?

Request parameters are a way for an HTTP request to take in information! They are pretty much identical in purpose to why you would want a parameter for a function in a coding language. In this instance, we will need a parameter for the password.
- Request parameters are a property of the `req` or request parameter of the module
- The request has a `query` object that stores all of the parameters passed in
- You don't need to specify what parameters the user needs to input into the HTTP request
- You can acess any parameters that are sent in

You would access a parameter by calling on the query like this:
```javascript
<property name> = req.query.<your property here>;

//example:
let color = req.query.color;
```

>💡 If the user makes a request with a parameter of `<url>?color=blue` then the variable color in your function will hold that value.

>💡 Note: your parameter must be named `password`


Finally, we have to return *something* to the users. In this case, we will be returning the value of the request parameter we just retrieved.

### How can I return something in the function body?

In Azure, `context` is an object that holds data about the response of the HTTP function. Read more about [Accessing the request and response](https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference-node?tabs=v2#accessing-the-request-and-response).

In our HTTP trigger function, we have defined context object with the body property:

```javascript
context.res = {
        // status: 200, /* Defaults to 200 */
        body: responseMessage
    };
```

To return the password in body, simply replace `responseMessage` with `password`.


## 4: Test your Function with Postman

1. Deploy your function to Azure
2. Get your function url from the Output window on VS Code(same as before) and make a request on Postman
3. Add a parameter with the key `password` and give it any random value
4. Make sure that your function is returning the `password` parameter in the body

## Test your Work
**Option 1:**
Paste the *function url* directly in your browser and add the query parameters to the end of the url: `&param_name=param_value`. Your inputted password value should appear.

**Option 2:**
Use **Postman**! Paste the *function url* and make a GET request. In the output box, you should receive the value you put in for the request parameter.

## Walkthrough Video
[![walkthrough video](https://img.youtube.com/vi/zzipvT2htUU/0.jpg)](https://www.youtube.com/watch?v=zzipvT2htUU)
