# Quickstart

ContextCrunch also has an integration with [LangChain](https://www.langchain.com/)

## Prerequisites

1. Install this package with `pip install contextcrunch-langchain`.
2. Add your [ContextCrunch](https://contextcrunch.com) API key in your environment file, such as `CONTEXTCRUNCH_API_KEY="aaa-bbb-ccc-ddd"`

## RAG
You can easily modify an existing RAG pipeline by simply applying a `ContextCruncher()` to the context before filling the prompt template.

For example, if you are using [this example](https://python.langchain.com/docs/use_cases/question_answering/quickstart#preview) from the LangChain docs, the modified pipeline becomes:
```python
rag_chain = (
    {"context": retriever | format_docs, "question": RunnablePassthrough()}
    | ContextCruncher(compression_ratio=0.95)
    | prompt
    | llm
    | StrOutputParser()
)
```

## Conversations

You can use `ConversationCruncher()` to compress a long message history.

Here is an example using ConversationBufferMemory, which is a LangChain memory module that stores the entire conversation history.

```python
model = ChatOpenAI()
prompt = ChatPromptTemplate.from_messages(
    [
        ("system", "Conversation Summary:\n{history}"),
        ("human", "{input}"),
    ]
)
memory = ConversationBufferMemory()
memory.chat_memory.add_user_message("My favourite color is purple, my favourite food is pizza.")
memory.chat_memory.add_ai_message("I understand. Your favourite color is purple, and your favourite food is pizza.")

chain = (
    {'history': RunnableLambda(memory.load_memory_variables) | itemgetter("history"), 'input': RunnablePassthrough()} # Fetch the history, feed the input to the next step
    | ConversationCruncher() # history and input is compressed, and fed into the prompt template (which takes 'history' and 'input' as inputs).
    | prompt
    | model
)
chain.invoke("What is favourite color?") # small contexts won't get compressed, so ConversationCruncher() will act as a passthrough.
```
