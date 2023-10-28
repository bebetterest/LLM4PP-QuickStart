# Accesses to LLMs

### Closed-source LLMs

#### Openai API

The most popular LLMs, GPT4 and ChatGPT(GPT3.5), are from Openai. The techniques and details are not available to the public, which is closed source. However, as long as your instructions are rdy and you have enough money, it's easy to call GPT4/GPT-3.5 to response. You can easily start from the official clear [guides](https://platform.openai.com/docs/guides/gpt/chat-completions-api). Here's an official example on gpt3.5-turbo to show you how easy it is:

```
# python

import openai
response = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Who won the world series in 2020?"},
        {"role": "assistant", "content": "The Los Angeles Dodgers won the World Series in 2020."},
        {"role": "user", "content": "Where was it played?"}
    ]
)
```

#### ANTHROPIC API

Not long after the eruption of ChatGPT, ANTHROPIC also announced its own close-source LLM, Claude. You can easily call the API according to [the official reference](https://docs.anthropic.com/claude/reference/complete\_post). Here's an official example on claude-2 to show you how easy it is:

```
# request

curl --request POST \
     --url https://api.anthropic.com/v1/complete \
     --header 'accept: application/json' \
     --header 'anthropic-version: 2023-06-01' \
     --header 'content-type: application/json' \
     --header 'x-api-key: $ANTHROPIC_API_KEY' \
     --data '
{
  "model": "claude-2",
  "prompt": "\n\nHuman: Hello, world!\n\nAssistant:",
  "max_tokens_to_sample": 256
}
'
```

#### GOOGLE API

Google's PaLM2 is available following [this link](https://developers.generativeai.google/tutorials/chat\_quickstart). Here's an official example on palm to show you how easy it is:

```
# python

import google.generativeai as palm
reply = palm.chat(context="Speak like Shakespeare.", messages='Hello')
print(reply.last)
```

It is worthy that the APIs are not free and you could not get access to the inside of the LLMs. For some APIs, there are additional settings such as temperature and services such as fine-tuning. Please read official specifications before your journey!

### Open-source LLMs

It seems that countless open-source LLMs are published every day. I will introduce 3 of them which I think are general for some experiments: [Alpaca](https://github.com/tatsu-lab/stanford\_alpaca), [Vicuna](https://github.com/lm-sys/FastChat#openai-compatible-restful-apis--sdk), [Llama2](https://github.com/facebookresearch/llama). You could implement them in the platform [huggingface ](https://huggingface.co/)with the corresponding easy-to-use library, transformers.

First, I would like to introduce [huggingface](https://huggingface.co/), a platform includes many open-source LLMs and an easy-to-use library, transformers. You could easily download a LLM, make some adjustments and run inference with transformers.

Alpaca/Vicuna are instruction-following LLMs, fine-tuned Llama models on collected self-instructs/user-shared conversations; Llma2 are new LLMs released by Meta. In addition, Vicuna has updated a new version based on Llma2.

To get access to Alpaca, you may have to recovering the weights with haggingface following the steps in the GitHub repository. For Vicuna, several methods, such as Openai-compatible APIs and huggingface generation APIs, are available. You could also apply Llma2 following the corresponding readme by the customized code and transformers library.

Here, with obtained model structures and the corresponding weights for free, you could adjust any detail as you like. However, you may need to change the source codes, **construct input contents with the correct format** and adjust/write inference codes utilizing libraries such as transformers, langchain and pytorch by yourself.

Besides, you would run the LLMs on your computation device(s)/service(s). Thus, you have to consider on your machines. To save memory or speed inference, you may need something special such as model parallelism and data parallelism. **However, maybe money is all you need** :smile:**.**

I think these models are enough for you to start. When they are not, you are rdy to find some you like in huggingface/github...

### Some additions for Chinese

Because of the special policy for the country safety, in China, the accesses mentioned above may be limited. Here I would introduce some available accesses in China.

#### BAIDU QIANFAN

It is a platform inlcudes many services on LLMs. Here we just introduce APIs. QIANFAN includes APIs of not only its own LLM, ERNIE-Bot, but also some open-source LLMs such as BLOOMZ and Llama2. Following [the document](https://cloud.baidu.com/doc/WENXINWORKSHOP/s/4lilb2lpf), we could simply call APIs such as ernie-bot as follows.

```
// python

import requests
import json

def main():
        
    url = "https://aip.baidubce.com/rpc/2.0/ai_custom/v1/wenxinworkshop/chat/completions_pro?access_token=" + your_access_token
    
    payload = json.dumps({
        "messages": [
            {
                "role": "user",
                "content": "请介绍一下你自己"
            },
            {
                "role": "assistant",
                "content": "我是百度公司开发的人工智能语言模型，我的中文名是文心一言，可以协助您完成范围广泛的任务并提供有关各种主题的信息，比如回答问题，提供定义和解释及建议。如果您有任何问题，请随时向我提问。"
            },
            {
                "role": "user",
                "content": "我在上海，周末可以去哪里玩？"
            },
            {
                "role": "assistant",
                "content": "上海是一个充满活力和文化氛围的城市，有很多适合周末游玩的地方。以下是几个值得推荐的地方：

1. 上海科技馆：上海科技馆是中国大陆最大的科技馆之一，有许多互动展览和科学实验室，可以让您了解科技的发展历史和最新成果。
2. 上海博物馆：上海博物馆是一座集艺术、历史和文化于一体的博物馆，有许多精美的艺术品和文物，可以让您深入了解中国和世界的文化历史。
3. 外滩：外滩是上海的标志性景点之一，有许多高楼大厦和繁华的商业街区，是欣赏黄浦江美景和城市风貌的好去处。
4. 上海迪士尼乐园：上海迪士尼乐园是世界上最大的迪士尼主题公园之一，有许多精彩的游乐项目和演出，可以让您尽情享受娱乐和欢乐。
5. 上海野生动物园：上海野生动物园是一个以自然保护为主题的野生动物园，有许多珍稀动物和植物，可以让您近距离接触大自然。

这些地方都是上海周末游玩的好去处，可以根据自己的兴趣和需求选择合适的行程。"
            },
            {
                "role": "user",
                "content": "上海有哪些美食？"
            }
        ]
    })
    headers = {
        'Content-Type': 'application/json'
    }
    
    response = requests.request("POST", url, headers=headers, data=payload)
    
    print(response.text)
    

if __name__ == '__main__':
    main()
```

#### ALI DashScope

DashScope is a platform similar to QIANFAN. We could call various APIs of LLMs including Qwen. Follow [the corresponding document](https://help.aliyun.com/zh/dashscope/developer-reference/quick-start?spm=a2c4g.11186623.0.0.59964bc140qR3j), we could call APIs such as as Qwen follows.

```
# python
# For prerequisites running the following sample, visit https://help.aliyun.com/document_detail/611472.html
from http import HTTPStatus
import dashscope


def call_with_messages():
    messages = [{'role': 'system', 'content': 'You are a helpful assistant.'},
                {'role': 'user', 'content': '如何做炒西红柿鸡蛋？'}]

    response = dashscope.Generation.call(
        dashscope.Generation.Models.qwen_turbo,
        messages=messages,
        result_format='message',  # set the result to be "message" format.
    )
    if response.status_code == HTTPStatus.OK:
        print(response)
    else:
        print('Request id: %s, Status code: %s, error code: %s, error message: %s' % (
            response.request_id, response.status_code,
            response.code, response.message
        ))


if __name__ == '__main__':
    call_with_messages()
```

#### ALI ModelScope

[ModelScope ](https://modelscope.cn/home)is a platform similar to huggingface. An easy-to-use library is also included.





## to be continue

