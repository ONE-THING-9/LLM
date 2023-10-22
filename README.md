# LLM

## (video)Large Language Models (in 2023) by Hyung Won Chung

[Video link](https://www.youtube.com/watch?v=dbo3kNKPaUA&t=2287s)

### summary
 - some ability LLm has been achieved after scaling those models in terms of parameters and dataset.

__Perspective of "yet"__ 

<img width="846" alt="Screenshot 2023-10-18 at 8 35 25 PM" src="https://github.com/ONE-THING-9/LLM/assets/123763769/a7f2ed4c-13bc-4c69-bd25-995cc2d60a78">

for LLM, the most capable model serves as an "axiom" for many research experiments run on top , so an idea or experiment may fail because of insufficient "intelligence" (yet perspective maybe like ablility3 first was failed experiment but later get solved once GPT3 came in picture.

__scaling doesn't solve all problems__
- pre-trained models are trained using next-token prediction. so given a prompt model just try to generate something that is a natural continuation of the prompts even if the prompts are malicious.
- here supervised pretraining and RLHF come into the picture.

__instruction finetuning__
- we simply do the next token prediction in the form of <natural institution in terms of question, answer of question>
- -Instruction fine-tuning is highly effective but it has inherent limitations, in instruction we told the model that this question has this correct answer, this is called "behaviour cloning".
- for "2+5", there is one single correct answer but for "Write a poem for Santa", there are many answers to it.
- The objective function of instruction finetuning seems to be the “bottleneck” of teaching these behaviours. The maximum likelihood objective is a “predefined” function (i.e. no learnable parameter). Can we parameterize the objective function and learn it?

__reward model__ 
-  given a generation we want a model that will give us a score of how good that generation is, however, the scaler score can be subjective so to avoid it we use the ranking method, like given two generated texts we will tell which one is better.
- RL training - Once we have a reward model, we can use it in RL to learn the language model parameters that maximize the expected reward.


__reward hacking__ - when the model only focuses on getting a maximum score, for eg if the model sees that large generated are getting high rewards then it gives more preference to larger generated text.

<img width="846" alt="Screenshot 2023-10-18 at 9 14 42 PM" src="https://github.com/ONE-THING-9/LLM/assets/123763769/39fcde2a-71b3-4a70-aed1-34ac6bae5a8b">
in the current scenario, only input and output and loss function are not learnable, so the next-gen model will focus on learnable loss function and RLHF is a step in that direction.



## FlashAttention by Aleksa Gordic
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

     






