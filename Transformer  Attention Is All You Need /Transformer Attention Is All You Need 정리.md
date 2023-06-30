# Transformer : Attention Is All You Need 정리

[[딥러닝 기계 번역] Transformer: Attention Is All You Need (꼼꼼한 딥러닝 논문 리뷰와 코드 실습)](https://www.youtube.com/watch?v=AA621UofTUA)

## Transformer (Attention Is All You Need)

- Seq2Seq 모델에 병목 현상이 발생하여 성능하락으로 인해 Transformer 개발

### Seq2Seq with Attention

![Untitled](https://github.com/seonwoonam/AI/assets/74304338/7f5ad615-b638-40fe-85e6-87c8c4ebcbc2)


- 에너지 : 소스 문장에서 나왔던 모든 출력값들 중에서 어떤 값과 가장 연관성이 있는지 구하기 위해서 그 수치를 구한 것
- 가중치 : 에너지 값들을 softmax를 사용해서 확률화 한 것

![Untitled 1](https://github.com/seonwoonam/AI/assets/74304338/191b8be3-9b24-4493-9960-63e36fce4a84)

### Transformer

- Attention 기법만 사용
- RNN 과 CNN 사용하지 않음

![Untitled 2](https://github.com/seonwoonam/AI/assets/74304338/09522aa5-e451-4e32-90c3-3df70301bc6e)

- 전통적인 입력 값 임베딩

![Untitled 3](https://github.com/seonwoonam/AI/assets/74304338/23c92e4d-d344-4b47-be95-96a4229b0067)

- RNN(seq2seq 방법 종류)을 사용하지 않으려면 위치 정보를 포함하고 있는 임베딩 사용해야함 ⇒ 트랜스포머에서는 Positional Encoding 사용

![Untitled 4](https://github.com/seonwoonam/AI/assets/74304338/f626fb38-f2c0-4d23-830a-5d1df5dd8956)

- 임베딩이 끝난 후에 self-attention 진행
    - 각각의 단어가 서로에게 어떤 연관성을 갖고 있는지 알기 위해 진행
    - 각각의 attention score 구함
    - 추가 + 잔여학습(Residual Learning)
        - 특정 레이어 건너뛰는 기술

- 인코더와 디코더

![Untitled 5](https://github.com/seonwoonam/AI/assets/74304338/4e78d83e-7a1b-4974-baf6-02bf4f5bedb3)

![Untitled 6](https://github.com/seonwoonam/AI/assets/74304338/164e73f1-7146-4759-a801-7b5e7f4743af)

- Multi-Head Attention

![Untitled 7](https://github.com/seonwoonam/AI/assets/74304338/7fb0e542-1292-45db-950a-4e34be9ea207)


- Scaled Dot - Product Attention
    - s는 softmax

![Untitled 8](https://github.com/seonwoonam/AI/assets/74304338/cf4d524e-c9ae-4a10-9797-9195a4209792)

- 행렬로 한번에 계산하는 scaled dot - product attention
    - graph 때랑 똑같은 느낌
    - 각각의 단어가 서로에게 얼마나 영향을 미치는지에 대한 attention energy가 나오게 된다.
    - Attention은 query, key, value와 같은 차원을 같게 됨.

![Untitled 9](https://github.com/seonwoonam/AI/assets/74304338/555c2c0b-67dd-4a7e-b03e-cedfa3bd24d0)

- 행렬 Multi-Head Attention
    - 인풋의 전체 차원에서 head 의 개수만큼 나누어 query, key, value의 차원을 결정해주었기 때문에 attention을 계산해 나온 head 들을 쭉 이어붙이면 원래 인풋의 차원이 된다.


![Untitled 10](https://github.com/seonwoonam/AI/assets/74304338/97ea9ce5-9c03-46a7-a198-17c61c50caef)
