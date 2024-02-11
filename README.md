Modified current GPT model to to incorporate two of the key ingredients found in state-of-the-art large language models (LLMs), such as LLAMA-2.

The two things modified are as follows:
1) Rotary Posiiton Embeddings (RoPE)- replace the existing absolute position embeddings with a relative position embedding that rotates small segments of each key and query vector.
2) Grouped Query Attention (GQA)- it enables the model to use less memory and run faster

**Dataset:**
The dataset used for this is a collection of the complete works of Shakespeare. The dataset file is input.txt, and is around 1.1MB in size.
