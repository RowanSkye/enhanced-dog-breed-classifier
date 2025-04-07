🐶 enhanced-dog-breed-classifier
강아지 사진을 업로드하면 품종을 예측하는 딥러닝 기반 이미지 분류 프로젝트입니다.
원본 코드의 구조를 개선하고, 하이퍼파라미터를 조정하여 성능을 향상시켰습니다.
학습된 모델을 즉시 불러와 품종을 빠르게 예측할 수 있도록 구성하여, 실제 서비스에 가까운 프로토타입 기능도 구현했습니다.

📌 프로젝트 개요
Capstone Project - dog breeds classifier (by hengzheng)
수정 및 확장: Enhanced Dog Breed Classifier (by RowanSkye)
모델: DenseNet121 기반 CNN
데이터: 이미지 + 레이블 (품종명)
✨ 주요 수정 및 개선 사항
1) 학습 데이터 구성 개선
✅ 기존 120개 품종 → 121개 품종으로 클래스 수 확장
→ 더 다양한 품종 분류 가능 + 실사용 확장성 향상

2) 학습 후 즉시 추론 가능한 구조 구현
✅ 모델 전체 구조 및 가중치를 .keras로 저장
✅ load_model() 후 추가 학습 없이 바로 품종 예측 가능
→ 재학습 없이 빠른 품종 추론 가능 (서비스화에 적합)

3) 학습 최적화를 위한 콜백 설정 개선
✅ ModelCheckpoint, ReduceLROnPlateau, EarlyStopping 적용
✅ 기존 대비 patience, factor, min_lr 등 세부 수치 조정
→ 성능 향상 + 과적합 방지 + 불필요한 학습 최소화

4) 성능 평가 및 해석 시각화 강화
✅ classification_report, confusion_matrix 출력
✅ 클래스별 정밀도, 재현율, F1-score를 Bar Plot으로 시각화
→ 모델 성능 분석 및 결과 해석 용이

📁 디렉토리 구조
enhanced-dog-breed-classifier/
├── archive/
│   ├── annotations/
│   │   └── Annotation/                  # XML 형식의 이미지 어노테이션 (bounding box 포함)
│   └── images/
│       └── Images/                      # 원본 강아지 이미지 121종 폴더별 저장
│
├── data/                                # 전처리된 이미지 저장 폴더 (잘린 + 리사이즈된 이미지)
│   └── [breed folders]/                 # 품종별 전처리 이미지 저장
│
├── dense/
│   ├── DenseNet-BC-121-32-no-top.h5     # 사전 학습된 DenseNet121 모델 (top 제거된 상태)
│   └── final_dog_breed_model.keras      # 학습된 최종 모델 (.keras 저장)
│
├── label_maps_rev.npy                   # 숫자 → 품종명 매핑된 딕셔너리 저장
│
├── code_enhanced_dog_breed_classifier.ipynb     # 최종 학습 및 평가 
├── code_dog_inference_demo.ipynb                # 실시간 예측 및 성능 시각화 데모
│
├── test_6.jpg, test_7.jpg, ...          # 테스트용 이미지 (URL 다운로드 or 직접 저장)
│
├── README.md                            # 프로젝트 설명 및 실행 방법 안내 문서

📁 주요 코드 파일
code_enhanced_dog_breed_classifier.ipynb: → 데이터 전처리, 모델 학습, 저장까지 포함한 전체 파이프라인

code_dog_inference_demo.ipynb: → 저장된 모델 불러와서 실시간 예측 + 시각화 (classification report, confusion matrix 등 포함)

💾 경로 설명
경로	설명	생성 방식
archive/	원본 데이터셋 폴더 (이미지 및 어노테이션 포함)	수동 준비 (Stanford Dogs Dataset)
├── images/Images/	121개 강아지 품종 이미지가 폴더별로 저장됨	수동 준비
├── annotations/Annotation/	이미지 별 bounding box 정보 (XML)	수동 준비
data/	잘린 + 리사이즈된 전처리 이미지 저장 폴더	자동 생성
├── [breed folders]/	품종별 전처리 이미지가 저장된 하위 폴더	자동 생성
dense/	모델 파일 저장 폴더	수동 생성 (폴더), 파일은 코드에서 저장
├── DenseNet-BC-121-32-no-top.h5	사전학습된 DenseNet121 모델	수동 준비 (Kaggle에서 제공)
├── final_dog_breed_model.keras	학습된 최종 모델 (.keras)	자동 생성
label_maps_rev.npy	숫자 레이블 → 품종명 매핑 딕셔너리	자동 생성
test_6.jpg, test_7.jpg 등	테스트용 강아지 이미지	수동 준비
📦 원본 이미지 데이터 다운로드 안내
⚠️ GitHub 저장 용량 제한으로 인해, 원본 이미지 및 어노테이션 데이터는 직접 다운로드해야 합니다. 👉 아래 링크를 통해 Stanford Dogs Dataset의 이미지 및 주석(XML) 파일을 받아주세요:

📂 Stanford Dogs Dataset 다운로드 (Images & Annotations)

📥 다운로드한 압축 파일을 해제한 후, 아래 경로에 맞게 폴더를 배치해 주세요:

📁 enhanced-dog-breed-classifier/
├── archive/
│   ├── images/
│   │   └── Images/                ← 121개 품종 이미지 폴더
│   └── annotations/
│       └── Annotation/           ← 각 이미지의 bounding box 정보(XML)
✅ 위 경로 구조는 모델 학습 및 전처리 과정에서 필수로 사용되므로, 정확한 위치에 배치해 주세요. (※ 경로가 다를 경우, 코드에서 오류가 발생할 수 있습니다.)

🙌 기여자
원작자: hengzheng
코드 구조 개선 및 기능 확장 : RowanSkye