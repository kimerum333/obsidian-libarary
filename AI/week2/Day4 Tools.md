# Tools?
- 모델로 하여금 외부 기능을 사용할 수 있도록 하는 것.
- 일반적으로 프론티어 모델에 붙인다.
## 대표적인 예시
 - 계산기를 붙여줄 수 있다!

## 어떻게 동작하는가?
### LLM이 사용할 수 있는 함수를 정의한다.
- 입력은 무엇?
- 출력은 무엇?
- LLM은 이것을 언제 사용해야 하는가?
###  보통 언제 쓰는가?
- 데이터를 읽어온다 (DB, 웹 등)
- 외부에 뭔가 액션을 취한다(회의를 예약하기 등)
- 정확한 계산을 한다(계산기 기능이나, 코드 처리기)
- UI를 변경한다(리렌더링을 스스로 처리)

#### 하지만...
- 외부에 액션을 취하기 위해서, 또 UI를 변경하기 위해서는 JSON 으로 구조화된 정보를 뽑아와서 프로그램적으로 처리해도 충분하다. 상황에 따라 맞는 전략이 있다.

# Tool의 실제 구성
- 툴로 사용할 파이썬 코드(함수 정의)를 사전에 만든 뒤

```python
# Let's start by making a useful function

ticket_prices = {"london": "$799", "paris": "$899", "tokyo": "$1400", "berlin": "$499"}

def get_ticket_price(destination_city):
    print(f"Tool get_ticket_price called for {destination_city}")
    city = destination_city.lower()
    return ticket_prices.get(city, "Unknown")
```

- AI가 사용할 수 있도록 딕셔너리 형태로 뼈대를 갖춰준다.
```python
# There's a particular dictionary structure that's required to describe our function:

price_function = {
    "name": "get_ticket_price",
    "description": "Get the price of a return ticket to the destination city. Call this whenever you need to know the ticket price, for example when a customer asks 'How much is a ticket to this city'",
    "parameters": {
        "type": "object",
        "properties": {
            "destination_city": {
                "type": "string",
                "description": "The city that the customer wants to travel to",
            },
        },
        "required": ["destination_city"],
        "additionalProperties": False
    }
}
```

- 그리고 LLM에 포함시켜준다.
```python
# And this is included in a list of tools:
# tool 의 리스트를 변수로 잡아준다.
 tools = [{"type": "function", "function": price_function}]

# LLM 인스턴스 정의시에 tools 를 명시
def chat(message, history):
    messages = [{"role": "system", "content": system_message}] + history + [{"role": "user", "content": message}]

# 여기서 툴을 정의
    response = openai.chat.completions.create(model=MODEL, messages=messages, tools=tools)

    if response.choices[0].finish_reason=="tool_calls":
        message = response.choices[0].message
        response, city = handle_tool_call(message)
        messages.append(message)
        messages.append(response)
        response = openai.chat.completions.create(model=MODEL, messages=messages)
    
    return response.choices[0].message.content
```