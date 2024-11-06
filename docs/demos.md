You'll need to register and obtain an OpenAI API key as described in the [Quick Start page](./quickstart.md).

### Obtaining the demos

The easiest way to obtain and set up the `OpenAI` demos is to use the `]get` user command.

```
      )clear
clear ws
      ]get https://github.com/Dyalog/OpenAI/archive/refs/heads/main.zip
Working on it…
#.main
      )cs #.main.demos
#.main.demos
```

If this doesn't work for you, then you can download and unzip [demos.zip](https://github.com/Dyalog/OpenAI/releases/latest) from GitHub.
Using the folder name that you unzipped into, use `]link.import` to import the demos.

```
    ]link.import # /your-folder-name-here/OpenAI-main/demos
Imported: # - ...
```

### Setting up the demos
 Run the `Setup` function to initialize `OpenAI`.

```
      Setup
Enter your OpenAI API key or the environment variable that contains your API key: your-API-key-here
The OpenAI interface is set up and ready for use
```

At the prompt either enter your OpenAI API key or, if you've saved your API key in an environment variable, enter the name of the environment variable.

Congratulations!  You're now ready to run the demos.

## Audio Demo Functions

* `Speech` which generates audio from text input.
* `Play` uses HTMLRenderer to play an audio file.
* `Transcription` which transcribes audio into the input language.
* `Translation` which translates audio in the English text.
* `ShowText` uses HTMLRenderer to display the result of `Transcription` or `Translation`.

### `Speech`
|--|--|
| Syntax | `(rc msg)←audioFile Speech text` |
| `audioFile` | The name of the .mp3 audio file to save. You do not have to specify the .mp3 extension. |
| `text` | Either<ul><li>The actual text to be converted to audio</li><li>The name of a file, prefixed with `file://`, containing the text to be converted.</li></ul> |
| `rc` | Either<ul><li>`0` indicating the text was successfully converted and written to the file.</li><li>non-`0` indicating some error occurred.</li></ul>|
| `msg` | Either<ul><li>If `rc` is `0`, the name of the audio file written (including the .mp3 extension)</li><li>If `rc` is not `0`, a message indicating what might have gone wrong</li></ul>|
| Example |&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`'/tmp/spanish.mp3' Speech 'APL es muy fácil de aprender y divertido de usar'`<br/>`0  C:/tmp/spanish.mp3`|        
| Notes | You can pass the result of `Speech` as the argument to `Play` to play the audio file.<br/>For example: `Play '/tmp/test' Speech 'This is a test'`|

### `Play`
|--|--|
| Syntax | `Play args` |
| `args` | Either<ul><li>The name of a .mp3 audio file to play.</li><li>The result from `Speech`</li></ul>|
| Examples |&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`Play '/tmp/test' Speech 'This is a test'`<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`Play '/tmp/spanish.mp3'`|        

### `Transcription`
|--|--|
| Syntax | `(rc msg)←Transcription args` |
| `args` | `audioFile [language]` where<ul><li>`audioFile` is the name of the .mp3 audio file to transcribe.</li><li>`language` is an optional 2-character [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes) language code. This will assist OpenAI to determine the spoken language in the audio file.|
| `rc` | Either<ul><li>`0` indicating the audio file was successfully transcribed.</li><li>non-`0` indicating some error occurred.</li></ul>|
| `msg` | Either<ul><li>If `rc` is `0`, the transcribed text</li><li>If `rc` is not `0`, a message indicating what might have gone wrong</li></ul>|
| Example |&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`Transcription '/tmp/spanish.mp3'`<br/>`0  APL es muy fácil de aprender y divertido de usar.` |        
| Notes | You can pass the result of `Transcription` as the argument to `ShowText` to display the transcribed text in an HTMLRenderer window.<br/>For example: `ShowText Transcription '/tmp/spanish.mp3'`|

### `Translation`
|--|--|
| Syntax | `(rc msg)←Translation args` |
| `audioFile` | The name of the .mp3 audio file to translate.|
| `rc` | Either<ul><li>`0` indicating the audio file was successfully translated.</li><li>non-`0` indicating some error occurred.</li></ul>|
| `msg` | Either<ul><li>If `rc` is `0`, the translated text</li><li>If `rc` is not `0`, a message indicating what might have gone wrong</li></ul>|
| Example |&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`Translation '/tmp/spanish.mp3'`<br/>`0  APL is very easy to learn and fun to use.` |        
| Notes | You can pass the result of `Translation` as the argument to `ShowText` to display the translated text in an HTMLRenderer window.<br/>For example: `ShowText Translation '/tmp/spanish.mp3'`|

