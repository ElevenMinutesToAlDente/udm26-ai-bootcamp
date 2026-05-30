## Module 1 notes

Module consisted of setting up anaconda environment with Jupyter notebook. However for my own home setup, I use headless linux dev environment, so I created an equivalent environment using `uv` and `venv`

I like to ssh tunnel to the linux machine from my laptop. Doing so is trivial

```bash
uv run jupyter lab --no-browser --port=8888
```

This runs a notebook server, then I use tools like vscode ssh port forwarding feature for tunneling.

Then can access the notebook from browser

The course requires you to make an OpenAI account and create an API token, but OpenAI free tier no longer provides free tier API tokens. So I briefly explored using groq free tier API tokens running open source models like llama. Good thing about this is it is compatible with python openai package and its client. 

```python
from openai import OpenAI
from dotenv import load_dotenv
import os

load_dotenv()

client = OpenAI(
    api_key=os.getenv("GROQ_API_KEY"),
    base_url="https://api.groq.com/openai/v1"
)

response = client.chat.completions.create(
    model="llama-3.1-8b-instant",
    messages=[{"role": "user", "content": "Say hello!"}]
)

print(response.choices[0].message.content)
```

While this worked, it doesn't provide the response object with all of its fields populated like the vanilla call to openai. And the further course work uses openai so, I caved in and spent $5 on OpenAI API credits just to move along the course

The rest of the module was pretty straightforward, playing around with personas, tokenizer from openai, playing with openai client.

P.S. Course material you download is chmod 555, so you can't edit but one can easily change this file permission. 