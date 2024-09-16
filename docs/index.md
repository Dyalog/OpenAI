`OpenAI` is a Dyalog APL namespace that contains code to interact with the [OpenAI API](https://platform.openai.com/docs/api-reference/introduction). OpenAI develops and maintains several Large Language Models (LLMs). `OpenAI` contains code to interact with OpenAI endpoints. A few things to note:

* We are going to use the term "OpenAI" a lot in this documentation. When formatted as `OpenAI`, we are referring to the Dyalog namespace which implements an interface to the OpenAI API. When formatted as OpenAI, we are referring to the OpenAI API itself.
* ChatGPT is actively developing OpenAI, adding new LLMs and endpoint definitions. This puts us in a reactive mode to incorporate these new features and interfaces. We anticipate  
* Not all OpenAI endpoints are currently implemented in `OpenAI`. This is partly due to the reason stated above. Our goal is to have sufficient endpoint coverage that our users can perform useful tasks with OpenAI from APL.
* There are other LLMs available - `OpenAI` should serve as a good model for how to implement interfaces to them. In particular, `OpenAI` makes heavy use of [`HttpCommand`](https://dyalog.github.io/HttpCommand) and the techniques used should be applicable for interacting with other LLM APIs.
* This documentation presents information on how to use the `OpenAI` namespace to interact with the OpenAI endpoints. It does not attempt to document all of the features and nuances of those endpoints.  For that information, please see the [OpenAI API Reference](https://platform.openai.com/docs/overview).
* We encourage feedback, feature requests, and guidance from our users.

## Endpoints Currently Implemented

* [Audio](./userguide.md#audio) - turn audio into text or text into audio
* [Chat](./userguide.md#chat) - have a conversation with an OpenAI model
* [Files](./userguide.md#files) - upload and manage documents that can be used with other features
* [Image](./userguide.md#image) - given a prompt or existing image, generate a new image
* [Models](./userguide.md#models) - list and describe the various models available in the OpenAI API
* [Moderations](./userguide.md#moderations) - Classify text input as potentially harmful

## Forthcoming Endpoints
### Expected in October 2024
OpenAI has released, in beta, version 2 of their Assistants and related endpoints. We expect to have completed their development in `OpenAI` in October 2024. 

* Assistants - Build assistants that can call models and use tools to perform tasks. 
* Threads  - Create threads that assistants can interact with.
* Messages - Create messages within threads.
* Runs - Represents an execution on a thread.
* Vector Stores - Used to store files for use be the OpenAI's `file_search` tool.
* Vector Store Files - Represent files inside a vector store.
### Future
Beyond October 2024, we expect to add support for the following endpoints.

* Vector Store File Batches - Represent operations to add multiple files to a vector store.
* Run Steps - Represents the steps (model and tool calls) taken during the run.
* Uploads - Upload large files in multiple parts.
* Embeddings - Get a vector representation of a given input that can be easily consumed by machine learning models and algorithms.

Other future work may include Projects and Users endpoints depending on our users' needs.