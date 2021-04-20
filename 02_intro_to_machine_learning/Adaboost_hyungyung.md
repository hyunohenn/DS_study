# Adaboost

> 에이다 부스트
>
> AdaBoost (Adaptive Boosting) is a generic name (rather, meta-algorithm) that stands for a group of algorithms developed by Schapire and Freund and others that combine a host of rather weak (not so accurate) classifiers to create a strong (accurate) classifier.



## Strong Model vs. Weak Model

- Weak Model
  - random guessing 보다 아주 약간 높은 모델
  - 50:50 -> 60: 40
  - 적절하게 boost되면 매우 강한 모델이 될 수 있음

- 이때에 강한 모델이 되기 위해
  - 오류에 집중해보겠다!



## AdaBoost?

- 성능 향승을 위해 다른 많은 형태의 학습 알고리즘과 결합하여 사용
- **다른 약한 학습 알고리즘의 결과물들을 가중치를 두어 더하는 방법**
  - 개별 학습기들의 성능이 떨어지더라도, 각각의 성능이 무작위 추정보다 조금이라도 더 나아진다면, 
  - 결과적으로 최종 모델은 강한 classifier로 수렴한다

- 어떠한 머신 러닝 알고리즘이라도 base classifier가 될 수 있지만 주로 decision tree

- 이전의 classifier에 의해 잘못 분류된 것들을 이어지는 약한 학습기들이 수정해줄 수 있다는 점에서 다양한 상황에 적용 => Adaptive
  - 앞선 모델이 풀지 못하는 오류에 가중치를 주어 새롭고 매우 정확한 모델을 만든다



- 다음과 같은 조건을 만족하여야 한다
  - 분류기는 다양한 가중치를 가진 트레이닝 데이터에 대해 상호 학습되어야 한다
  - 반복 할 때마다 훈련 오류를 최소화하는 방법으로 최적의 fit을 찾는다



## Process

1. 처음에는 모든 관측치에 대해 동일한 가중치를 부여
2. 모델은 데이터의 부분집합을 활용하여 생성
3. 이 모델을 사용하여 전체 데이터 셋에 대한 예측 진행
4. 오류는 예측된 값과 실제 값을 비교하여 계산됨
5. 다음 모델을 생성 할 때에 오류로 판정된 데이터 포인트에 더 높은 가중치가 부여됨
6. 오차가 클 수록 데이터 포인트에 더 높은 가중치가 부여됨
7. 이 과정은 error가 더 이상 변하지 않을때까지 계속되거나, 또는 



![image-20210420013953557](Adaboost.assets/image-20210420013953557.png)

(ref) 고려대학교 DSBA, 강필성, https://youtu.be/Y2rsmO6Nr4I) 

강의가 아주 탁월합니다





**장단점**

- 장점: 다른 학습 알고리즘보다 과적합(overfitting)에 덜 취약 

- 단점: 잡음이 많은 데이터와 이사점(outlier)에 취약



## 앙상블 (Ensemble Learning)

- 여러개의 모델을 <u>조화롭게</u> 학습시켜 좀 더 정확한 모델을 생성하는 것
- 여러 개의 약한 성과를 가지는 모델들을 결함하여 좀 더 강력한 classifier를 생성하는 것
- 여러 개의 Decision Tree를 결합하여 하나의 결정 트리보다 더 좋은 성능을 내는 머신러닝 기법
- 배깅, 부스팅의 두 가지 방법이 있음



- 퀴즈쇼 예시

  - **BAGGING**

    - A 팀은 팀원이 각각 다른 책을 읽어서 할당하여 공부
    - 일주일동안 공부
    - 이 사람들이 공부한 내용을 바탕으로 대답의 대푯값을 팀의 대답으로 정함

    

  - **Boosting**

    - 첫번 째 사람에게 책 주고 보라고 시킴
    - 이 사람이 이 책에 어느 부분에 장점이 있고 약점이 있는지 확인
    - 앞 사람이 잘 푸는 영역에 대해서는 비중이 낮고 그렇지 않은 부분의 영역이 높은 책을 다음 사람에게 공부시킨다
    - 순차적으로 진행
    - 최종적으로 한 문제를 가지고 각각 문제를 풀게 한 뒤에 Aggregate



### 배깅 (Bagging)

> Bootstrap Aggregation 

- 샘플을 여러번 뽑아(Bootstrap) 각 모델을 학습시켜 결과물을 확인
- 추정의 분산(variance of estimates)를 줄이는 방법으로 결합된다

- 데이터를 부트스트랩(복원 랜덤 샘플링) 한 뒤 부트스트랩한 데이터로 모델 학습
  - 데이터를 뽑을 확률이 항상 같음
  - (부스팅은 그 선택 확률이 항상 다름)
- 학습된 모델을 확인하여 예측값 결정
  - Categorical Data -> Voting으로 결정
  - Continuous Data -> Mean으로 결정



- 모델이 상호 독립적

- Random forest, extra trees...
- Bias는 낮지만 Variance는 높은 (모델의 복잡도가 높은 알고리즘들)을 학습시킨 다음에 결합
- 장단점
  - 장점: overfitting을 감소, 병렬화 가능





### 부스팅 (Boosting)

> 가중치를 활용한 방법

- 모델 간 영향을 받음
- 모델이 예측을 하면 그 예측 결과에 따라 데이터에 가중치가 부여됨

- 오답에 대해서 높은 가중치 부여, 정답에 대해서는 낮은 가중치를 부여
  - 오답을 정답으로 맞추기 위해 오답에 집중하게 됨

- 최근에 kaggle등에서 많이 사용되고 있음
- AdaBoost, Gradient Boosting, XGBoost.....
- 특정한 데이터 셋에 대해 먼저 알고리즘으로 학습을 하고 학습된 알고리즘이 잘 풀어내지 못하는 문제들을 다음 단계에서
  중점적으로 풀어보는 시도가 주 목적

- 장단점
  - 장점: 배깅에 비해 error가 적다 (성능 좋음)
  - 단점: 속도가 느리고 overfitting의 가능성 증가
    -  각각의 예측이 이전의 모델이 훈련/ 평가된 후에만 진행되기 때문에 모델의 병렬화 불가능(오래걸림)



## References

- Hyeong In Choi, Lectures on Machine Learning, Seoul National University, https://www.math.snu.ac.kr/~hichoi/machinelearning/lecturenotes/AdaBoost.pdf

- Baek Kyun Shin, https://bkshin.tistory.com/entry/%EB%A8%B8%EC%8B%A0%EB%9F%AC%EB%8B%9D-11-%EC%95%99%EC%83%81%EB%B8%94-%ED%95%99%EC%8A%B5-Ensemble-Learning-%EB%B0%B0%EA%B9%85Bagging%EA%B3%BC-%EB%B6%80%EC%8A%A4%ED%8C%85Boosting

- https://www.kaggle.com/prashant111/adaboost-classifier-tutorial
- https://www.youtube.com/watch?v=Y2rsmO6Nr4I