# 20210420



## Random Forest

- 분류, 회귀분석 등에 사용되는 앙상블 학습방법의 일종

- 일반적으로 결정트리를 이용한 방법의 경우 결과 및 성능의 변동 폭이 크다
  - 계층적 접근방식
    - 에러 확대됨.
- bagging, randomized node optimization과 같은 랜덤화 기술이 결정트리가 가진 단점을 극복하게 함.



- 랜덤성으로 인해 트리들이 서로 조금씩 다른 특성을 갖게 됨.
  - 예측 간 상관관계를 줄임
  - generalization
  - overfitting 방지

### Bagging

- Bootstrap aggregating의 약자.
  - 주어진 훈련데이터에서 중복을 허용하여 원 데이터셋과 같은 크기의 데이터셋을 만들어서(복원 표본추출)
  - base learner들을 Aggregating시키는 방법이다.

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/3/36/%EB%9E%9C%EB%8D%A4%ED%8F%AC%EB%A0%88%EC%8A%A4%ED%8A%B8_%ED%95%99%EC%8A%B5%EA%B3%BC%EC%A0%95_%EB%B0%B0%EA%B9%85.png/1024px-%EB%9E%9C%EB%8D%A4%ED%8F%AC%EB%A0%88%EC%8A%A4%ED%8A%B8_%ED%95%99%EC%8A%B5%EA%B3%BC%EC%A0%95_%EB%B0%B0%EA%B9%85.png)

### 임의 노드 최적화

![img](https://upload.wikimedia.org/wikipedia/commons/8/8b/RF_training_RNO.png)



### 앙상블 모델

![img](https://upload.wikimedia.org/wikipedia/commons/c/c7/Randomforests_ensemble.gif)



포레스트 예측결과 = 모든 트리의 예측결과들의 평균.

### 매개변수

1. 포레스트의 크기 (= 트리의 개수) : 트리가 많을수록 test time ↑ , generalization↑
2. 최대 허용 깊이: 허용깊이가 너무 크면 overfitting, 너무 작으면 underfitting
3. 임의성의 정도와 종류
4. 노드 분할 함수의 선택 등등



참고 : 

https://ko.wikipedia.org/wiki/%EB%9E%9C%EB%8D%A4_%ED%8F%AC%EB%A0%88%EC%8A%A4%ED%8A%B8#cite_note-Breiman1996-4 [위키백과: 랜덤포레스트]

https://ko.wikipedia.org/wiki/%EB%B0%B0%EA%B9%85 [위키백과 : 배깅]