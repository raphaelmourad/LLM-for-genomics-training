---
license: apache-2.0
language:
- fr
- it
- de
- es
- en
---
# Model Card for Mixtral-8x7B
The Mixtral-8x7B Large Language Model (LLM) is a pretrained generative Sparse Mixture of Experts. The Mistral-8x7B outperforms Llama 2 70B on most benchmarks we tested.

For full details of this model please read our [release blog post](https://mistral.ai/news/mixtral-of-experts/).

## Warning
This repo contains weights that are compatible with [vLLM](https://github.com/vllm-project/vllm) serving of the model as well as Hugging Face [transformers](https://github.com/huggingface/transformers) library. It is based on the original Mixtral [torrent release](magnet:?xt=urn:btih:5546272da9065eddeb6fcd7ffddeef5b75be79a7&dn=mixtral-8x7b-32kseqlen&tr=udp%3A%2F%http://2Fopentracker.i2p.rocks%3A6969%2Fannounce&tr=http%3A%2F%http://2Ftracker.openbittorrent.com%3A80%2Fannounce), but the file format and parameter names are different. Please note that model cannot (yet) be instantiated with HF.

## Run the model


```python
from transformers import AutoModelForCausalLM, AutoTokenizer

model_id = "mistralai/Mixtral-8x7B-v0.1"
tokenizer = AutoTokenizer.from_pretrained(model_id)

model = AutoModelForCausalLM.from_pretrained(model_id)

text = "Hello my name is"
inputs = tokenizer(text, return_tensors="pt")

outputs = model.generate(**inputs, max_new_tokens=20)
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```

By default, transformers will load the model in full precision. Therefore you might be interested to further reduce down the memory requirements to run the model through the optimizations we offer in HF ecosystem:

### In half-precision

Note `float16` precision only works on GPU devices

<details>
<summary> Click to expand </summary>

```diff
+ import torch
from transformers import AutoModelForCausalLM, AutoTokenizer

model_id = "mistralai/Mixtral-8x7B-v0.1"
tokenizer = AutoTokenizer.from_pretrained(model_id)

+ model = AutoModelForCausalLM.from_pretrained(model_id, torch_dtype=torch.float16).to(0)

text = "Hello my name is"
+ inputs = tokenizer(text, return_tensors="pt").to(0)

outputs = model.generate(**inputs, max_new_tokens=20)
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```
</details>

### Lower precision using (8-bit & 4-bit) using `bitsandbytes`

<details>
<summary> Click to expand </summary>

```diff
+ import torch
from transformers import AutoModelForCausalLM, AutoTokenizer

model_id = "mistralai/Mixtral-8x7B-v0.1"
tokenizer = AutoTokenizer.from_pretrained(model_id)

+ model = AutoModelForCausalLM.from_pretrained(model_id, load_in_4bit=True)

text = "Hello my name is"
+ inputs = tokenizer(text, return_tensors="pt").to(0)

outputs = model.generate(**inputs, max_new_tokens=20)
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```
</details>

### Load the model with Flash Attention 2

<details>
<summary> Click to expand </summary>

```diff
+ import torch
from transformers import AutoModelForCausalLM, AutoTokenizer

model_id = "mistralai/Mixtral-8x7B-v0.1"
tokenizer = AutoTokenizer.from_pretrained(model_id)

+ model = AutoModelForCausalLM.from_pretrained(model_id, use_flash_attention_2=True)

text = "Hello my name is"
+ inputs = tokenizer(text, return_tensors="pt").to(0)

outputs = model.generate(**inputs, max_new_tokens=20)
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```
</details>

## Notice
Mixtral-8x7B is a pretrained base model and therefore does not have any moderation mechanisms.

# The Mistral AI Team
Albert Jiang, Alexandre Sablayrolles, Arthur Mensch, Blanche Savary, Chris Bamford, Devendra Singh Chaplot, Diego de las Casas, Emma Bou Hanna, Florian Bressand, Gianna Lengyel, Guillaume Bour, Guillaume Lample, Lélio Renard Lavaud, Louis Ternon, Lucile Saulnier, Marie-Anne Lachaux, Pierre Stock, Teven Le Scao, Théophile Gervet, Thibaut Lavril, Thomas Wang, Timothée Lacroix, William El Sayed.