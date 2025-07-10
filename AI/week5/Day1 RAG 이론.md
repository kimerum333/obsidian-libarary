# Auto-Encoding
- 완전한 입력을 받고 출력하는 모델
- 예시 : 분류, 감정 분석, 벡터 임베딩
# Auto-Regressive
- 불완전한 입력을 받고 출력하는 모델
- 예시 : 일반적인 채팅모델(LLM)
# 벡터 계산
- King - Man + Woman = Queen
# 일반적인 RAG 구조
1. input
2. input 을 벡터화
3. RAG로부터 input 관련 정보를 검색
4. 3의 정보를 프롬프트에 삽입
5. LLM은 4로 만들어진 프롬프트에 기반해 답변