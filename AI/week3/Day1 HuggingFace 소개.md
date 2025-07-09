# HuggingFace 생태계 정리

---

## HuggingFace Website

### Models
- 다양한 사전학습 모델을 공유하는 공간
- 예: GPT2, BERT, T5, LLaMA, Falcon 등

### Datasets
- 자연어처리, 음성, 이미지 등 다양한 공개 데이터셋 저장소
- `load_dataset()`으로 바로 활용 가능

### Spaces
- 실제로 배포 가능한 클라우드 호스팅 공간
- 대부분 Gradio 기반 데모이며, Streamlit도 지원
- 예: `https://username.hf.space` 형식의 공개 URL 제공

### Leaderboards
- 다양한 벤치마크 데이터셋 기반 성능 평가 제공
- 대표 지표: MMLU, ARC, HellaSwag, TruthfulQA 등
- 오픈 LLM 모델 성능 비교 가능

---

## HuggingFace Python 라이브러리

### Hub
- 모델과 데이터셋을 공유하거나 다운로드하는 API
- `from_pretrained()`, `push_to_hub()` 등 HuggingFace 웹과 연동

### datasets
- 다양한 데이터셋 로딩, 전처리를 위한 유틸리티
- `load_dataset()`, `Dataset.map()` 등 제공
- CSV, JSON, parquet 등 포맷 지원

### transformers
- 사전학습 언어모델 실행용 코드
- PyTorch 또는 TensorFlow 기반 모델을 래핑
- 토크나이저, 생성, 분류, 파인튜닝 등 대부분 작업 가능

```python
from transformers import AutoModelForCausalLM, AutoTokenizer

model = AutoModelForCausalLM.from_pretrained("gpt2")
tokenizer = AutoTokenizer.from_pretrained("gpt2")
```

### PEFT (Parameter Efficient Fine Tuning)
- 전체 모델을 학습하지 않고 일부 파라미터만 학습하는 방법
- 메모리 효율적이며 빠른 파인튜닝 가능
- 대표 기법: LoRA, Prefix Tuning, Prompt Tuning

```python
from peft import get_peft_model, LoraConfig
```

### TRL (Transformer Reinforcement Learning)
- RLHF (Reinforcement Learning from Human Feedback)를 위한 라이브러리
- SFT → Reward Modeling → PPO 튜닝 구조로 구성
- PPO, DPO 등의 강화학습 기법을 이용해 모델 응답을 사용자 선호에 맞게 튜닝

```python
from trl import PPOTrainer
```

### Accelerate
- 분산 환경(GPU/TPU 등)에서 모델 실행을 단순화하는 도구
- DeepSpeed, FSDP, mixed precision(fp16/bf16) 지원
- 복잡한 분산 설정 없이 실행 가능

```bash
accelerate launch train.py
```

---

## HuggingFace 전체 흐름 요약

모델을 찾고 (Hub)  
데이터를 불러오고 (datasets)  
실행하거나 튜닝하고 (transformers, peft, trl, accelerate)  
데모를 배포하고 (Spaces)  
성능을 평가한다 (Leaderboards)
