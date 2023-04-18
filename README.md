# Vanilla JavaScript version of AJAX

This is a helper function for making AJAX requests.

## Usage
To use this function, call it with an options object. The options object should contain any or all of the following properties:

- `url` (optional, default: current page) - The URL to send the request to.
- `type` (optional, default: GET) - The HTTP method to use for the request.
- `async` (optional, default: true) - Whether to perform the request asynchronously.
- `data` (optional) - Data to be sent to the server. If the HTTP method is one that cannot have an entity body, such as GET, the data is appended to the URL.
- `headers` (optional) - HTTP headers to be sent with the request.
- `beforeSend` (optional) - A function to be called before the request is sent.
- `progress` (optional) - A function to be called periodically while the request is in progress.
- `success` (optional) - A function to be called when the request is successful.
- `failure` (optional) - A function to be called when the request fails.
- `complete` (optional) - A function to be called when the request is complete (whether it succeeded or failed).
- `error` (optional) - A function to be called when the request couldn’t be made. E.g., network failure, cross-origin access
- `abort` (optional) - A function to be called if the request is aborted.
- `timeout` (optional) - The local timeout (in milliseconds) for the request.
- `ontimeout` (optional) - A function to be called if the request times out.

## Examples
Here are a few examples showing how to use this function:

### Full with comments

```js
ajax({
  // url Specifies the URL to send the request to. Default is the current page
  url: "http://localhost/",
  type: 'GET',
  async: true, // default: true
  // Data to be sent to the server. If the HTTP method is one that cannot have an entity body, such as GET, the data is appended to the URL.
  data: {
    'foo': 'bar',
  },
  headers: {},
  beforeSend: () => {
    // Returning false in the beforeSend function will cancel the request.
    // return false;
  },
  progress: (xhr, loaded, total) => {
    console.log('progress');
    // Triggered periodically until the response is fully downloaded.
    // Using this event, we can track how much data is downloaded from the server.
    if (total) {
      console.log(`${loaded} of ${total}`);
    } else {
      console.log(`${loaded} downloaded`);
    }
  },
  success: (xhr, data) => {
    console.log('success', data);
  },
  failure: (xhr, data) => {
    console.log('failure', data);
  },
  // The load event is triggered when an XMLHttpRequest is completed successfully
  // (even if HTTP status is 400 or 500) and the response is fully downloaded.
  complete: (xhr) => {
    // A function to be called when the request finishes (after success and error/failure callbacks are executed).
    console.log('complete');
  },
  // When the request couldn’t be made. E.g., network failure, cross-origin access
  error: (xhr, error) => {
    console.log('Unable to make request');
  },
  abort: (xhr) => {
    console.log('abort');
  },
  timeout: null, // timeout	The local timeout (in milliseconds) for the request
  ontimeout: (xhr) => {
    console.log('ontimeout');
  },
});
```

### Practical - ready to use

```js
ajax({
  url: "http://localhost/",
  data: {
    'foo': 'bar',
  },
  beforeSend: () => {},
  progress: (xhr, loaded, total) => {
    if (total) {
      console.log(`${loaded} of ${total}`);
    } else {
      console.log(`${loaded} downloaded`);
    }
  },
  success: (xhr, data) => console.log('success', data),
  failure: (xhr, data) => console.log('failure', data),
  complete: (xhr)      => console.log("Response from server = ", xhr.responseText),
  error: (xhr, error)  => console.log('Unable to make request'),
});
```

## Short one

```js
ajax({
  url: 'http://localhost/',
  complete: (xhr) => console.log("Response from server = ", xhr.responseText),
});
```
