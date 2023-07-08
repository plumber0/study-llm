- Introduction  
  - LLM app을 만드는데 사용하는 framework
  - 관련 필드에서 app을 만드는데 common abstraction을 보았고 이를 LangChain으로 구현
  - 관련 필드에서 빠르게 adopt되어 사용되어 지고 있음
  - python, js(ts) 패키지 존재
  - combine components

- Models, Prompts and Parsers
  - models : type of llm
  - prompts : input 전에 처리과정
    - prompt templates are a useful abstraction to help you reuse good prompts when you can
    - LangChain provides prompts for some common operations, such as summarization, question answering, connecting to SQL databases, connecting APIS
  - parsers : output 후에 처리과정
    - often instruct the LLM to generate its output in a certain format, this can be coupled with a parser to extract out the text 

- Memory
  - LLM are `stateless`, each transaction is independent
  - chatbots appeart to have memory by providing the full conversation as `context`
  - LangChain provides several kinds of `memory` to store and accumulate the conversation
  - ConversationBufferMemory
    - This memory allows for storing of messages and then extracts the messages in a variable.
  - ConversationBufferWindowMemory
    - This memory keeps a list of the interactions of the conversation over time. It only uses the last K iterations.
  - ConversationTokenBufferMemory
    - This memory keeps a buffer of recent interactions in memory, and uses token length rather than number of interactions to determine when to flush interactions.
  - ConversationSummaryMemory
    -This memory creates a summary of the conversation over time.

  - Vector data memory
    - stores text(from conversation or elsewhere) in a vector database and retrieves the most relevant blocks of text
  - Entity memories
    - using an LLM, it remembers details about specific entities

  can use multiple meories at one time
  - conversation memory + Entity memory to recall individuals

  you can also store the conversation in a conventional database(such as SQL)

- Chains in LangChain
  - Building block of LangChain
  - The chain usually combines an LLM, large language model, together with a prompt, and with this building block you can also put a bunch of these building blocks together to carry out a sequence of operations on your text or on your other data. 
  - LLMChain
  - Sequential Chains
    - SimpleSequentialChain
    - SequentialChain
  - RouterChain

- Question and Answer
  - one of most powerful app that can built with llm is answer question on top of document
  - LLM can only inspect a few thousand words at a time
  - Embeddings Vector
    - Embedding vector captures content/meaning
    - Text with similar content will have similar vectors
    - this let us compare pieces of text in the vector space
  - Vector Database
    1. chop it to small chunks from document
    2. create embedding for each of these chunks
    3. store those in a vector database with index
    4. when query comes in first create an embedding for that query
    5. compare all the vectors in the database and pick the most similar

  - stuff method
    - stuffing is the simplest method. you simply stuff all data into the prompt as context to pass to the language model'
      - pros : it makes a single call to the llm. the llm has access to all the data at once
      - cons : llms have a context length, and for large documents or many documents this will not work as it will result in a prompt larger than the context length

     
  - map reduce
  - refine
  - map rerank
