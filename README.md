# DeepVoice Detection with Benford's Law

딥보이스(Deepfake Voice) 탐지를 위해 벤포드의 법칙(Benford's Law)을 적용한 연구 코드 저장소입니다.  
본 프로젝트는 경희대학교 테크노경영대학원 AI기술경영학과 석사학위 논문  
_"딥보이스 탐지를 위한 벤포드의 법칙 적용 가능성에 관한 연구 (2025)"_ 를 기반으로 작성되었습니다.

---

## 연구 배경
딥보이스 기술은 특정 인물의 음성을 정밀하게 모방하여 합성할 수 있는 기술로,  
보이스피싱, 음성 기반 인증 우회, 정치적 허위 정보 유포 등 다양한 악용 가능성이 존재합니다.  
이에 따라 실제 음성과 합성 음성을 구분할 수 있는 탐지 기술이 필수적입니다.

벤포드의 법칙은 자연 발생 데이터의 첫 자릿수가 특정 분포를 따른다는 통계적 현상으로,  
본 연구에서는 이를 활용하여 합성 음성과 실제 음성을 구분하는 벤포드 스코어(Benford Score) 변수를 설계하고  
탐지 모델(LSTM)에 적용하였습니다.

---

## 연구 방법론
1. 데이터 수집  
   - Kaggle 공개 데이터셋: [Deep-Voice: DeepFake Voice Recognition](https://www.kaggle.com/datasets/birdy654/deep-voice-deepfake-voice-recognition)  
   - 추가 데이터: 문재인/윤석열 대통령 신년사(YouTube), HitPaw VoicePea를 이용한 합성 음성

2. 특징 추출  
   - 오디오 특징 26종 (Chroma, RMS, Spectral Centroid, Bandwidth, Rolloff, ZCR, MFCC 1~20)  
   - 각 데이터 벡터에 대해 벤포드 스코어를 계산하여 추가 변수로 활용

3. 모델 설계  
   - Bi-LSTM 기반 분류 모델  
   - 두 가지 모델 비교
     - (1) 벤포드 스코어 미적용
     - (2) 벤포드 스코어 적용

4. 성능 평가  
   - 지표: Accuracy, Precision, Recall, F1-Score, ROC-AUC  
   - 벤포드 스코어 적용 모델이 전반적으로 더 높은 성능을 기록  
   - Kaggle 데이터셋 기준: Accuracy 0.994, F1 0.994 (벤포드 적용 시)  

---

## 주요 결과
- 벤포드 스코어 적용 시 모델의 재현율(Recall)과 정확도(Accuracy)가 유의미하게 개선됨  
- 오탐(False Positive) 수가 50건 → 10건으로 감소  
- 추가 검증 데이터(한국어 음성)에서도 성능 개선 효과 확인 (다만 데이터셋 환경 차이로 성능 저하 존재)  
- 10분 길이 음성 기준 실시간 탐지 가능성 확인 (총 처리 시간 약 43.5초)  

---

## Repository 구조
```
├── DATA/  
│   └── 실험에 사용한 데이터셋 (원본 + 추가 합성 데이터)
├── 1_extract.ipynb  
│   └── 음성 및 주변음 분리, 특징 추출 코드
├── 2_Deepvoice_Detection_Original.ipynb  
│   └── 벤포드 스코어 미적용 모델 학습/평가
├── 3_Deepvoice_Detection_Benford.ipynb  
│   └── 벤포드 스코어 적용 모델 학습/평가
```

---

## 실행 방법
1. 저장소 클론
   ```bash
   git clone https://github.com/DoDuck9403/Deepvoice_Detection.git
   cd Deepvoice_Detection
   ```
2. Jupyter Notebook 실행 후, 각 단계별 `.ipynb` 파일 실행
   - `1_extract.ipynb`: 데이터 전처리 및 특징 추출
   - `2_Deepvoice_Detection_Original.ipynb`: 기본 모델 학습/평가
   - `3_Deepvoice_Detection_Benford.ipynb`: 벤포드 적용 모델 학습/평가

---

## 참고 논문
이민성 (2025). _딥보이스 탐지를 위한 벤포드의 법칙 적용 가능성에 관한 연구_,  
경희대학교 테크노경영대학원, 석사학위논문.

---

## 키워드
`Benford’s Law` `Deep Voice Detection` `LSTM` `Voice Synthesis` `AI Security`
