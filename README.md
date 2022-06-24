# Data Mining Term Project

## [ Term Project ] 
1. 선택한 데이터셋 소개와 속성 설명
    1) 선택한 데이터셋 : 스팸베이스 데이터로, 스팸 메일 분류 분석을 실시한다. 
    2) 속성 : 4601 rows X 58 columns
		- 1 ~ 57번째 변수 : 이메일의 텍스트로부터 계산된 특징값들
		- 58번째 변수 : 스팸(1)인지 아닌지(0)를 나타내는 반응 변수
		- word_freq_WORD : 이메일에서 WORD 단어의 발생 빈도 퍼센트
		- char_freq_CHAR : 이메일에서 CHAR 글자의 발생 빈도 퍼센트
		- capital_run_length_average : 연속으로 등장하는 대문자들의 평균 길이
		- capital_run_length_longest : 연속으로 등장하는 대문자들 중 가장 긴 길이
		- capital_run_length_total : 연속으로 등장하는 대문자들의 총 개수

2. 전처리와 학습 알고리즘 적용 및 성능 평가
 1) 전처리
 데이터에 결측치가 없고, 모두 연속형 변수이다.
 
 ![image](https://user-images.githubusercontent.com/74047671/175525417-cc9cd4fd-ebf9-4530-bdbd-834ef4ce3ec0.png)
 
![image](https://user-images.githubusercontent.com/74047671/175525422-ea68fe4c-8307-49c7-addc-526da76c3c53.png)
  
Y값을 제외하고 55, 56번째 변수만 int형이어서 float형으로 형변환해주었다.

![image](https://user-images.githubusercontent.com/74047671/175525454-c42bec40-456b-4e1c-8ede-53acaac31f2b.png)

 
Data와 target을 분리하고, target 데이터 값의 전체적인 비율을 확인했다.

![image](https://user-images.githubusercontent.com/74047671/175525490-1c1ce4e1-a7a2-4acc-8cc2-378e535385d6.png)

 
연속형 변수들에 StandardScaler를 적용시켰다.
 
 ![image](https://user-images.githubusercontent.com/74047671/175525506-bca45649-874e-4e02-8322-7b7b52d6e578.png)


2) 모델 적용 및 성능 평가
먼저 DecisionTreeClassifier를 Pipeline을 사용해 적용시켰다. 
597개의 노드와 정확도는 약 89.91%이다.

![image](https://user-images.githubusercontent.com/74047671/175525522-c66c15ad-9adb-4b21-a7a4-27f97311ca61.png)

![image](https://user-images.githubusercontent.com/74047671/175525532-34d8c71e-1b22-445c-a120-967e8a2557a0.png)

최적의 깊이도 구해보았다.

![image](https://user-images.githubusercontent.com/74047671/175525607-1b18bb4f-0ad0-4e71-910a-0025346c565c.png)

 
깊이가 10일 때, 정확도가 약 91.19%로 가장 성능이 좋은 것을 확인했다.
다음으로 KNN과 Random Forest를 적용시키면서 ROC 분석을 실행했다.

![image](https://user-images.githubusercontent.com/74047671/175525655-3f8faaf7-89f7-480c-8e21-2d3074fdbbad.png)

![image](https://user-images.githubusercontent.com/74047671/175525672-e4baea5f-3f15-4574-82a8-643b6ae3f58e.png)

실행 결과, 전체적으로 성능이 좋고 그 중에서도 RandomForest가 가장 좋은 것을 확인했다.
Confusion_matrix를 사용해 KNN과 RandomForest의 정확도를 평가해봤다.

![image](https://user-images.githubusercontent.com/74047671/175525700-5ae0c201-8418-4f7d-a7a2-291503d061cf.png)

![image](https://user-images.githubusercontent.com/74047671/175525708-d2c5e06a-c890-4a58-9e0d-87f46513b04d.png)

K가 5일 때 정확도가 90.98%로 가장 좋은 것을 확인했다.
다음으로 RandomForest의 Confusion matrix이다.

![image](https://user-images.githubusercontent.com/74047671/175525738-2a1b606d-c8ab-4024-a757-b0c185b25cb0.png)

정확도가 약 95.58%로 가장 좋은 것을 확인했다.
결과적으로, Random Forest 분류기를 적용하면 95.58%의 정확도로 스팸 메일을 분류할 수 있다.
