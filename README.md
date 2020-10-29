# KoSentenceBERT_V2
모델 구조 변경으로 성능 향상

## Model Architecture 
<img src= "https://user-images.githubusercontent.com/55969260/97127194-4b33c680-177c-11eb-9ff7-b2c3c233434d.png"> <br>
NLI 모델 학습은 [그림 1] 구조를 따른다. 서로 다른 두 문장 Sentence A와 Sentence B가 BERT 임베딩 후 Pooling을 거쳐 u와 v 벡터로 나오게 된다. u와 v 벡터
사이의 거리를 나타내는 벡터인 |u-v|와의 결합과 더불어 두 문장 임베딩 사이의 Attention이 추가된 벡터 u* 와 v* 결합이 더해진다. u* 와 v* 의 계산은 'Attention is all you need'에서 제시된 Multi-head Attention  방법과 유사하게 진행된다. : <br>
<img src= "https://user-images.githubusercontent.com/55969260/97126995-b4ffa080-177b-11eb-8a0a-c2ac48cd52b6.png"> <br>
u*와 v*를 나머지와 결합하여 최종적으로 (u, v, |u-v|, u*, v*) 벡터를 생성한다. 

## Experiments
실험 결과는 [표 2]와 같으며, 성능 평가는 Pearson correlation과 Spearman’s rank correlation으로 모델의 선형성과 단조성을 측정하였다. <br> SBERT에서의 결과와 마찬가지로 한국어 데이터에서도 NLI 데이터로 pre-training 후 STS 데이터로 fine-tuning 한 NLI + STS 모델이 NLI와 STS를 단독으로 학습 시킨 모델에 비해 성능이 좋게 나왔다. 또한 본 논문에서 제시한 구조로 학습한 모델도 데이터에 상관 없이 NLI + STS로 학습한 모델 성능 둘 다의 향상을 보였다.  <br> [표 2]의 결과로 보아 기존의 SBERT에서 각각 다른 문장 임베딩 u, v에서 서로의 Attention이 추가된 새로운 벡터 u*, v* 의 결합이 성능을 향상 시켰음을 알 수 있다. u*, v* 의 결합은 서로 다른 문장의 함축적인 벡터 표현으로 둘 사이의 연관성이라는 정보를 모델에게 주어 이전에는 찾을 수 없었던 정보를 통해 성능이 향상되었다. <br><br>
<img src = "https://user-images.githubusercontent.com/55969260/97127404-dca33880-177c-11eb-86c4-a31515b1556b.png"> <br>

## Downstream Tasks Demo
<img src = "https://user-images.githubusercontent.com/55969260/97133748-5b54a180-178e-11eb-8c80-04291456d561.gif"> <br>
