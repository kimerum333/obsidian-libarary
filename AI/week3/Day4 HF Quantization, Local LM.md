# Quantization
- 양자화.
- 모델을 경량화하는 것. 모델의 weight 를 줄인다. 정밀도precision 를 줄인다.
- 매개변수를... 32비트에서 4비트로 압축해 줄이는 것과 같다. 보통 손실이 많아서 하면 안 되는 일이겠지만, LLM에서는 그리 큰 차이가 없다.
- 메모리도 줄이고, 실행도 빠르게 한다.
- 훈련을 하기 위해서는 필수일 것이다.
- Q-LoRA
## BitsAndBytesConfig
- 양자화를 실행하기 위한 라이브러리
```python
quant_config = BitsAndBytesConfig(
	# 4비트로 압축한다.(압축도 영향 大)
	load_in_4bit = True,
	# 압축 프로세스를 2번 실행(압축도 영향 中)
	bnb_4bit_use_double_quant=True,

	# bfloat16 라이브러리 이용해서 계산함(압축도 영향 小)
	bnb_4bit_compute_dtype=torch.bfloat16,
	# 4비트 넘버를 어떻게 표현할것인가?(압축도 영향  小)
	bnb_4bit_quant_type="nf4" 
)
```

# 양자화된 Model 생성

```python
model = AutoModelFroCasualLM.from_pretrained(LLMA,device_map="auto",quantization_config=quant_config)
# device_map = 만약 GPU 있으면 쓰고싶다 같은 느낌
```

# Wrapping up
```python
# Wrapping everything in a function - and adding Streaming and generation prompts

  

def generate(model, messages):

  tokenizer = AutoTokenizer.from_pretrained(model)

  tokenizer.pad_token = tokenizer.eos_token

  inputs = tokenizer.apply_chat_template(messages, return_tensors="pt", add_generation_prompt=True).to("cuda")

  streamer = TextStreamer(tokenizer)

  model = AutoModelForCausalLM.from_pretrained(model, device_map="auto", quantization_config=quant_config)

  outputs = model.generate(inputs, max_new_tokens=80, streamer=streamer)

  del model, inputs, tokenizer, outputs, streamer

  gc.collect()

  torch.cuda.empty_cache()
```