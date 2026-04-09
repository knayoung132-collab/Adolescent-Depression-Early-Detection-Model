# 😔 Adolescent Depression Early Detection Model

**Accuracy 84.6% / F1 84.6% / AUC 0.96**

An NLP pipeline that detects depression in adolescents by combining Naver KnowledgeIN text data with AI Hub youth voice data, using KLUE/BERT fine-tuning and Whisper STT.

[▶ Live Demo](https://ireneminhee-depression-detector.hf.space)

---

## My Contributions *(4-person team)*

| Area | What I did |
|------|------------|
| **Project Architecture** | Designed overall data pipeline strategy, defined depression labeling criteria, architected training workflow for heterogeneous data integration |
| **Data Strategy** | Determined how to combine two different data sources (crawled text + voice), designed GPT-4 auto-labeling pipeline based on expert answers and context |
| **Model Design** | Selected KLUE/BERT-base for Korean NLP, designed transfer learning approach for binary depression classification |
| **Training Design** | Defined train/val/test split strategy, selected evaluation metrics, designed sentence-level prediction pipeline |

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

## Key Design Decisions

**Why two data sources?**
KnowledgeIN provides expert-validated text on depression, while AI Hub provides real adolescent voice patterns. Combining both improves coverage of how depression actually manifests in language.

**Why GPT-4 for labeling?**
Manual labeling of 8,000+ posts was infeasible. GPT-4 was prompted with expert answers and context to replicate clinical judgment at scale.

**Why KLUE/BERT?**
Pre-trained on Korean corpus with strong performance on Korean NLP benchmarks. Transfer learning allowed effective fine-tuning with limited labeled data.

**Why fear/sadness/anger as depression signals?**
Based on clinical literature linking these emotions to depressive episodes in adolescents.

---

## Dataset

| Source | Description | Size |
|--------|-------------|------|
| Naver KnowledgeIN | Q&A with expert answers on student depression | ~8,000 posts |
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
| **프로젝트 설계** | 전체 데이터 파이프라인 전략 수립, 우울감 라벨링 기준 정의, 이종 데이터 통합 방식 결정 |
| **데이터 전략** | 텍스트·음성 두 데이터 소스 통합 방식 설계, GPT-4 자동 라벨링 파이프라인 기획 |
| **모델 설계** | 한국어 NLP에 최적화된 KLUE/BERT 선정, Transfer Learning 기반 이진 분류 접근법 설계 |
| **학습 설계** | 학습/검증/테스트 분리 전략 수립, 평가 지표 선정, 문장 단위 예측 파이프라인 설계 |

---

## 설계 의사결정 근거

**왜 두 개의 데이터를 결합했나?**
지식iN은 전문가 검증 텍스트를, AI Hub는 실제 청소년 음성 패턴을 제공합니다. 두 데이터를 결합해 우울감이 언어에서 나타나는 다양한 방식을 커버했습니다.

**왜 GPT-4로 라벨링했나?**
8,000건 이상의 수동 라벨링은 현실적으로 불가능했습니다. 전문가 답변과 문맥을 프롬프트에 포함시켜 임상적 판단을 대규모로 재현했습니다.

**왜 KLUE/BERT를 선택했나?**
한국어 말뭉치로 사전 학습되어 한국어 NLP 벤치마크에서 우수한 성능을 보이며, 제한된 라벨 데이터에서도 Transfer Learning으로 효과적인 fine-tuning이 가능합니다.

**왜 두려움·슬픔·분노를 우울감 지표로 정의했나?**
청소년 우울 삽화와 이 감정들의 연관성을 다룬 임상 문헌을 근거로 기준을 수립했습니다.

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
| **프로젝트 설계 (본인)** | 데이터 구성 전략, 학습 파이프라인 설계, 이종 데이터 통합 방식 결정 |
| 데이터 수집 | AI Hub 음성 데이터 전처리 및 라벨링 구현 |
| EDA | 감정 유형별 분석, Word Cloud |
| 서비스 배포 | Gradio 구현, HuggingFace Space 배포 |

---

## 한계 및 개선 방향

- 56명 학생 데이터로 학습 → 일반화 성능 부족
- 이질적 출처 두 개 혼합 학습 → 단일 출처 데이터 필요
- 음성 데이터 라벨링이 AI 모델 기반 → 전문가 라벨링 필요
- 비언어적 요소(억양, 속도) 미반영
