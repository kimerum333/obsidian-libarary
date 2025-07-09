# Chunking(Langchain)
```python
text_splitter = CharacterTextSplitter(chunk_size = 1000, chunk_overlap=200)

chunks = text_splitter.split_documents(documents)

```
## Chunk 의 메타데이터 구성요소
- Source : 파일 출처
- Doc_type: 임의 설정 태그