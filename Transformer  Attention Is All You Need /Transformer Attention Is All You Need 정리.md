# Transformer : Attention Is All You Need 정리

[[딥러닝 기계 번역] Transformer: Attention Is All You Need (꼼꼼한 딥러닝 논문 리뷰와 코드 실습)](https://www.youtube.com/watch?v=AA621UofTUA)

## Transformer (Attention Is All You Need)

- Seq2Seq 모델에 병목 현상이 발생하여 성능하락으로 인해 Transformer 개발

### Seq2Seq with Attention

![Untitled](Transformer%20Attention%20Is%20All%20You%20Need%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%2094a42c60bb694693bfcba7cc7540497d/Untitled.png)

- 에너지 : 소스 문장에서 나왔던 모든 출력값들 중에서 어떤 값과 가장 연관성이 있는지 구하기 위해서 그 수치를 구한 것
- 가중치 : 에너지 값들을 softmax를 사용해서 확률화 한 것

![Untitled](Transformer%20Attention%20Is%20All%20You%20Need%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%2094a42c60bb694693bfcba7cc7540497d/Untitled%201.png)

### Transformer

- Attention 기법만 사용
- RNN 과 CNN 사용하지 않음

![Untitled](Transformer%20Attention%20Is%20All%20You%20Need%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%2094a42c60bb694693bfcba7cc7540497d/Untitled%202.png)

- 전통적인 입력 값 임베딩

![Untitled](Transformer%20Attention%20Is%20All%20You%20Need%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%2094a42c60bb694693bfcba7cc7540497d/Untitled%203.png)

- RNN(seq2seq 방법 종류)을 사용하지 않으려면 위치 정보를 포함하고 있는 임베딩 사용해야함 ⇒ 트랜스포머에서는 Positional Encoding 사용

![Untitled](Transformer%20Attention%20Is%20All%20You%20Need%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%2094a42c60bb694693bfcba7cc7540497d/Untitled%204.png)

- 임베딩이 끝난 후에 self-attention 진행
    - 각각의 단어가 서로에게 어떤 연관성을 갖고 있는지 알기 위해 진행
    - 각각의 attention score 구함
    - 추가 + 잔여학습(Residual Learning)
        - 특정 레이어 건너뛰는 기술

- 인코더와 디코더

![Untitled](Transformer%20Attention%20Is%20All%20You%20Need%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%2094a42c60bb694693bfcba7cc7540497d/Untitled%205.png)

![Untitled](Transformer%20Attention%20Is%20All%20You%20Need%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%2094a42c60bb694693bfcba7cc7540497d/Untitled%206.png)

- Multi-Head Attention

![Untitled](Transformer%20Attention%20Is%20All%20You%20Need%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%2094a42c60bb694693bfcba7cc7540497d/Untitled%207.png)

- Scaled Dot - Product Attention
    - s는 softmax

![Untitled](Transformer%20Attention%20Is%20All%20You%20Need%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%2094a42c60bb694693bfcba7cc7540497d/Untitled%208.png)

- 행렬로 한번에 계산하는 scaled dot - product attention
    - graph 때랑 똑같은 느낌
    - 각각의 단어가 서로에게 얼마나 영향을 미치는지에 대한 attention energy가 나오게 된다.
    - Attention은 query, key, value와 같은 차원을 같게 됨.

![Untitled](Transformer%20Attention%20Is%20All%20You%20Need%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%2094a42c60bb694693bfcba7cc7540497d/Untitled%209.png)

- 행렬 Multi-Head Attention
    - 인풋의 전체 차원에서 head 의 개수만큼 나누어 query, key, value의 차원을 결정해주었기 때문에 attention을 계산해 나온 head 들을 쭉 이어붙이면 원래 인풋의 차원이 된다.

![Untitled](Transformer%20Attention%20Is%20All%20You%20Need%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%2094a42c60bb694693bfcba7cc7540497d/Untitled%2010.png)