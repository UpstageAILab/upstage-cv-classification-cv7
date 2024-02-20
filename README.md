# Computer Vision 문서 타입 분류 대회

## Team

| ![김윤겸](https://avatars.githubusercontent.com/u/156163982?v=4) | ![남영진](https://avatars.githubusercontent.com/u/156163982?v=4) | ![노균호](https://avatars.githubusercontent.com/u/156163982?v=4) | ![이재민](https://avatars.githubusercontent.com/u/156163982?v=4) | ![윤수인](https://avatars.githubusercontent.com/u/156163982?v=4) |
| :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: | :--------------------------------------------------------------: |
|            [노균호](https://github.com/UpstageAILab)             |            [남영진](https://github.com/UpstageAILab)             |            [김윤겸](https://github.com/UpstageAILab)             |            [이재민](https://github.com/UpstageAILab)             |            [윤수인](https://github.com/UpstageAILab)             |
|                            팀장, Modeling                             |                            Modeling                           |                         Modeling, CV검증                        |                            Modeling                          |                            Modeling,  Augmentation                  |


## 1. Competiton Info

### Document type classification : 문서 타입 분류

- 대회 개요
     - 제공 데이터 활용, 주어진 문서 이미지를 입력 받아 17개의 클래스 중 정답을 예측
     - 주어진 문서 이미지를 입력 받아 17개의 클래스 중 정답을 예측
- 평가지표
     - Macro F1
- 제출물
     - 1570장의 학습 이미지를 통해 3140장의 평가 이미지를 예측(CSV파일)


## 2. Data Description

### Dataset overview

- 학습 데이터
     - 1570장의 학습 데이터

- 평가 데이터
     - 3140장의 이미지
     - 다양한 방식으로 왜곡된 이미지들이 존재함.
     - 왜곡 유형 1 :  다양한 각도의 회전
     - 왜곡 유형 2 :  좌우/상하 반전
     - 왜곡 유형 3 :  흐릿한 이미지
     - 왜곡 유형 4 :  그림자
     - 왜곡 유형 5 :  겹침/흔들림이 있는 이미지
     - 왜곡 유형 6 :  기타 


## 3. Augmentation

### augraphy는 문서에 특화된 라이브러리로 단독으로 사용하는 것은 자동차번호판 등 문서가 아닌 데이터에는 효과적이지 않을 것이라 생각되어  augraphy와 albumentations 사용.
### 다양한 실험을 통해 가장 데이터셋에 적합한 augmentation 조합을 찾음.

- Augraphy
     - BadPhotoCopy()
     - NoiseTexturize()
     - Folding()
     - DirtyDrum()
     - ShadowCast()
     - LightingGradient()
     - LowLightNoise() 

- albumentations 사용
     - Resize
     - HorizontalFlip
     - VerticalFlip
     - ShiftScaleRotate
     - Normalize

- Oversampling
     - 이미지 랜덤 회전: 90°/180°/270°/360° 중 랜덤 회전
     - 이미지 뒤집기: 수평 또는 수직 방향의 랜덤 뒤집기
     - 가우시안 노이즈 추가: 정규분포 노이즈의 적용
     - 블러 효과 적용: 모션, Median, 일반 블러 중 선택 적용
     - 외곽 회전 보완: 회전 후 남는 외곽을 흰색으로 채움
     - 이미지 왜곡 처리: 광학, 그리드, 어파인 변환 중 선택 적용

 

## 4. Modeling

### Model descrition

- Model : maxvit_xlarge_tf_512 
- Optimizer : NAdam


## 5. Result

### Leader Board

- pulic: 3등, F1 score 0.9634
- private: 5등, F1 score 0.9459 

### Presentation

- [_발표 Presentation file_]([https://docs.google.com/presentation/d/1OYKb5oHg4sF1zsmD0uk_fSvYPxf9Soo6icxFd6eUEHk/edit#slide=id.g2b368e284d4_1_75])

## etc



### Reference

- chrome-extension://efaidnbmnnnibpcajpcglclefindmkaj/https://arxiv.org/pdf/2204.01697v4.pdf
