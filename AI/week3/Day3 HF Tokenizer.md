# Tokenizer

## 역할
- 자연어 텍스트를 **모델이 이해할 수 있는 토큰 단위로 분해하거나 재조립**하는 도구
- LLM의 입력/출력 전처리와 후처리에 반드시 사용됨

## 주요 기능

### Encode
- 텍스트 → 토큰 ID (숫자 리스트)로 변환
- 예: `"hello"` → `[15496]` (GPT-2 기준)
```python
tokenizer = AutoTokenizer.from_pretrained('meta-llama/Meta-Llama-3.1-8B', trust_remote_code=True)

text = "I am excited to show Tokenizers in action to my LLM engineers"
tokens = tokenizer.encode(text)
print(tokens)

```

### Decode
- 토큰 ID → 텍스트로 복원
- 예: `[15496]` → `"hello"`
```python
tokenizer.decode(tokens)
# <|begin_of_text|>
# 128000 번 토큰. 이 토큰은 프롬프트 텍스트의 시작을 나타낸다. 헥스값에서의 0x 과 비슷한 역할. 물론 이건 트레이닝 과정에서 사용된 것.(이건 라마의 경우)

tokenizer.batch_decode(tokens)
# 원본 문자열을 토큰화한 배열로 복원
```

---

## Vocab (어휘 사전)
- 토큰화는 **전체 단어가 아니라, 단어 조각(subword)**을 단위로 나누는 방식이 일반적
- 이를 통해 어미/어간, 희귀어 등을 효과적으로 처리할 수 있음
```python
tokenizer.vocab
# 용어 사전. 등록된 모든 어휘사전을 단어 : 숫자ID 형태로 출력.

tokenizer.get_added_vocab()
# <|begin_of_text|> 등의 특수 어휘 사전을 단어: 숫자ID 의 형태로 출력.(이건 라마의 경우)

```

### Fragments of Characters
- 예: `"running"` → `["run", "ning"]`  
- BPE(Byte Pair Encoding)나 SentencePiece 등의 알고리즘 기반
- 결과적으로 **단어를 구성하는 어간(語幹)** 중심의 토큰이 생성됨

---

## 모델 종속성

- **토크나이저는 모델에 종속적으로 학습된 도구**임  
  → 각 모델은 자신에게 최적화된 vocab과 토큰화 전략을 기반으로 훈련됨
- 따라서, 각 모델에 맞는 토크나이저를 자동으로 가져오는 방법도 있다.
```python
tokenizer = AutoTokenizer.from_pretrained('meta-llama/Meta-3.1-8B-Instruct', trust_remote_code=True)

prompt = tokenizer.apply_chat_template(messages, tokenize=False, add_generation_prompt=True)
```

### 따라서:
- `gpt2` 모델에는 `gpt2`용 토크나이저를,
- `bert-base-uncased`에는 `bert-base-uncased`용 토크나이저를 사용해야 가장 정확한 결과를 얻을 수 있음

> 물론 다른 토크나이저를 억지로 써도 동작은 하지만,  
> 학습 시 사용한 토큰 분할 방식과 달라져서 성능이나 일관성이 깨질 수 있음

---

## 실전 예시 (transformers 기준)

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("bert-base-uncased")

text = "Transformers are powerful."
tokens = tokenizer.encode(text)
decoded = tokenizer.decode(tokens)

print("Tokens:", tok
