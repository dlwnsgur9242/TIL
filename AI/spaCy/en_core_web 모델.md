# en_core_web 모델

spaCy에서 제공하는 영어 모델은 작업의 정확도와 처리 속도에 따라 선택할 수 있습니다. en_core_web_sm은 빠르고 가볍지만, 더 좋은 성능을 원하는 경우 아래 모델을 고려해볼 수 있습니다.

## 1. en_core_web_sm
    +   크기
        -   약 10MB

    +   장점
        -   가볍고 빠른 모델.
        -   토큰화, 품사 태깅, 개체명 인식 등의 기본 NLP 작업에 적합.
        -   빠른 속도를 요구하는 애플리케이션에서 사용 가능.

    +   제한점
        -   워드 벡터가 포함되지 않아 단어 간 유사도 계산 기능이 제한적.
        -   문맥 이해 및 정밀도가 비교적 낮음.

    +   사용 추천
        -   경량 애플리케이션.
        -   NLP 학습 및 프로토타이핑.
        -   대규모 모델이 필요하지 않은 간단한 작업.

    +   설치
        -   python -m spacy download en_core_web_sm

## 2. en_core_web_md
    +   크기
        -   약 40MB
    
    +   장점
        -   중간 크기의 워드 벡터를 포함.
        -   en_core_web_sm보다 더 정밀한 결과 제공.
        -   문맥 기반 단어 유사도 계산 가능.
    
    +   사용 추천
        -   중간 규모의 애플리케이션이나 더 나은 성능이 필요한 경우.
    
    +   설치
        -   python -m spacy download en_core_web_md

## 3. en_core_web_lg
    +   크기 
        -   약 700MB
    
    +   장점
        -   대규모의 정교한 워드 벡터 포함.
        -   가장 높은 정확도 제공.
        -   복잡한 자연어 처리 작업에 적합.
    
    +   사용 추천
        -   대규모 데이터셋 또는 높은 정확도가 요구되는 작업.
    
    +   설치
        -   python -m spacy download en_core_web_lg

## 4. transformer 기반 모델
    +   예시
        -   en_core_web_trf
    +   크기
        -   약 500MB 이상 (BERT 기반)
    +   장점
        -   최신 트랜스포머 아키텍처 사용.
        -   문맥을 깊이 이해하며, 고난이도의 NLP 작업에 탁월.
        -   문장 내 복잡한 관계를 잘 파악.
    +   사용 추천
        -   최상의 정확도를 요구하는 연구 또는 고급 애플리케이션.
    +   설치
        -   python -m spacy download en_core_web_trf

<br>

### en_core_web 모델 별 비교
![alt text](../imgs/en_core_web%20모델.PNG)
<br>

### 추천
+   빠른 작업: en_core_web_sm
+   중간 수준: en_core_web_md
+   최고 성능: en_core_web_trf
+   트랜스포머 모델(en_core_web_trf)은 속도가 느리지만, 매우 정확하므로 최신 모델 성능이 필요한 작업에 적합합니다. 