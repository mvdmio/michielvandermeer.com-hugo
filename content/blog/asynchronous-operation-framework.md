+++
title = "Asynchronous Operation Framework (AOF)"
date = 2019-10-15
feature_image = "/images/blog/asynchronous_operation_framework.png"
author = "Michiel van der Meer"
tags = ["Concept"]
+++

Some API calls need to perform fully asynchronous operations, like wait for a serverless function to complete or some other event to fire. It is not advisable to wait for these asynchronous operations to finish before completing the API request, since such requests block sockets and the caller might want to do something else while waiting for the operation(s) to finish.

My client has a use-case that requires some operations to run asynchronously without the user proceeding to the next step. I've created this concept to support these kinds of use cases.

Microsoft Azure Durable Functions already support such use cases. In the case of Durable Functions a status url is returned that the client can use to periodically poll the status of the request. However, this is not possible in ASP.NET Core API controllers at the time of writing.

To support this in ASP.NET Core API projects, I propose the following model. 
- The client calls the Public API and receives a status-check URL in the response. 
- The public API creates a new operation at the Asynchronous Operation API (AOF API) and receives the newly created `operationId` as a response.
- The public API triggers the asynchronous operation and passes it the `operationId`
- The asynchronous operation updates the status of the operation as-needed. In the example this is done once (in-progress).
- The client checks the status of the operation at any time and receives the latest status as a response
- When done, the asynchronous operation calls the `Complete()` method on the AOF API for the opeartion
- When the client retrieves the status of the operation after `complete()` has been called, the client will receive the `Completed` state. This signals the client to continue the user flow.

![Asynchronous Operation Framework](/images/blog/asynchronous_operation_framework.png)

Some additional requirements:
- The AOF API should be able to combine the state of multiple operations if a single unit-of-work involves multiple seperate asynchronous operations.
- The AOF API should also have a `Error()`, `Faulted()` or `Fail()` method so that operations can be marked as failed.
- `SetState()` can be used to set any state. The only named states that the AOF API specifies are: `Created`, `Completed` and `Failed`. All other states are at the descression of the clients.