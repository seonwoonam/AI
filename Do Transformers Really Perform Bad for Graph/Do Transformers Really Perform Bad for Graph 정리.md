# Do Transformers Really Perform Bad for Graph 정리

[[Paper Review] Do Transformers Really Perform Bad for Graph Representation? (Graphormer)](https://www.youtube.com/watch?v=G2PoGAyg-1k&t=1376s)

## Introduction

- 일반 transformer 에서도 위치 정보를 넣어주는 positional encoding이 있듯이, 그래프에서도 노드 위치 정보를 넣어줄 필요가 있다.

- Graph network Task
    - Node Classification
        - Node의 label을 예측하는 task
        - X : Node → Y : Node label
        - Large graph 에서 Node 를 기준으로 시행됨. node 가 기준으로
    - Link Prediction
        - **social network 구조**에서 친구 추천같이 missing edge를 예측하는 task
        - X : Node pair → Y : edge
        - Large graph 에서 Node 를 기준으로 시행됨. node 가 기준으로
    - Graph Classification
        - Graph 자체의 class를 분류하는 task
        - 예시) 분자구조의 화학 속성 예측
        - Graph Representation 중요
        - 위의 방법대로 node를 잘 표현하고 합쳐 그래프로 나타낼때 손실이 많이 발생 → 그래프를 잘표현하는 것의 중요성이 높아짐.
        - small graph에서 graph를 기준으로 시행됨.
        - 다수의 그래프가 인풋으로 들어가는 task

## Graphormer

- **Centrality Encoding**
    - centrality : 그래프 내 중심성을 나타내는 지표
    - degree : 얼마나 많이 edge 들이 연결되어 있냐
    - betweenness
    - closeness
    - page rank
    - eigenvalue
    - 그냥 self attention을 통해 학습할 경우 **node 간의 중요도 차이가 있을때 어떤 node 가 중요한지**에 대한 정보를 주지 못해서 centrality encoding 을 하게 됨.
    
    ⇒ 의미적 유사성과 **노드의 중요도** 모두를 고려한 attention
    
- **Spatial Encoding**
    - positional encoding 해주는느낌
        - sequential 데이터 처리 같은
        - (transformer에서는 rnn, cnn을 사용하지 않기때문에 sequential 순서로 데이터를 지나지 않아 positional encoding을 해주었음)
    - 고차원에서 표현되는 노드의 위치 정보 표현
    - Edge를 통해 연결된 정보를 기반으로, 노드 간의 거리를 측정
    
    ⇒ 그래프의 구조적 정보 학습
    
- **Edge Encoding**
    - Edge Embedding 을 통해 노드 간의 상관관계를 좀 더 표현하고자 함
        - ex) 분자구조에서 일반결합, 이중결합 같은 특징의 구조 표현
    - edge에 feature 가 생김
    - sp feature 는 shortest path feature인데 가중치 같은 느낌인것 같다.
    
    ![Untitled](Do%20Transformers%20Really%20Perform%20Bad%20for%20Graph%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%20542183a6c3684659a790000f2898b4fb/Untitled.png)
    

- Special Node
    - **노드들을 다시 그래프로 표현하는 readout function을 사용하지않고 이 논문에서는 Vnode(Virtual Node)라는 것을 사용함.**
    - Vnode
        - 전체 노드와 연결되는 가상의 node 생성
        - 모든 노드에서 정보를 다 연결받기 때문에 그래프를 대표하는 노드가 됨. ⇒ 그래프를 표현하는 representation으로 사용할 수 있음.