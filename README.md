Modified current GPT model to to incorporate two of the key ingredients found in state-of-the-art large language models (LLMs), such as LLAMA-2.

The two things modified are as follows:
1) Rotary Posiiton Embeddings (RoPE)- replace the existing absolute position embeddings with a relative position embedding that rotates small segments of each key and query vector.
2) Grouped Query Attention (GQA)- it enables the model to use less memory and run faster

**Dataset:**
The dataset used for this is a collection of the complete works of Shakespeare. The dataset file is input.txt, and is around 1.1MB in size.

**Flags:**
| Configuration Parameters  | Example Flag Usage |
| ------------- | ------------- |
| Model sequence length  | --data.block_size=128 ( model.block_size is autoset based on this flag)  |
| Directory where model is stored  | --system.work_dir=out/new_chargpt  |
|Number of query heads(hyperparameter for GQA) |--model.n_query_head=6|
| Number of key-value heads (hyperparameter for GQA)  | --model.n_kv_head=3 (n_query_head must be divisible by n_kv_head) (For standard multi-head attention n_query_head = n_kv_head)t  |
| Directory from which to load a model trained in a previous run  | --model.pretrained_folder=out/chargpt/pretrained  |
| Whether to enable RoPE embeddings  | --model.rope=True  |
| Number of iterations to train the model  | --trainer.max_iters=200   |
| Device type (useful for debugging), one of| --trainer.device=cpu |


