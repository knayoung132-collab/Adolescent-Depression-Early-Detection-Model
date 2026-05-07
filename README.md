# 😔 Adolescent Depression Early Detection Model

**Accuracy 84.6% / F1 84.6% / AUC 0.96**

An NLP pipeline that detects depression in adolescents by combining Naver KnowledgeIN text data with AI Hub youth voice data, using KLUE/BERT fine-tuning and Whisper STT.

## My Contributions *(4-person team)*

| Area | What I did |
|------|------------|
| **Data Collection** | Proposed using Naver KnowledgeIN expert Q&A as an alternative to inaccessible clinical data, and implemented data collection via Naver KnowledgeIN API |

---

## Results

| Metric | Score |
|--------|-------|
| **Accuracy** | **84.6%** |
| **F1-Score** | **84.6%** |
| **AUC** | **0.96** |

---

## Pipeline

    Data Sources
      ├── Naver KnowledgeIN crawling → GPT-4 API labeling
      └── AI Hub youth voice data (56 students, 27,214 utterances) → emotion tag labeling
                        ↓
                  Data merge & preprocessing
                        ↓
            [KLUE/BERT-base] Transfer Learning
                        ↓
           Sentence-level binary classification (depressed / not)
                        ↓
           [OpenAI Whisper] Speech → Text
                        ↓
             [Gradio] Deployed on HuggingFace Space

---

## Dataset

| Source | Description | Size |
|--------|-------------|------|
| Naver KnowledgeIN | Expert Q&A on student depression | ~8,000 posts |
| AI Hub | Free conversation voice data from 56 adolescents | 27,214 utterances |

---

## Tech Stack

`Python` `PyTorch` `KLUE/BERT-base` `HuggingFace Transformers` `OpenAI Whisper` `GPT-4 API` `Gradio` `BeautifulSoup` `Pandas`

---

## Training Config

| Parameter | Value |
|-----------|-------|
| Model | klue/bert-base |
| Epochs | 3 |
| Batch Size | 8 |
| Warmup Steps | 500 |
| Weight Decay | 0.01 |

---

## Team Contributions *(4-person team)*

| Role | Area |
|------|------|
| **Data Collection (Me)** | Proposed KnowledgeIN as data source, implemented API crawling |
| Labeling | GPT-4 auto-labeling pipeline, AI Hub emotion tag labeling |
| Modeling | KLUE/BERT fine-tuning, Whisper STT integration |
| Deployment | Gradio app, HuggingFace Space |

---

## Limitations & Next Steps

- Small voice dataset (56 students) limits generalization
- Two heterogeneous data sources may introduce noise
- AI-based labeling for voice data lacks clinical validation
- Non-verbal cues (tone, speed) not yet incorporated

---

---

# 😔 청소년 우울감 조기발견 모델

**Accuracy 84.6% / F1 84.6% / AUC 0.96**

음성 데이터와 텍스트 데이터를 결합하여 청소년의 우울감을 조기에 탐지하는 AI 모델입니다.

[▶ 서비스 체험하기](https://ireneminhee-depression-detector.hf.space)

---

## 본인 담당 역할

| 역할 | 내용 |
|------|------|
| **데이터 기획 (본인)** | 정신과 데이터의 민감성과 수집 한계를 고려하여 네이버 지식iN 전문가 답변 데이터 활용 아이디어 제안 및 네이버 지식iN API를 통한 데이터 수집 담당 |

---

## 성능

| 지표 | 값 |
|------|----|
| **Accuracy** | **84.6%** |
| **F1-Score** | **84.6%** |
| **AUC** | **0.96** |

---

## 데이터셋

| 데이터 | 출처 | 설명 |
|--------|------|------|
| 지식iN 크롤링 | 네이버 지식iN API | 학생 우울증 관련 질문·답변 ~8,000건 |
| 청소년 음성 | AI Hub | 56명 학생 자유 대화, 27,214 문장 |

---

## 모델 성능

| Epoch | Val Loss | Accuracy | F1 |
|-------|----------|----------|----|
| 1 | 0.5708 | 0.7308 | 0.7246 |
| 2 | 0.4213 | 0.7981 | 0.7968 |
| **3** | **0.3466** | **0.8462** | **0.8463** |

---

## 팀 구성 (4인)

| 역할 | 담당 |
|------|------|
| **데이터 기획 (본인)** | 지식iN 데이터 소스 제안, API 크롤링 구현 |
| 라벨링 | GPT-4 자동 라벨링, AI Hub 감정 태그 라벨링 |
| 모델링 | KLUE/BERT fine-tuning, Whisper STT 연동 |
| 배포 | Gradio 구현, HuggingFace Space 배포 |

---

## 한계 및 개선 방향

- 56명 학생 데이터로 학습 → 일반화 성능 부족
- 이질적 출처 두 개 혼합 학습 → 단일 출처 데이터 필요
- 음성 데이터 라벨링이 AI 모델 기반 → 전문가 라벨링 필요
- 비언어적 요소(억양, 속도) 미반영
