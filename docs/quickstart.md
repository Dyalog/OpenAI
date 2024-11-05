## Getting Started
This is an abbreviated introduction to get you started with `OpenAI`. The [OpenAI website](https://platform.openai.com) has considerably more information. `OpenAI` uses `HttpCommand` to communicate with the OpenAI API.

### 1. Create an OpenAI account
* Navigate to OpenAI's [quickstart page](https://platform.openai.com/docs/quickstart). 
* Click "Sign up" and follow the instructions to create your account

### 2. Optionally, create an OpenAI project
* You can create an OpenAI project. If you don't create a project, OpenAI will use a Default project.

### 3. Create an OpenAI API project key
You will need a project API key to be able to access the OpenAI API via `OpenAI`. Protect this API key, **do not** publish it on GitHub or other public places.

* Navigate to OpenAI's [API keys page](https://platform.openai.com/api-keys)
* Click "+ Create a new secret key"
* Click "Create secret key"
* Make sure you copy and save the generated secret key! **This will be the only time it will be displayed.**
* OpenAI recommends that you set an environment variable to hold your API key.  This way you will not expose the key in your APL code.<br>If you're using Linux, do: `export OPENAI_API_KEY="your_api_key_here"`<br>If you're using Windows, under PowerShell do: `setx OPENAI_API_KEY "your_api_key_here"`
* If you choose to not use an environment variable, you could save your API key in a text file and then   
 
### 4. Obtain `OpenAI`
There are a couple options to obtain `OpenAI`.

* Use the `]get` user command 
```
      ]get github.com/Dyalog/OpenAI/blob/main/source/OpenAI.apln
```
* Download [`OpenAI.apln`](https://github.com/Dyalog/OpenAI/releases/latest) from GitHub. Remember where you saved the downloaded file and then use the `]import` user command, replacing "downloaded-file-path" with the path name where you saved the downloaded file.
```
      ]import # downloaded-file-path/OpenAI.apln
```

### 5. Configure `OpenAI`
Now that you have `OpenAI` in your workspace, you can configure it. First, run `OpenAI.Initialize`. This will copy the latest release of `HttpCommand` into the `OpenAI` namespace.
```
      OpenAI.Initialize
0  Initialized
```
If the result of `OpenAI.Initialize` is not as shown above, the result will contain an error message explaining what failed.

If you have saved your OpenAI API key as an environment variable, you can use `HttpCommand`'s `HeaderSubstitution` setting to have `HttpCommand` use the environment variable rather than explicitly setting the API key in the configuration.

```
      OpenAI.HttpCommand.HeaderSubstitution←'%'        ⍝ sets '%' as the environment variable indicator
      OpenAI.APIKey←'%your-environment-variable-name%' ⍝ note the leading and trailing '%'
```
If you have not saved your OpenAI API key as an environment variable, you will need to set `OpenAI.APIKey` to the API key's value directly.
```
      OpenAI.APIKey←'your-OpenAI-API-key-here'
```
## Next Steps
Having completed the above steps, you are now ready to begin interacting with the OpenAI API. From here you may want to look at:

* [`OpenAI` demos](./demos.md)
* [Using `OpenAI`](./userguide.md)