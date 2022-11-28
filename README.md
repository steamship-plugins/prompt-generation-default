# Steamship Prompt Text Generation Plugin

This project implements Steamship's default text-generation plugin. The goal is to take an arbitrary prompt
(represented in a File) and continue the text as best it can.


## Usage

This plugin is invoked in the standard Tagger interface:

```python
from steamship import Steamship, File

client = Steamship()

generator = client.use_plugin(plugin_handle='prompt-generation-default')
...
file: File
file.tag(plugin_instance=generator.handle).wait()
file.refresh()
```
 
## Output

For each `Block` in the `File`, the tagger will produce an additional `Tag` with `kind` `TagKind.GENERATION`, 
`name` `GenerationTag.PROMPT_COMPLETION`, and `value` `{'string_value':'<the generated text>'}`.

## Parameters

 * __max_words__ - The maximum number of tokens to generate after the prompt
 * __temperature__ - Controls randomness. Lower values produce higher likelihood / more predictable results; higher values produce more variety. Values between 0-1.
 * __openai_api_key__ - OpenAI API key.

##TODOS
 * Capture output scores
 * Param for # of alternatives

