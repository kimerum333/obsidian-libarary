# 핵심 추상 래퍼 3계층
- LLM : LLM
- Retriever : RAG
- Memory : History Context
```python
llm = ChatOpenAI(temperature=0.7)

memory = ConversationBufferMemory(memory_key='chat_history', return_messages=True)

retriever = vectorstore.as_retriever()

conversation_chain = ConversationalRetrievalChain.from_llm(llm=llm,retriever=retriever, memory=memory)
```

