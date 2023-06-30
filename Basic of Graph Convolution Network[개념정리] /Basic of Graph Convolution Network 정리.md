# Basic of Graph Convolution Network 정리

[[#30.Lec] Basic of Graph Convolution Network - 딥러닝 홀로서기](https://www.youtube.com/watch?v=YL1jGgcY78U&t=1420s)

### What is Graph?

- 예시
    - 페이스북 소셜 그래프
    - 3D Mesh
    - Molecular Graph(분자 그래프)
- 그래프란
    - vertices(node) 와 edge로 이루어진 것
    - vertices와 그 사이 edge로 이루어진 형태. edge가 vertices 사이에 없을 수도 있다.
    - edge에 방향이 있을 수도 있다.
    - edge에 값이 있을 수 있다. ⇒ weighted graph
- 딥러닝을 위해서 표현
    - Node Feature Matrix
        - 각각의 node에 담긴 정보들을 나타내는 matrix
        - n은 노드의 개수라고 할때 nxf(feature의 개수) matrix를 갖게됨.
    - Adjacency Matrix
        - node간의 connectivity를 나타내는 matrix(edge를 나타내는 matrix)
        - 노드가 n개 있으면 nxn matrix가 됨.
        - 의미를 추가하고 싶으면 0과 1말고 다른 값을 사용할 수도 있음.
        

### Graph Convolution Network

- 그래프 형태의 데이터에 대해서 정보를 뽑아내는 네트워크
- Convolution 연산
    - 어떤 이미지를 필터로 덮어 씌우고, 슬라이딩 시켜 연산시켜 다음 텐서를 만드는 연산
    - weight sharing을 하여 파라미터 줄여주는 장점
- output은 무엇이 될까?
    - 그래프가 나타내는 상태, 정보가 뭔지
- graph convolution layer를 거치면 node feature 에 담긴 값이 업데이트가 되어야함.
    - 각각의 노드의 정보 업데이트
- hidden state : 각 layer를 거친 node feature matrix

- 계산 방법
    - 다음 H1의 값은 주변 값들도 더해진 값
    - 같은 weight 값을 곱합
      
![Untitled](https://github.com/seonwoonam/AI/assets/74304338/93648919-6043-413f-a9cc-83f2330fe611)

- 어떻게 구현할까
    - 그냥 for문 돌려서 하면 너무 cost가 높다
    - Adjacency matrix 를 이용해서 연산을 하면 되겠다
    - 아래와 같은 행렬 연산

![Untitled](Basic%20of%20Graph%20Convolution%20Network%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%2029227e42741d48a396b9bec2d1e1ed19/Untitled%201.png)

- Adjacency matrix를 행으로 feature matrix를 열로 곱해서 인접되어있는 node 끼리에만 가중치가 업데이트 되게 연산

![Untitled](Basic%20of%20Graph%20Convolution%20Network%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%2029227e42741d48a396b9bec2d1e1ed19/Untitled%202.png)

- Readout
    - 아래 그림 처럼 그래프의 모양이 완전히 같지만 어떻게 matrix에 입력 하느냐에 따라 바뀔 수 있음
    - 결국 같은 그래프니까 뽑아냈을때 같은 값을 뽑아내야함.
    - 아래식 처럼 적용하면 수학적으로 permutation 해소 가능.

![Untitled](Basic%20of%20Graph%20Convolution%20Network%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%2029227e42741d48a396b9bec2d1e1ed19/Untitled%203.png)

- 전체적인 구조

![Untitled](Basic%20of%20Graph%20Convolution%20Network%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%2029227e42741d48a396b9bec2d1e1ed19/Untitled%204.png)

- 참고
    - Regression ⇒ 손실함수 : MLE
    - Classification ⇒ 손실함수 : Cross-Entropy

### Advanced technique of GCN

- Inception 적용
    - adjancecy를 한번 더 곱하기

![Untitled](Basic%20of%20Graph%20Convolution%20Network%20%E1%84%8C%E1%85%A5%E1%86%BC%E1%84%85%E1%85%B5%2029227e42741d48a396b9bec2d1e1ed19/Untitled%205.png)

- Skip Connection
    - Gated Skip Connection
    
- Attention
    - 노드의 정보를 업데이트 할 때 인접한 것을 다 똑같은 비율로 하지 않고, 중요도에 따라 적절한 비율로 학습해서 곱하기.
