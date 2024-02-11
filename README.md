Modified current GPT model to to incorporate two of the key ingredients found in state-of-the-art large language models (LLMs), such as LLAMA-2.

The two things modified are as follows:
1) Rotary Posiiton Embeddings (RoPE)- replaces the existing absolute position embeddings with a relative position embedding that rotates small segments of each key and query vector. [Su et al. 2021](https://arxiv.org/pdf/2104.09864.pdf)
2) Grouped Query Attention (GQA)- it enables the model to use less memory and run faster [Ainslie et al. 2023](https://arxiv.org/pdf/2305.13245.pdf)

**Dataset:**
The dataset used for this is a collection of the complete works of Shakespeare. The dataset file is input.txt, and is around 1.1MB in size.

**Files Description:**
1) requirements.txt: A list of packages that need to be installed - torch and einops.
2) input.txt: The dataset—the works of Shakespeare.
3) chargpt.py: Main file. It can be run with the command "_python chargpt.py_". Append flags to this command to adjust the transformer configuration.
4) mingpt/model.py: This file contains the construction of the GPT model. Contains vanilla transformer, GQA and RoPE.
5) mingpt/trainer.py: Code for the training loop of the transformer.
6) mingpt/utils.py: Helper functions for saving logs and configs.

**Flags:**
| Configuration Parameters  | Example Flag Usage |
| ------------- | ------------- |
| Model sequence length  | --data.block_size=128 ( model.block_size is autoset based on this flag)  |
| Directory where model is stored  | --system.work_dir=out/new_chargpt  |
|Number of query heads(hyperparameter for GQA) |--model.n_query_head=6|
| Number of key-value heads (hyperparameter for GQA)  | --model.n_kv_head=3 (n_query_head must be divisible by n_kv_head) (For standard multi-head attention n_query_head = n_kv_head)  |
| Directory from which to load a model trained in a previous run  | --model.pretrained_folder=out/chargpt/pretrained  |
| Whether to enable RoPE embeddings  | --model.rope=True  |
| Number of iterations to train the model  | --trainer.max_iters=200   |
| Device type (useful for debugging), one of| --trainer.device=cpu |

**Results:**

![4_1](https://github.com/vigkneshvr/RoPE-and-GQA-addition-to-MinGPT/assets/48051034/fc1e7437-63e4-4112-98d1-222f6bef7d36)

![4_5](https://github.com/vigkneshvr/RoPE-and-GQA-addition-to-MinGPT/assets/48051034/0b554cc6-de6c-46a6-bf67-d0879ee60bd4)

![4_6](https://github.com/vigkneshvr/RoPE-and-GQA-addition-to-MinGPT/assets/48051034/01501801-5dd7-430b-b2e2-a91845075388)

![4_7](https://github.com/vigkneshvr/RoPE-and-GQA-addition-to-MinGPT/assets/48051034/f8d2c495-40d3-4285-a58a-a689f8e5506f)


**References:**
1) the official GPT-2 TensorFlow implementation released by OpenAI: [](https://github.com/openai/gpt-2/blob/master/src/model.py)
2) huggingface/transformers PyTorch implementation: [](https://github.com/huggingface/transformers/blob/main/src/transformers/models/gpt2/modeling_gpt2.py)
