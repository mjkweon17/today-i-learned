### Pinecone
- Pinecone은 고성능 AI 애플리케이션을 위한 장기 메모리를 제공하기 쉽게 만드는 관리형, 클라우드 기반 벡터 데이터베이스
- 단순한 API와 인프라 문제 없이 낮은 지연 시간으로 신선하고 필터링된 쿼리 결과를 수십억 개의 벡터 규모로 제공
- 벡터 데이터베이스는 전통적인 스칼라 기반 데이터베이스가 부족한 벡터 임베딩의 저장과 쿼리를 최적화하여 제공하는 것이 특징
- 이는 기계 학습 애플리케이션에서 벡터 기반의 개인화, 랭킹, 검색 시스템을 정확하고 빠르며 확장 가능하게 구축할 수 있도록 도움

### RAG
- https://www.youtube.com/watch?v=m7cNjCVpSrw
- Retreival Augumented Generation
- 질문 -> 내 데이터 저장소 -> AI 언어 모델 -> 답변
    - 내 데이터 저장소: 기존 DB 형식, 벡터 DB, 스프레드 시트
    - AI 언어 모델: GPT, Claude, Palm2, 네이버 하이퍼클로바 등
- 프로세스
    1. 사용자 질문
    2. 질문을 이용해 저장소에서 검색
    3. 지시 프롬포트 + 질문 + 검색 결과 n개 > 언어모델(GPT)에게 제공
    4. 언어 모델이 답변 생성
    5. 답변 출력
- RAG 구조
    - 질문 & 내 데이터 -> 임베딩 AI 모델 -> 벡터 DB(저장소) -> 사용자 질문 + 검색결과 n개(Top k = n) -> AI 언어 모델 -> 답변
    - 임베딩 AI 모델: OpenAI text-embedding-ada-002
- RAG 구성 요소
    1. 문서 또는 데이터 가공
        - 현존하는 대부분의 문서 양식 또는 데이터 사용 가능
        - 문서 또는 데이터를 반드시 나누어야 한다
            - 나누는 이유
                - 언어 모델 및 임베딩 모델 토큰 크기(토큰은 언어 모델에게 전송하고 처리하는 단위) (예: 하드디스크 512MB와 유사한 개념)
                - 기대하는 답변의 성격 또는 형식에 따라 나누는 기준을 정할 수도 있다.
                - 문서나 데이터의 현재 형식: 구조화된 문서냐 구조가 일관성 없는 문서 등을 고려해서 나누기도 함
            - 내용의 주제 기준을 나누는 예: 문서 제목, 제목, 부제목, 주제, 내용
            - 하나의 묶음으로 나누자: 문서가 다수의 페이지거나 유사한 문서가 여러 개일 때 나누어 처리시, 나누어진 내용만 보아도 구분이 되거나 연결이 되어야 하는 경우, 언어 모델이 파편적인 정보를 접하더라도 이해력이 높아져 더 정확한 답변 생성
    2. 임베딩
        - 임베딩은 글자, 단어, 문장을 분류하는 것
            - 모든 과일에는 '과일'이라는 스티커가 붙고, 모든 장난감에는 '장난감'이라는 스티커를 붙이는 것
            - 임베딩은 전용 AI 모델을 이용해 스티커 대신 숫자를 붙이는 것
            - 즉 숫자들이 서로 가까울수록 서로의 거리가 가까워서 자연스럽게 분류가 됨
    3. 임베딩 모델
        - AI가 사람의 언어를 이해하기 위한 방법으로 숫자로 변환해주는 역할을 하는 AI 모델
        - 임베딩 모델의 성능은 RAG 챗봇 만들 때 매우 중요
        - 임베딩 모델을 지정된 차워 수를 가지고 있고, 현재 가장 많이 사용하는 모델은 OpenAI의 Ada모델(text-embedding-ada-002)
            - 24년 1월 말에 text-embedding-3-large가 생김
    4. 벡터 데이터베이스
        - 벡터 데이터베시는 과일 상자 또는 장난감 상자
            - 장난감을 주제, 크기, 색깔별로 나워서 상자에 넣듯이
            - 임베딩 모델을 이용해 붙은 숫자를 이용하여 벡터라는 조각으로 나누어 저장
        - 문장도 벡터화해서 저장하면 하나의 벡터 좌표를 차지함
        - 문서 또는 데이터를 나눈 기준으로 하나의 벡터 위치를 차지
        - 질문도 임베딩 모델을 통해 벡터화
        - Top k
    5. 프롬포트
        - 기본적인 프롬포트의 역할
            - 잘문 _ 검색 결과(n=2) + 지시
        - 다양한 고급 프롬포트 기술로 답변 품질 크게 개선 가능
        