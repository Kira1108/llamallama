# Use Llama API

*Step 1 - [Get API Key from Llama official page](https://docs.llama-api.com/quickstart)*

*Step 2 - Install Llama python package*  
```bash
pip install llamaapi
```

*Step 3 Use the function from documentation*

```python
import json
from llamaapi import LlamaAPI

# LLama API key
llama = LlamaAPI("<your_api_token>")

# 请求体
# 1. 一个正常的聊天历史
# 2. LLM可以调用的本地函数schema
api_request_json = {
    "messages": [
        {"role": "user", "content": "What is the weather like in Boston?"},
    ],
    "functions": [
        {
            "name": "get_current_weather",
            "description": "Get the current weather in a given location",
            "parameters": {
                "type": "object",
                "properties": {
                    "location": {
                        "type": "string",
                        "description": "The city and state, e.g. San Francisco, CA",
                    },
                    "days": {
                        "type": "number",
                        "description": "for how many days ahead you wants the forecast",
                    },
                    "unit": {"type": "string", "enum": ["celsius", "fahrenheit"]},
                },
            },
            "required": ["location", "days"],
        }
    ],
    "stream": False,
    "function_call": "get_current_weather",
}

# 向Llama API发送请求
response = llama.run(api_request_json)
print(json.dumps(response.json(), indent=2))
```


