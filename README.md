# KoSentenceBERT_V2
모델 구조 변경으로 성능 향상

## Model Architecture 
<img src= "https://user-images.githubusercontent.com/55969260/98637180-710bbe80-236b-11eb-9818-864f14610f40.png"> <br>
NLI 데이터를 통한 모델 학습은 [그림 1] 구조를 따른다. 서로 다른 두 문장 Sentence A와 Sentence B가 BERT Embedding 후 Pooling을 거쳐 u와 v 벡터로 나오게 된다. u와 v 벡터 사이의 거리를 나타내는 벡터인 |u-v|와의 결합과 더불어 두 문장 사이의 관계 정보가 더해진 벡터 u* 와 v* 결합이 추가된다. u* 와 v* 의 계산은 'Attention is all you need' 에서 제시된 Multi-head Attention 방법과 유사하게 진행된다. : <br>
<img src= "https://user-images.githubusercontent.com/55969260/97126995-b4ffa080-177b-11eb-8a0a-c2ac48cd52b6.png"> <br>
u* 와 v* 를 나머지와 결합하여 최종적으로 (u, v, |u-v|, u*, v*) 벡터를 생성한다. 

## Experiments
실험 결과는 [표 2]와 같으며,  성능 평가는 Cosine, Euclidean, Manhattan 그리고 Dot Product 각각의 Pearson correlation 과 Spearman’s rank correlation의 평균을 구하여 모델의 선형성과 단조성을 측정하였다. <br> SBERT에서의 결과와 마찬가지로 한국어 데이터에서도 NLI 데이터로 pre-training 후 STS 데이터로 fine-tuning한 NLI + STS 모델이 NLI와 STS를 단독으로 학습시킨 모델에 비해 성능이 좋게 나왔다. 또한 본 논문에서 제시한 구조로 학습한 모델은 영어 데이터에선 단독으로 학습시킨 NLI 모델과 NLI + STS로 학습한 모델 성능 둘 다의 향상을 보였지만 단독으로 학습된 한국어 NLI 모델은 성능이 테스트셋에선 낮아졌다.   <br> [표 2]의 결과로 보아 기존의 SBERT에서 각각 다른 문장의 Sentence Embedding u, v에서 서로의 관계 정보가 추가된 새로운 벡터 u*, v* 의 결합이 성능을 향상 시켰음을 알 수 있다. u* , v* 의 결합은 서로 다른 문장의 함축적인 벡터 표현으로 둘 사이의 연관성이라는 정보를 모델에게 주어 이전에는 찾을 수 없었던 정보를 통해 성능 향상을 이끌어 냈다. 이는 Sentence Embedding 벡터표현 또한 전체 Sequence의 출력 벡터의 Self-Attention 처럼 사용될 수 있음을 의미한다. <br><br>
<img src = "https://user-images.githubusercontent.com/55969260/98637937-803f3c00-236c-11eb-9eee-f11093cedecd.png"> <br>

## Downstream Tasks Demo
<img src = "https://user-images.githubusercontent.com/55969260/97133748-5b54a180-178e-11eb-8c80-04291456d561.gif"> <br>
