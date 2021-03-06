## Random Forest 
### 1. 결정 트리 앙상블 기법의 하나  

#### 1) 앙상블(ensemble) 
 - 여러 머신러닝 모델을 연결하여 더 강력한 모델을 만드는 기법으로 앙상블 기법중 랜덤포레스트(random forest)와 그래디언트 부스팅(gradient boosting)은 둘 다 기본을 구성하는 요소가 결정 트리로 되어 있다.   

#### 2) 결정 트리는 분류를 위한 알고리즘이 아닌가? 
 - 결정 트리 알고리즘은 분류 뿐 아니라 회귀도 가능함 
 - 트리가 CART(Classification and Regression Tree) 기반으로 만들어져 있기 때문에, 회귀도 가능한 알고리즘임 
 - 분할의 기준은 RSS(SSE)가 최소가 될 수 있는 기준을 찾아서 분할 하게 되며, 최종 분할이 완료 된 후에 각 분할 영역에 있는 데이터 결정값들의 평균 값으로 학습/예측하게 됨 
 
![Random_forest_dt_ex](https://user-images.githubusercontent.com/49746140/104828313-6b6eaf80-58ab-11eb-98df-ab4ec07a27eb.JPG)

<I> 하지만 랜덤포레스트의 기본 요소인 결정 트리의 단점은 훈련 데이터에 과대적합되는 경향이 있다는 것이며 따라서 트리의 크기 및 노드 개수에 제한해야함.따라서 과적합을 피하기 위한 방법으로 앙상블 기법이 사용됨 </I>

### 2. 랜덤포레스트 

#### 1) 랜덤포레스트란? 
 - 결정 트리의 주요 단점인 과대적합을 회피할 수 있는 방법으로, 결정 트리의 묶음. 각 트리는 비교적 예측을 잘 하지만, 일부에 있어 과대 적합이 발생하는 경향을 보이므로 서로 다른 방향으로 과대적합된 트리를 많이 만들고 그 결과를 평균 냄으로써 과대적합된 양을 줄이는 알고리즘이다. 
 - 이를 위해서 각각의 트리는 타깃 예측을 잘하면서 다른 트리들과는 구별되는 많은 트리를 만들어야 됨 
 - 따라서 랜덤포레스트에서 많은 트리를 생성하기 위한 방법은 2가지 있음   
   a. 데이터를 무작위로 선택   
   b. 분할 테스트에서 특성을 무작위로 선택   
 
#### 2) 랜덤포레스트 구축 
 - from sklearn.ensemble import RandomForestRegressor 를 통해 구축 가능하며,  
   각 parameter에 대해서 설명하면 
   a. n_estimators : 트리 개수로, 클수록 안정적인 모델을 만들어 주어 좋지만 메모리를 많이 사용하게 되어 훈련과 예측이 느려진다.  
   b. n_samples : 트리를 만들기 위해 먼저 데이터의 bootstrap sample을 생성해야하며, 몇 개의 sample을 생성할지를 나타냄. 
   c. max_features : n_samples개의 데이터 셋으로 결정 트리를 만들게 되며, 이 때 각 노드에서 전체 feature를 대상으로 하는 것이 아닌, 각 노드에서 후보 feature를 무작위로 선택한 후 이 후보들 중에서 최선의 결과를 찾는다. 
   
   <I> 랜덤 포레스트는 결정 트리와 같이 특성 중요도를 제공하며, 이 특성 중요도는 각 트리의 특성 중요도를 취합하여 계산된 것이기 때문에 하나의 트리에서 제공하는 것보다 더 신뢰도가 높다 </I> 
   
#### 3) 랜덤포레스트 장단점 
 - 랜덤 포레스트는 매개 변수 튜닝을 많이 하지 않아도 잘 작동하며, 데이터의 스케일을 맞출 필요가 없다 
 - 단일 트리의 과적합 등의 단점을 보완해준다. 
 - 대량의 데이터셋에서 모델을 만들 때 다소 시간이 걸릴 수 있다. 단, CPU 코어가 많다면 손귑게 병렬 처리 가능하며 <B> n_jobs </B> 변수를 이용하여 사용할 코어 수를 지정할 수 있다. 
 
#### 4) 랜덤포레스트 사용 시 주의할 점 
 - random_state : 랜덤 포레스트는 랜덤하게 선택되어지는 부분들이 있기 떄문에 random_state를 다르게 지정하면 전혀 다른 모델이 만들어진다. 따라서 지정이 꼭 필요하다. 하지만 트리의 수가 많아지면 그 변동은 적다. 
 - 랜덤 포레스트는 텍스트 데이터와 같이 매우 차원이 높고 sparse한 데이터에는 잘 작동하지 않는다. 이런 모델은 선형 모델이 더 적합할 수 있다. 
   
   
 
