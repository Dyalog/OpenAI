## Getting Started
### Register and Create an OpenAI Project
To use OpenAI API, you will need to:

* [Create an account with OpenAI](https://platform.openai.com/signup). 
* Provide billing/payment information.
* Create a project
* Create one or more project API key(s). You will need a project API key to be able to access the OpenAI API via `OpenAI`. Protect this API key, do not publish it in GitHub or other public places.
### Obtain `OpenAI`
Download [`OpenAI.apln`](https://github.com/Dyalog/OpenAI/releases/latest) from GitHub.
### Configure `OpenAI`
You will need to provide the API key you created earlier.

```
      OpenAI.APIKey←'your-API-key-here'
```
You may not want to include your API key in your code that initializes `OpenAI`. One technique to avoid this is to store your APIKey in an environment variable and then retrieve its value.
```
      OpenAI.APIKey←2 ⎕NQ # 'GetEnvironment' 'your-APIKey-environment-variable-name'
```
## `OpenAI` Initialization
`OpenAI` makes heavy use of `HttpCommand` and requires `HttpCommand` version 5.6 or later. During initialization, `OpenAI` will look for `HttpCommand` in its parent namespace and if it doesn't find `HttpCommand` it will load it from your Dyalog installation and then upgrade to the latest version of HttpCommand. The endpoints implemented in `OpenAI` will initialize `OpenAI` if not already initialized. You can also initialize `OpenAI` by running `OpenAI.Initialize`. In a production environment, `HttpCommand` should be copied and saved into the workspace rather than relying on loading and upgrading.

## `OpenAI` Naming Conventions
Each of the endpoints implemented in `OpenAI` has a number of parameters. Parameters beginning with a lower-case letter (a-z) are parameters that OpenAI itself uses. Parameters beginning with an upper-case letter (A-Z) are parameters used by `OpenAI` to make it easier to use in an APL environment.  

## Endpoints
Most endpoints, when run, will save the last `HttpCommand` response namespace in the `Response` variable for the endpoint. This can be used to access the result of the endpoint's execution or to examine in case the execution failed.

For example:
```
      s←OpenAI.Audio.Speech 'This is a test'
      s.Run
[rc: 0 | msg:  | HTTP Status: 401 "Unauthorized" | ≢Data: 1 (namespace)]
      s.Show ⍝ show Response.Data
{
  "error": {
    "code": null,
    "message": "You didn't provide an API key. You need to provide your API key in an Authorization header using Bearer auth (i.e. Authorization: Bearer YOUR_KEY), or as the password field (with blank username) if you're accessing the API from your browser and are prompted for a username and password. You can obtain an API key from https://platform.openai.com/account/api-keys.",
    "param": null,
    "type": "invalid_request_error"
  }
}
```
!!! Important
    Remember to set `OpenAI.APIKey` prior to running any endpoints.
