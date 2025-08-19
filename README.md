# DeepVoice Detection with Benford's Law  

딥보이스(Deepfake Voice) 탐지를 위해 벤포드의 법칙(Benford's Law)을 적용한 탐지 모델 연구/개발 프로젝트입니다.  
본 프로젝트는 경희대학교 테크노경영대학원 석사 학위 논문  
"딥보이스 탐지를 위한 벤포드의 법칙 적용 가능성에 관한 연구 (2025)"를 기반으로 작성되었으며,  
연구 결과뿐만 아니라 데이터 처리 파이프라인과 코드 실행 재현이 가능하도록 구성되었습니다.  

---

## 연구 배경
딥보이스 기술은 특정 인물의 음성을 정밀하게 합성할 수 있어,  
보이스피싱, 음성 기반 인증 우회, 정치적 허위 정보 유포 등 악용 가능성이 큽니다.  
이에 따라 합성 음성과 실제 음성을 구분할 수 있는 탐지 기술이 필수적입니다.  

벤포드의 법칙은 자연 발생 데이터의 첫 자릿수가 특정 분포를 따른다는 통계적 현상입니다.  
본 연구에서는 이를 오디오 특징 벡터에 적용해 벤포드 스코어(Benford Score) 변수를 설계하고,  
Bi-LSTM 모델 학습에 반영하여 딥보이스 탐지 성능을 개선했습니다.  

---

## 프로젝트 개요
- 데이터 수집
  - Kaggle 공개 데이터셋: *Deep-Voice: DeepFake Voice Recognition*  
  - 자체 수집: 대통령 신년사 음성(문재인/윤석열), HitPaw VoicePea로 생성한 합성 음성  
- 데이터 전처리 및 특징 추출
  - 오디오 특징 26종 추출 (Chroma, RMS, Spectral Centroid, Bandwidth, Rolloff, ZCR, MFCC 1~20)  
  - 각 데이터 벡터에 대해 벤포드 스코어 계산 → 새로운 특징으로 구조화  
  - 실제/합성 여부 라벨링하여 학습용 데이터셋 구성  
- 모델 설계
  - Bi-LSTM 기반 분류 모델  
  - (1) 벤포드 스코어 미적용 vs (2) 벤포드 스코어 적용 모델 비교  
- 성능 평가
  - 지표: Accuracy, Precision, Recall, F1-Score, ROC-AUC  
  - Kaggle 데이터셋 기준: Accuracy 0.994, F1 0.994 (벤포드 적용 시)  
  - 한국어 음성 추가 검증 시에도 성능 개선 확인 (다만 데이터셋 특성 차이로 일부 성능 저하 존재)  

---

## 주요 결과
- 벤포드 스코어 적용 시 모델의 Recall·Accuracy 모두 개선  
- False Positive 50건 → 10건으로 감소  
- 추가 한국어 음성 검증에서도 성능 개선 확인  
- 10분 길이 음성 기준 실시간 탐지 가능성 검증 (처리 시간 약 43.5초)  

---

## Repository 구조
```
├── DATA/  
│   └── 실험 데이터셋 (원본 + 합성 데이터)  
├── 1_extract.ipynb  
│   └── 음성 및 주변음 분리, 특징 추출 코드  
├── 2_Deepvoice_Detection_Original.ipynb  
│   └── 벤포드 스코어 미적용 모델 학습/평가  
├── 3_Deepvoice_Detection_Benford.ipynb  
│   └── 벤포드 스코어 적용 모델 학습/평가  
```

---

## 실행 방법
```
# 저장소 클론
git clone https://github.com/DoDuck9403/Deepvoice_Detection.git
cd Deepvoice_Detection

# Jupyter Notebook 실행 후 단계별 실행
1_extract.ipynb                   # 데이터 전처리 및 특징 추출
2_Deepvoice_Detection_Original.ipynb   # 기본 모델 학습/평가
3_Deepvoice_Detection_Benford.ipynb    # 벤포드 적용 모델 학습/평가
```

---

## 기술 포인트
- 데이터 엔지니어링 : 원천 오디오 → 특징 추출 → 구조화된 벡터 데이터셋 자동 생성  
- 라벨링 : 실제/합성 음성 라벨링 기반 학습 데이터셋 구성  
- 모델링 : Bi-LSTM + Benford Score 적용 비교 실험  
- 운영 고려 : 실시간 처리 가능성 검증, 데이터셋 확장성 확인  

---

## 참고 논문
이민성 (2025). 딥보이스 탐지를 위한 벤포드의 법칙 적용 가능성에 관한 연구,  
경희대학교 테크노경영대학원, 석사학위논문.  
