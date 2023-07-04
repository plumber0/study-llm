- Introduction  
  - LLM app을 만드는데 사용하는 framework
  - 관련 필드에서 app을 만드는데 common abstraction을 보았고 이를 LangChain으로 구현
  - 관련 필드에서 빠르게 adopt되어 사용되어 지고 있음
  - python, js(ts) 패키지 존재
  - combine components

- Models, Prompts and Parsers
  - models : llm
  - prompts : input 전에 처리과정
  - parsers : output 후에 처리과정


####
- Introduction
  - application often needs multiple internal steps that are invisible to the end-user
  - evaluating and improving a system over time

- Language Models, the Chat Format and Tokens
  - use supervised learning for repeatedly predict the next word
  - two types of LLM
    - Base LLM
      - predicts next word, based on text training data
    - Instruction Tuned LLM
      - tries to follow to instruction
      - getting from a Base LLM to an instruction tuned LLM:
        - Train a Base LLM on a lot of data
        - Further train the model:
          - Fine-tune on examples of where the output follows an input instruction
          - Obtain human-ratings of the quality of different LLM outputs, on criteria such as whether it is helpful, honest and harmless
          - Tune LLM to increase probability that it generates the more highly rated outputs(using RLHF: Reinforcement Learning from Human Feedback)
  - tokens
    - predict next token(sequences of letters) not the word
    - for English input 1 token is around 4 characters, or 3/4 of a word
    - Different models have different limits on the number tokens in the input `context` + output completion
    - gpt3.5-turbo ~4000 tokens

  - system, user and assistant messages
    - system : sets tone/behavior of assistant
    - assistant : LLM response
    - user : prompts
    multi-term conversation, you can also input assistant messages based on things that it had perviously said


  - Prompting is revolutionizing AI application development
    - compare to Supervised learning
    - `Get labeled data` -> `Train model on data` -> `Deployu & call model`
    - `Specify Prompt` -> `Call model`
    - many unstructured data applications text application, vision technology
    - not good for structured data 
