[blog link](https://gordicaleksa.medium.com/eli5-flash-attention-5c44017022ad)

### summary
![image](https://github.com/ONE-THING-9/LLM/assets/123763769/9269e103-f60d-4570-855f-a2f685a107ef)

- most of the research and methods focused on reducing FLOPS and ignoring the overhead of memory access.
- over the years GPUs have been adding compute capacity(FLOPS) at a faster pace than increasing the memory throughput.
- Depending on this ratio between computation and memory accesses, operations can be classified as either:
  
 •	 __compute-bound__ (example: matrix multiplication)
 
 •	__memory-bound__ (examples: elementwise ops (activation, dropout, masking), reduction ops (softmax, layer norm, sum, etc.)…)
- it turns out that attention is memory-bound with current hardware because as compared to matmul it has more elementwise ops.
  ![image](https://github.com/ONE-THING-9/LLM/assets/123763769/0b44e11f-3f53-4be7-b8ba-540feef20169)

- memory is hierarchical so memory overhead and access cost change according to memory level.
  ![image](https://github.com/ONE-THING-9/LLM/assets/123763769/86f9e2d0-0d96-4cef-bb7e-c87c25396fd1)

- how can we make this memory access more efficient
- remove redundant HBM read and write, write into it after doing all steps(kernel fusion)
  ![image](https://github.com/ONE-THING-9/LLM/assets/123763769/8e107c27-057d-4f7a-b0cb-fb6a438ba9dd)
  
- but Softmax couples all of the score columns together. To compute how much a particular i-th token from the input sequence pays attention to other tokens in the sequence you’d need to have all of those scores readily available (denoted here by z_j) in SRAM. But let me remind you: SRAM is severely limited in its capacity. You can’t just load the whole thing. N (sequence length) can be 1000 or even 100.000 tokens. So N² explodes fairly quickly
  
![image](https://github.com/ONE-THING-9/LLM/assets/123763769/33a6325e-0493-40ba-8366-105383d668c1)
