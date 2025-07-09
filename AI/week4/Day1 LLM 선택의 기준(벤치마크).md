# 모델을 어떻게 비교하는가?
## 1. 기본 스펙 비교
### 체급
- 오픈소스 / 클로즈 소스
- 출시일 / 지식의 컷오프일
- 파라미터의 개수 : 모델의 체급
- Training tokens
- Context length (Size of Context Window)
### 가격
- 추론 비용(API, 구독 비용, 컴퓨팅 파워 비용)
- 훈련 비용(특히, 프론티어 모델에 파인 튜닝을 고려한다면)
- 빌드 비용(로컬 오픈소스모델을 훈련한다면)
- Time to market (신뢰성, 가용성) 
- rate limits(시간 당 호출 횟수 제한, 시간당 처리 토큰량 제한)
- speed
- latency
- lincense(약관에 사인해야 할 수도 있다.)
## 2. 결과 비교
- 벤치마크 확인
- HF 리더보드
- Arena