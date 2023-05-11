# Lab 3: Handling Errors and Rate Limiting with APIs

Objective: Learn how to handle errors and rate limiting in APIs using `curl`.

## Overview

In this lab, we'll explore error handling and rate limiting in APIs. Proper error handling is essential for building robust applications that can gracefully handle issues that may arise when interacting with APIs.

## Step 1: Understanding HTTP Status Codes

HTTP status codes are three-digit numbers that indicate the outcome of an HTTP request. They are grouped into five classes based on the first digit:

- 1xx (Informational): The request was received, and the server is continuing to process it.
- 2xx (Successful): The request was successfully received, understood, and accepted.
- 3xx (Redirection): The request needs further action to be completed.
- 4xx (Client Error): The request contains bad syntax or cannot be fulfilled by the server.
- 5xx (Server Error): The server failed to fulfill a valid request.

For this lab, we'll focus on some common 4xx status codes.

## Step 2: Triggering a 400 Bad Request Error

A 400 Bad Request error occurs when the server cannot process the request due to invalid syntax. Let's trigger this error by sending a malformed JSON payload in a POST request. To do this, run the following command:

```bash
curl -X POST -H "Content-Type: application/json" -d '{"malformedJson": "missingClosingBrace}' https://jsonplaceholder.typicode.com/posts
```

This command sends a POST request to the API with an invalid JSON payload, resulting in a 400 Bad Request error.

## Step 3: Triggering a 404 Not Found Error

A 404 Not Found error occurs when the requested resource could not be found on the server. Let's trigger this error by requesting a non-existent resource. To do this, run the following command:

```bash
curl -X GET "https://jsonplaceholder.typicode.com/nonexistent"
```


This command sends a GET request to an endpoint with a non-existent post ID, resulting in a 404 Not Found error.

## Step 4: Handling Errors in Your Application

When interacting with APIs, it's essential to handle errors gracefully. In your application, you should:

1. Check the HTTP status code of the response to determine if the request was successful.
2. If the request was not successful, parse the error response to gather more information about the issue.
3. Display a helpful error message to the user or implement a fallback mechanism (e.g., retrying the request, using cached data, or redirecting to an error page).

For example, if you're using a JavaScript-based application with the `fetch` API, you could handle errors as follows:

```javascript
fetch("https://jsonplaceholder.typicode.com/posts/999999")
  .then((response) => {
    if (!response.ok) {
      throw new Error(`HTTP error: ${response.status}`);
    }
    return response.json();
  })
  .then((data) => {
    // Process the data
  })
  .catch((error) => {
    console.error('There was a problem with the fetch operation:', error);
  });
```

In this example, the `fetch` function returns a `Promise` that resolves to the `Response` object representing the response to the request. This response is then processed and if the response was not successful (i.e., if the `ok` property of the `Response` object is `false`), an error is thrown.

The `catch` method is used to handle the error. In this case, it logs the error message to the console, but in a real-world application, you might want to show an error message to the user, retry the request, or perform some other error recovery action.

## Conclusion

By the end of this lab, you should have a better understanding of how to handle errors and rate limiting in APIs using `curl`. This knowledge will help you build more robust applications that can gracefully handle issues that may arise when interacting with APIs.
