

Whenever you see OpenAI formatted as `OpenAI`, it is referring to the Dyalog OpenAI API interface. `OpenAI` is a Dyalog APL namespace which contains code that implements interfaces to OpenAI API endpoints.

## Getting Started
To use the OpenAI API, you will need to:

* Create an OpenAI account
* Optionally, create an OpenAI project
* Create an OpenAI API key - this will enable you to make calls to the OpenAI API
* Download `OpenAI`
* Configure `OpenAI`

### Create an OpenAI account
* Navigate to OpenAI's [quickstart page](https://platform.openai.com/docs/quickstart). 
* Click "Sign up" and follow the instructions to create your account

### Optionally, create an OpenAI project
* Optionally, create an OpenAI project. If you don't create a project, OpenAI will use a "Default project".
* Create one or more project API key(s). You will need a project API key to be able to access the OpenAI API via `OpenAI`. Protect this API key, **do not** publish it on GitHub or other public places.
    * Navigate to OpenAI's [API keys page](https://platform.openai.com/api-keys)
    * Click "+ Create a new secret key"
    * Click "Create secret key"
    * Make sure you copy the generated secret key! **This will be the only time it will be displayed.**
    * OpenAI recommends that you set an environment variable to hold your API key.  This way you will not expose the key in your APL code.<br>If you're using Linux, do: `export OPENAI_API_KEY="your_api_key_here"`<br>If you're using Windows, under PowerShell do: `setx OPENAI_API_KEY "your_api_key_here"`

    * 
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
