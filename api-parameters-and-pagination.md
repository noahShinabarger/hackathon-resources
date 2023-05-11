# Lab 2: Query Parameters and Pagination with APIs

Objective: Learn how to use query parameters to filter, sort, and paginate API responses using `curl`.

## Overview

In this lab, we'll continue using the JSONPlaceholder API to learn how to work with query parameters. Query parameters are used to refine the data returned by an API and can be used for filtering, sorting, and pagination.

## Step 1: Filtering Data

We'll start by filtering the data returned by the API using query parameters. For example, let's filter the list of posts by a specific user. To do this, run the following command:

```bash
curl -X GET "https://jsonplaceholder.typicode.com/posts?userId=1"
```

This command sends a GET request to the API and includes the `userId` query parameter to filter posts by user ID 1.

## Step 2: Combining Multiple Query Parameters

You can combine multiple query parameters to further refine the data returned by the API. For example, let's filter the list of comments by post ID and sort them by email. To do this, run the following command:

```bash
curl -X GET "https://jsonplaceholder.typicode.com/comments?postId=1&_sort=email&_order=asc"
```

This command sends a GET request to the API and includes the following query parameters:

- `postId`: Filter comments by post ID 1.
- `_sort`: Sort the results by the specified field (in this case, email).
- `_order`: Determine the sort order (either `asc` for ascending or `desc` for descending).

## Step 3: Pagination

Many APIs implement pagination to limit the number of results returned per request. JSONPlaceholder supports the `_start` and `_limit` query parameters for pagination. Let's retrieve a limited number of results from the list of posts. To do this, run the following command:

```bash
curl -X GET "https://jsonplaceholder.typicode.com/posts?_start=0&_limit=5"
```

This command sends a GET request to the API and includes the following query parameters:

- `_start`: The starting index of the results (in this case, 0, which is the first result).
- `_limit`: The maximum number of results to return (in this case, 5).

## Conclusion

By the end of this lab, you should have a better understanding of how to use query parameters with `curl` to filter, sort, and paginate API responses. This knowledge will help you work more effectively with APIs that support query parameters for refining the data returned.

### [Lab 3: API Error Handling](error-handling.md)
