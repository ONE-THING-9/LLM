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
