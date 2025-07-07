
# 조건부 컨텍스트 확장
```python
# Fixed a bug in this function brilliantly identified by student Gabor M.!
# I've also improved the structure of this function

def chat(message, history):

    relevant_system_message = system_message
    if 'belt' in message:
        relevant_system_message += " The store does not sell belts; if you are asked for belts, be sure to point out other items on sale."
    
    messages = [{"role": "system", "content": relevant_system_message}] + history + [{"role": "user", "content": message}]

    stream = openai.chat.completions.create(model=MODEL, messages=messages, stream=True)

    response = ""
    for chunk in stream:
        response += chunk.choices[0].delta.content or ''
        yield response
```
- if 'belt' in message: 구문으로 문맥을 즉석에서 확장. 인풋토큰을 min으로 유지하면서, 적절한 제약조건을 그때그때 삽입 가능한 수법이다.