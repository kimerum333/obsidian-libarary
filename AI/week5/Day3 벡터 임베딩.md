
# 벡터 임베딩 모델
- word2vec(2013)
- BERT(2018)
- OpenAI Embeddings(2024)

# 벡터 DB: Chroma
- 오래 된 전통의 모델.
- Query, Retrieval
```python
embeddings = OpenAIEmbeddings()

vectorstore = Chroma.from_documents(documents=chunks, embedding=embeddings, persist_directory=db_name)
```

벡터 DB: FAISS
- 인메모리 벡터 DB
-  
# Libaray
## TSNE
- 차원축소, 시각화
## plotly
- 파이썬 범용 그래프 라이브러리


