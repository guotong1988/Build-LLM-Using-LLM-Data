# Build-LLM-Using-LLM-Data
Build LLM/MLLM From Scratch Using LLM/MLLM Data

## Chat Test
Start vLLM server
```
python3 -m vllm.entrypoints.openai.api_server --model /my_model_path/ --host 0.0.0.0 --port 8001 --served-model-name my_model
```
Request
```
curl http://localhost:8000/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "/the_model_path/",
    "messages": [
      {"role": "system", "content": "You are a helpful assistant."},
      {"role": "user", "content": "你好"}
    ],
    "temperature": 0.7,
    "max_tokens": 4096
  }'
```
EVAL
```
evalscope eval --model my_model --eval-type openai_api --api-url http://127.0.0.1:8001/v1 --api-key EMPTY --datasets ceval --generation-config '{"max_tokens":6000}' --limit 10
```


## Eval Results
| **Base Model**   | **SFT Dataset** | **ceval** | **cmmlu** | **mmlu** | **math_500**|
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| Qwen3-32B-Base  | [Chinese](https://download.csdn.net/download/guotong1988/92837490), Non-thinking, 3 Epoch | 0.7077 | 0.791 | 0.7789 | 0.78 |
| Qwen3-32B-Base  | [Chinese](https://download.csdn.net/download/guotong1988/92837490) + [English](https://download.csdn.net/download/guotong1988/92837508), Non-thinking, 2 Epoch | 0.7194 | 0.8075 | 0.7871 | 0.8133 |
