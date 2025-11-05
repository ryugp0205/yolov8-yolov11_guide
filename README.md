# yolov8-yolov11_guide
### YOLOv11 정리

안녕하세요! 이 문서는 컴퓨터 비전에서 많이 쓰이는 **YOLO(You Only Look Once)** 모델 중, 최신 버전인 **YOLOv11**을 이해하고 사용하기 위해 정리한 내용입니다.  

---

## 1. YOLO 소개

YOLO는 **실시간 객체 탐지(Object Detection)** 모델입니다.  
한 번의 신경망 연산으로 이미지 내의 객체 위치와 클래스(종류)를 동시에 예측할 수 있습니다.

- **장점**
  - 빠른 속도 (실시간 가능)
  - End-to-End 학습 가능
  - 비교적 간단한 구조
<img width="838" height="347" alt="스크린샷 2025-11-05 151532" src="https://github.com/user-attachments/assets/63d14c93-3bb2-481e-921d-76adb5f6a5cf" />

---

## 2. YOLOv8 vs YOLOv11 비교

| 항목 | YOLOv8 | YOLOv11 |
|------|--------|---------|
| 발표년도 | 2023 | 2024 |
| 모델 구조 | PyTorch 기반, 간단 | YOLOv8 개선, 정확도 향상 |
| 속도 | 빠름 | YOLOv8 대비 약간 느림, 정확도 ↑ |
| 학습 편의성 | 쉬움 | YOLOv8과 비슷, 더 정교한 데이터 증강 지원 |
| 특징 | 경량화, 실시간 사용에 적합 | 더 나은 작은 객체 탐지, 다양한 백본 지원 |
| 사용 예시 | 웹캠 객체 탐지 | 산업용 CCTV, 정밀 객체 탐지 |

---

## 3. YOLO에서 자주 쓰이는 용어

| 용어 | 의미 |
|------|------|
| Backbone | 특징(feature)을 추출하는 신경망 부분 (예: CSPDarknet) |
| Head | 최종 출력(예: 바운딩 박스, 클래스) 부분 |
| Anchor | 객체 크기와 비율을 미리 정의한 기준 박스 |
| IOU(Intersection over Union) | 예측 박스와 실제 박스 겹치는 정도 |
| Confidence | 객체 존재 확률 |
| Class | 객체 종류 (예: 사람, 자동차 등) |
| Dataset | 학습에 사용되는 이미지와 라벨 집합 |
| Epoch | 전체 데이터셋을 한 번 학습하는 과정 |
| Augmentation | 학습 데이터 변형 기법 (회전, 반전 등) |
| Loss | 모델 학습 중 오류 측정 값 |

---

## 4. YOLOv11 설치 및 사용 (간단 예시)

```bash
# YOLOv11 설치
pip install ultralytics

# 학습 예시
yolo task=detect mode=train data=coco128.yaml model=yolov11n.pt epochs=100

# 추론 예시
yolo task=detect mode=predict model=yolov11n.pt source='images/test.jpg'''

# 🚀 YOLOv11 설치 및 사용 가이드

Ultralytics의 **YOLOv11**은 최신 객체 탐지(Object Detection) 모델입니다.  
이 문서는 설치부터 학습, 추론, 모델 다운로드까지 빠르게 사용할 수 있도록 구성되어 있습니다.

---

## ⚙️ 1. 설치

아래 명령어를 터미널에 입력하세요 👇

```bash
pip install ultralytics
## YOLO11 모델 다운로드
| 모델                                                                                   | 크기(픽셀) | mAPval 50-95 | 속도 CPU ONNX (ms) | 속도 T4 TensorRT10 (ms) | 파라미터 (M) | FLOPs (B) |
| ------------------------------------------------------------------------------------ | ------ | ------------ | ---------------- | --------------------- | -------- | --------- |
| [YOLO11n](https://github.com/ultralytics/assets/releases/download/v8.3.0/yolo11n.pt) | 640    | 39.5         | 56.1 ± 0.8       | 1.5 ± 0.0             | 2.6      | 6.5       |
| [YOLO11s](https://github.com/ultralytics/assets/releases/download/v8.3.0/yolo11s.pt) | 640    | 47.0         | 90.0 ± 1.2       | 2.5 ± 0.0             | 9.4      | 21.5      |
| [YOLO11m](https://github.com/ultralytics/assets/releases/download/v8.3.0/yolo11m.pt) | 640    | 51.5         | 183.2 ± 2.0      | 4.7 ± 0.1             | 20.1     | 68.0      |
| [YOLO11l](https://github.com/ultralytics/assets/releases/download/v8.3.0/yolo11l.pt) | 640    | 53.4         | 318.4 ± 1.4      | 6.2 ± 0.1             | 25.3     | 86.9      |
| [YOLO11x](https://github.com/ultralytics/assets/releases/download/v8.3.0/yolo11x.pt) | 640    | 54.7         | 462.8 ± 6.7      | 11.3 ± 0.2            | 56.9     | 194.9     |