### `ShowText`
|--|--|
| Syntax | `ShowText args` |
| `args` | The result from `Transcription` or `Translation`|
| Examples |&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`ShowText Transcription '/tmp/spanish.mp3'`|   

## Image Demo Functions

* Image - generate an image from a text prompt
* ShowImage - display an image using HTMLRenderer

### `Image`
|--|--|
| Syntax | `(rc msg)←Image description` |
| `description` | a description of the image to generate. The description can be in most languages.|
| `rc` | Either<ul><li>`0` indicating an image was successfully generated.</li><li>non-`0` indicating some error occurred.</li></ul>|
| `msg` | Either<ul><li>If `rc` is `0`, the base64-encoded representation of the .png image data</li><li>If `rc` is not `0`, a message indicating what might have gone wrong</li></ul>|
| Example |&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`Image 'drei süße Welpen' ⍝ three cute puppies`|        
| Notes | You can pass the result of `Image` as the argument to `ShowImage` to display the generated imagein an HTMLRenderer window.<br/>For example: `ShowImage Image 'a pretty sunset on the water'`|

### `ShowImage`
|--|--|
| Syntax | `ShowImage args` |
| `args` | The result from `Image`|
| Examples |&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`ShowImage Image 'dos perros' ⍝ two dogs`|   

## Chat Demo Functions

* Chat - have a chat with an assistant you describe
* Linguist - translate phrases into a desired language, optionally playing audio of the translation

### `Chat`
|--|--|
| Syntax | `Chat` |
| Usage | <ul><li>Describe the type of assistant you want to chat with; a more detailed description will generally result in more focused response.</li><li>Then ask questions, give directions, and so on for the assisant to respond to. The assistant "remembers" the conversation so you can build upon previous inputs and responses.</li><li>Pressing "Enter" without entering any text will cause `Chat` to exit.</li></ul> |

#### `Chat` Example 1
```      
      Chat
Describe the assistant you would like to chat with: poetic
Enter user message: compose a haiku about APL

Symbols dance with code,
APL's concise power,
Elegance in form.

Enter user message: translate that to German

Symbole tanzen mit Code,
APLs präzise Kraft,
Eleganz in Form.

Enter user message: 
```
#### `Chat` Example 2
```
      Chat
Describe the assistant you would like to chat with: you understand programming languages
Enter user message: translate APL's +.× to python
                                                                               
In APL, the +.× operator represents the matrix multiplication operation. To    
translate this operation to Python using NumPy, you can use the numpy.dot()    
function. Here's how you can do it:                                            
                                                                               
python                                                                         
import numpy as np                                                             
                                                                               
# Define two matrices                                                          
matrix1 = np.array([[1, 2], [3, 4]])                                           
matrix2 = np.array([[5, 6], [7, 8]])                                           
                                                                               
# Perform matrix multiplication                                                
result = np.dot(matrix1, matrix2)                                              
                                                                               
print("Result of matrix multiplication:")                                      
print(result)                                                                  
                                                                               
                                                                               
In this Python code snippet, we first import the NumPy library. We define two  
matrices matrix1 and matrix2 using NumPy arrays. Then, we use the np.dot()     
function to perform matrix multiplication between matrix1 and matrix2. Finally,
we print the result of the matrix multiplication.                              
                                                                               
Enter user message:
```


### `Linguist`
|--|--|
| Syntax | `Linguist` |
| Usage | <ul><li>Specify the output language that you would like</li><li>Specify whether you would like audio output for the responses</li><li>Enter some text to translate and press Enter<br>(pressing Enter without any text will exit `Linguist`)</li><li>`Linguist` will display the translation text</li><li>If you specified that you would like audio output, a window with audio controls will pop up and you can play the audio.<br>You must close the window to enter more text to translate.|   

#### `Linguist` Example

```
      Linguist
What output language would you like? German
Would you like audio output (y/N)? n
Text to translate: Good morning
Guten Morgen

Text to translate: Buenos dias
Guten Morgen

Text to translate: 
```