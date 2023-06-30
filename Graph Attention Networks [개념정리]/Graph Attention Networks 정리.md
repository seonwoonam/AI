# Graph Attention Networks 정리

[[DMQA Open Seminar] Graph Attention Networks](https://www.youtube.com/watch?v=NSjpECvEf0Y&t=4151s)

### Graph Neural Networks

- Node-Edge로 구성된 그래프 데이터의 구조를 학습하는 딥러닝 모델

### Graph Attention Networks

- graph neural networks + attention
- 그래프 데이터의 구조를 학습하는 딥러닝을 할때 중요 node에 가중치를 부여하는 어텐션 메커니즘을 사용하는 모델.

### Seq2seq

- Encoder : RNN → Context vector → Decoder : RNN
    - 문장이 벡터화 된것을 다시 decode 하는 방법.
- 문장이 길어지면 문제(Long term dependency)
    - 몇몇 단어를 벡터화 중 까먹게 됨.

### Seq2seq with Attention

- 초기 attention 컨셉 : 예측해야할 단어에 가중치를 두어 까먹지 않게 하는 컨셉

### Attention

- dictionary 자료 구조
    - query 와 key 가 일치하면 value 를 return
        
![Untitled](https://github.com/seonwoonam/AI/assets/74304338/ec1f9a04-490c-41d4-b5f0-a06b7f2b2072)
        
- dictionary 자료 결과 리턴 과정
    1. 유사도 확인 과정
    2. 유사도와 value 곱하는 과정
    3. 최종 결과 리턴하는 과정(유사도와 value를 곱한 값의 합을 리턴)
        
![Untitled 1](https://github.com/seonwoonam/AI/assets/74304338/9f6c2bca-e944-495e-91ad-7ea6d305d4d0)
        

- dictionary 자료가 결과를 리턴하는 과정이 attention에서 feature 생성하는 과정과 유사.

![Untitled 2](https://github.com/seonwoonam/AI/assets/74304338/1b8f93c2-4ab8-4d26-b637-b7b9afc94dee)

- Attention : Query와 key의 유사도를 계산한 후 value의 가중합을 계산하는 과정, 위에서 하나만 만들어진 context vector가 여러개 만들어지는 듯한 느낌
- Attention score : value에 곱해지는 가중치
- attention이 적용된 서로다른 context vector를 갖게됨

- similarity function(alignment model)
    - vector 간 유사도를 계산하는 다양한 방법을 similarity function으로 사용가능.

### self attention

- RNN,CNN 구조를 사용하지 않고 attention 만을 사용해서 feature representation
- key = query = value
- scale dot product attention
    
![Untitled 3](https://github.com/seonwoonam/AI/assets/74304338/e7558219-2d85-419b-a676-f5f5c18994bd)
    

![Untitled 4](https://github.com/seonwoonam/AI/assets/74304338/fc99b61c-bbde-4cac-b546-c74adfc983d9)

- Multi-head attention
    - scale to product attention 을 여러번 하겠다.
    
![Untitled 5](https://github.com/seonwoonam/AI/assets/74304338/749d866a-432a-4416-b80f-30b3f2a91904)

    

- transformer의 기반.

### GNN

1. Aggregate / Message passing
    - 타켓 노드의 이웃 노드들의 k 시점의 hidden state 결합
2. combine / update
    - k-1 시점의 target node와 위에서 만든 aggregate information을 사용하여 k 시점의 target node 계산.
3. readout
    - 만들어진 target node 들을 하나의 graph로 생성하는 과정

- GNN Variants
    - Aggregate 함수와 combine 함수의 정의에 따라 다양한 GNN 변형 가능.

### Gated Graph Neural Network

- 층을 깊게 쌓으면 overfit에 빠질 수 있고, vanishing gradient 문제 발생 가능
- Combine 하는 과정에서 GRU cell 에 넣어서 combine 시키는 과정.

### Graph Attention Network

- Aggregate
    - 타켓 노드와 이웃 노드를 포함한 hidden embedding 에 대해서 attention 수행.
    - 아래 과정을 같은 key 와 query에서도 하지만 인접 노드도 가서 한다
    
![Untitled 6](https://github.com/seonwoonam/AI/assets/74304338/263b88c1-88ce-4246-b0da-f9d08f5b8753)
    
![Untitled 7](https://github.com/seonwoonam/AI/assets/74304338/79d22e52-77da-431e-a341-4bcaa72a3434)

    
    - e11 : 1번 타겟 노드를 학습 시킬 때 자기자신에서 얼마나 정보를 가져올지
    - e12 : 1번 타켓 노드를 학습 시킬 때 2번 노드에서 얼마나 정보를 가져올지
    
    - masked attention
        - 일단 e 값을 연결 안되어있는 노드도 다 계산
        - 그 후 인접 노드를 이용하여 마스킹 시킴.

- Combine
    - 위에서 구한 값 바탕으로 새로운 target node feature 업데이트
    
![Untitled 8](https://github.com/seonwoonam/AI/assets/74304338/7222063d-25ec-4b2e-9cde-3f54833f27d0)

    
    - 각각의 모든 node 를 업데이트 하면 업데이트 된 graph 생성됨.
