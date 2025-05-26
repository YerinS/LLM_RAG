# 📚 PDF QA with LangChain & Qdrant Vector DB

## 개요
이 리포지토리는 PDF 문서에서 텍스트를 추출하고, 구조화된 메타데이터와 함께 LangChain을 활용해 문서 검색 및 질문 답변(QA) 시스템을 구현한 예제입니다.  
Qdrant 벡터 데이터베이스를 사용해 임베딩 기반 검색을 수행합니다.

---

## 주요 기능
- PDF 페이지별 header/footer 제거 (상단/하단 각 10%)
- 대목차/중목차/소목차별 문서 청크 분리 및 메타데이터 저장
- 표 등 비정형 요소 추출(추후 추가 예정)
- Qdrant 벡터DB를 활용한 유사도 검색
- LangChain `load_qa_chain`으로 질문에 대한 답변 생성

---

## 사용법

### 1. 환경 세팅
- Python 3.8 이상 권장
- 주요 라이브러리 설치

```bash
pip install langchain langchain_openai qdrant-client pdfplumber openai
```

### 2. PDF 전처리 및 문서 분리
- pdfplumber로 페이지별 텍스트 추출
- header/footer 제거를 위한 crop 적용 (상단/하단 각 10%)
- 대목차/중목차/소목차 기준으로 문서 청크 생성
- 각 청크에 페이지 번호 포함한 메타데이터 저장

### 3. Qdrant 벡터 DB 구축 및 검색
- 문서 임베딩(OpenAI Embeddings) 생성 후 Qdrant에 저장
- 임베딩 기반 유사도 검색 수행
- 유사도 점수 0.4 이상 필터링 및 결과 출력

### 4. LangChain QA 체인 실행
- load_qa_chain(chain_type="stuff") 로 QA 체인 생성
- invoke 메서드로 input_documents와 question 입력하여 답변 생성

---

## 예시 출력

❓ 질문: What is 'Chain of Thought(CoT)' in prompt engineering?

💡 답변: 'Chain of Thought' refers to a prompting technique where...

---

## 파일 구성
|파일명|설명|
|---|---|
|RAG_Qdrant.ipynb|PDF 처리 및 QA 예제 Jupyter 노트북|
|PromptEngineering.pdf|테스트용 PDF 문서|

---

## 참고 사항
- Qdrant 도커 컨테이너가 로컬에서 실행 중이어야 합니다 (localhost:6333)
- OpenAI API 키 환경 변수 설정 필요 (OPENAI_API_KEY)

---

## 추가 개선 사항
- 표 및 그래프, 도식 자동 추출 기능 보완
- 검색 결과 랭킹 및 필터링 고도화
- 대화형 QA 기능 및 UI 확장
