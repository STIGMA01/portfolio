# 백엔드 개발자로서 무엇을 경험했는지...

<br>

## 소개
STIGMA의 포트폴리오 공간입니다.

<br>

## 목차
- [경력 및 업무 경험](#-경력-및-업무-경험)
- [기술 스택](#-기술-스택)
- [주요 프로젝트](#-주요-프로젝트)
- [연락처](#-연락처)


----
<br>

## 💻 경력 및 업무 경험

> [!NOTE]
> 개인 프로젝트가 아닌 업무적인 연관성이 깊은 내용은 소스코드나 구체적인 내용 등을 게재하지 않았습니다.

<br> 

### 1. 백엔드 개발 | 자연어 처리(NLP) 솔루션 기업 <sub> **2024. 02. ~ 2024. 12.**</sub>
![NLP](https://img.shields.io/badge/NLP-Machine%20Learning-blue?style=flat-square)
<p>
  <img src="https://cdn.simpleicons.org/python/3776AB" height="24" />
  <img src="https://cdn.simpleicons.org/django/092E20" height="24" />
  <img src="https://cdn.simpleicons.org/flask/000000" height="24" />
  <img src="https://cdn.simpleicons.org/neo4j/008CC1" height="24" />
  <img src="https://cdn.simpleicons.org/mariadb/003545" height="24" />
  <img src="https://cdn.simpleicons.org/splunk/003545" height="24" />
  <img src="https://cdn.simpleicons.org/html5/E34F26" height="24" />
  <img src="https://cdn.simpleicons.org/css/1572B6" height="24" />
  <img src="https://cdn.simpleicons.org/bootstrap/1572B6" height="24" />
  <img src="https://cdn.simpleicons.org/docker/2496ED" height="24" />
</p>

1) **전자 문서에 대한 NLP 처리 및 핵심 솔루션 개발**
    - `Python` 언어 처리 라이브러리 및 솔루션 알고리즘을 통한 자연어 처리 및 문서 프로세싱 코드 개발
    - 내부 웹(Web)과 백엔드 처리와의 연동을 위한 프론트엔드 개발자와 협업 및 `Flask API` 도입
    - 대량의 데이터 처리를 위해 멀티 프로세스 적용
    - `MariaDB` 쿼리 조작 및 기본적인 사용
    - `Cypher Query(Neo4j)`를 통한 문장/토큰 데이터 관련 솔루션 모듈 개발
    - 한국어 구조와 문법을 이해하고 자연어 처리 모듈 내 알고리즘 적용
  
2) **상용 웹페이지 개발**
    - `Django` 프레임워크에 대한 유지보수 및 페이지 개발
    - 웹페이지 디자인 개선 및 UI 개발 `(Bootstrap5)`
    - SEO 개선 및 홈페이지 게시판, 관리자 관리 기능 등 개발

    2-2. **핵심 크롤러 및 데이터 수집**
    - 자연어 데이터 처리 및 수집/분석을 위한 `Splunk DB` 유지보수
 
3) **백엔드 API 개발**
    - `Django Rest Framework`를 통한 솔루션 패키지 및 모듈들에 대한 백엔드 서비스 API 개발
    - `Celery`, `Redis` 등을 통해 `Cpu Bound`의 `Heavy Task`에 대한 처리 구현

    <details>
      <summary>Architecture</summary>
      <img width="904" height="677" alt="NLP Service" src="https://github.com/user-attachments/assets/4a374d96-d188-4077-aa93-0e0c8085f897" />
    </details>

4) **Docker 환경 구성**
    - `Docker` 환경 생성 및 유지보수를 통해 실제 서비스 구성 및 구축

<br>

----


### 2. [1인 개발] 경량 웹 서비스 개발 | 영상 자막 등 언어 데이터에 대한 사용자 작업 서비스 구축 <sub> **2025. 06. ~ ...**</sub>
<p>
  <img src="https://cdn.simpleicons.org/python/3776AB" height="24" />
  <img src="https://cdn.simpleicons.org/django/092E20" height="24" />
  <img src="https://cdn.simpleicons.org/neo4j/008CC1" height="24" />
  <img src="https://cdn.simpleicons.org/nginx/008CC1" height="24" />
  <img src="https://cdn.simpleicons.org/streamlit/008CC1" height="24" />
  <img src="https://cdn.simpleicons.org/docker/2496ED" height="24" />
</p>

<img width="740" height="360" alt="자막 말뭉치 처리 서비스" src="https://github.com/user-attachments/assets/8b726484-eb9d-4059-835c-fb61e55f40a6" />


1) **`Django REST framework`를 기반으로 백엔드 API 구축**
    <details>
     <summary>API 명세서 (예시)</summary>
     <img width="800" height="265" alt="image" src="https://github.com/user-attachments/assets/c8489ea8-dc74-485d-aa32-1eb4e066e8e9" />
    </details>
     
    - **Neo4j에 대한 CURD 작업 등을 위한 API 개발**
      > 성능과 업데이트에 대한 우려가 있지만, Neo4j Engine 주력으로 `Py2Neo`를 사용하기로 했습니다.
      > 또한 `graphene`나 `neomodel` 등 외부 라이브러리는 사용하지 못했고, dataclass로 순수하게 스키마 모델 부문을 만들고, Service 레이어를 만들었습니다.
      <details>
       <summary>[Example.1] DRF의 API 뷰</summary>
        
       ```python
       
       class CorpusUploadView(GenericAPIView): 
           parser_classes = [MultiPartParser, FormParser] 
           renderer_classes = [JSONRenderer, BrowsableAPIRenderer] 
           serializer_class = CorpusSRTUploadSerializer
       
           def get_queryset(self):
               return None
       
           @handle_exceptions_drf
           def post(self, request, *args, **kwargs):
               serializer = self.get_serializer(data=request.data)
               serializer.is_valid(raise_exception=True)
       
               data = serializer.validated_data.copy()
               content = data.pop("srt_file").read().decode("utf-8")
       
               service = SubtitleCorpusNeoService()
               result = service.create_corpus_from_srt_data(
                   srt_content=content,
                   **data
               )
       
               if result:
                   response_data = {
                       "message": "Corpus and sentences uploaded successfully.",
                   }
                   response_data['result'] = dict(result)
                   return Response(response_data, status=status.HTTP_200_OK)
               else:
                   return Response({"message": "No sentences parsed, corpus not created."}, status=status.HTTP_200_OK)
  
      ```
       
      </details>
    
1) **1인 개발임을 감안하며, 내부망 서비스임을 착안해 `Streamlit`을 이용한 빠른 프론트엔드 구축**
     - `Streamlit`을 통해 자막 데이터 CRUD 및 편집 UI/기능 개발.
     - 내부 API 상호작용 모듈 개발.
  
        <details>
        <summary>[Example.1] API 호출 클라이언트 부문 개발 </summary>
  
        프론트에서 백엔드 API를 호출할 때 사용할 기본적인 클라이언트를 만들었습니다.
  
        ```python
        class CorpusAPIClient(BaseAPIClient):
            ENDPOINTS = {
                'list': DRF_ENDPOINT_NODES_LIST,
                'create': DRF_ENDPOINT_CORPUS_UPLOAD,
                'retrieve': DRF_ENDPOINT_CORPUS_DETAIL,
                'destroy': DRF_ENDPOINT_CORPUS_DETAIL,
            }
            # 'update', 'partial_update'
            
            @handle_api_errors
            def get_corpus_list(self):
                return self.get('list', path_vars={'node_label': 'Corpus'})
        
            @handle_api_errors
            def get_corpus_sentences(self, corpus_id: str):
                return self.get('retrieve', path_vars={'corpus_id': corpus_id})
        
            @handle_api_errors
            def upload_corpus(self, corpus_upload_req: CorpusUploadRequestModel):
                print(corpus_upload_req)
                file_field_key = 'srt_file'
                files = corpus_upload_req.srt_file.to_request_file(field_key=file_field_key)
                data = corpus_upload_req.to_dict(drop_null=True,
                                                 exclude_fields=[file_field_key])
                return self.post('create', data=data, files=files)
        
            @handle_api_errors
            def delete_corpus(self, corpus_id: str):
                res = self.delete('destroy', path_vars={'corpus_id': corpus_id})
                if res.status_code == 204:
                    return {"message": f"Completed delete: {corpus_id}"}
                elif res.content:
                    return res.json()
                else:
                    return {"message": f"Status: {res.status_code}, No response body"}
  
        ```
        </details>
  
        <details>
        <summary>[Example.2] API 호출/수신시 스키마 모델화</summary>
  
        프론트에서 API를 호출할 때, 유지보수와 정합성을 고려하면 스키마를 모델화하여 처리하는 것이 필요하다고 판단하였습니다.
        또한 `Pydantic` 라이브러리가 아닌 가벼운 dataclass로 신속히 만드는 것을 채택했습니다.
        
        ```python
   
        from dataclasses import dataclass, asdict, fields
        from typing import Type, TypeVar, Any, Dict, Union, IO, Optional, List
        from .enums.enum import MimeType
        
        T = TypeVar('T', bound='BaseDataModel')
        
        
        @dataclass
        class BaseDataModel:
            def to_dict(self, drop_null: bool = True,
                        exclude_fields: Optional[List[str]] = None) -> dict:
                """
                데이터 모델을 딕셔너리로 변환한다.
        
                Args:
                    drop_null (bool, optional): None 값을 제거할지 여부. 기본값은 True이다.
                    exclude_fields (List[str], optional): 딕셔너리에서 제외할 필드 이름 목록. 기본값은 None이다.
                """
                result = asdict(self)
                
                def _filter(item):
                    key, value = item
                    if drop_null and value is None:
                        return False
                    if exclude_fields and key in exclude_fields:
                        return False
                    return True
        
                filtered_items = filter(_filter, result.items())
                return dict(filtered_items)
        
            @classmethod
            def from_dict(cls: Type[T], data: Dict) -> T:
                field_names = {f.name for f in fields(cls)}
                filtered_data = {k: v for k, v in data.items()
                                  if k in field_names}
                return cls(**filtered_data)
        ```
  
        ```python
   
        from dataclasses import dataclass, field
        from typing import Optional, List
        from .base import BaseDataModel, UploadFileModel
        
        
        @dataclass
        class CorpusUploadRequestModel(BaseDataModel):
            srt_file: UploadFileModel
            corpus_title: str
            corpus_subtitle: Optional[str] = None
            corpus_author: Optional[str] = None
            corpus_category: Optional[str] = None
            corpus_language: Optional[str] = None
            corpus_video_unique_id: Optional[str] = None
  
        ```
        </details>

        <details>
        <summary>[Example.3] 호출 함수</summary>
          
        ```python
        # Streamlit의 기능을 활용한 파일 업로드 부문
        
        with st.spinner("Wait..."):
            try:
                res_content = client.upload_corpus(
                    _ = CorpusUploadRequestModel(
                        srt_file=UploadFileModel(
                            name=uploaded_file.name,
                            content=uploaded_file.getvalue(),
                            content_type=uploaded_file.type
                        ),
                        **detail_data
                    )
                )
                st.success("File upload completed successfully.")
                # st.write("**Test Response:**")
                # st.json(res_content)
                st.cache_data.clear()
            except Exception as e:
                st.error(f"A temporary error occurred. Please try again later. [code: 033]")
                logger.error(f"Clientside error: {e}")
        
        ```
          
        </details>
        
      - 빠른 프로토타입 제공에 최적화된 Streamlit 활용
        <details>
          <summary>개발 모드 실행</summary>
          <img width="800" height="75" alt="image" src="https://github.com/user-attachments/assets/63f24b61-bb36-4416-bf1c-62d5b6eb2a8a" />

        </details>

2) **언어 데이터 특성상 관계형 데이터베이스 사용을 착안해 `GraphDB` 구축**
     - 관계형 DB를 통해 문장과 문장간의 연결, 문장과 특수 태그들과의 연결로서 `지식 그래프`와 같은 아키텍쳐 구성
       <details>
         <summary>[Example.1] 노드 데이터</summary>
         <img width="800" height="290" alt="image" src="https://github.com/user-attachments/assets/3be777c8-cace-4142-af68-baf7113c34aa" />
  
       </details>

3) **`Docker`를 통해 빠른 배포, 쉬운 운영 환경 구성**
    - 도커 환경으로 빠른 Prototype과 운영 환경 구축.
    <details>
    <summary>[Example.1] Neo4j Dockerfile 구성으로 빠르게 Neo4j DB 구축</summary>
      
    ```Dockerfile
    FROM neo4j:5.20
    ARG APOC_VERSION=5.20.0
    
    ENV NEO4J_HOME=/var/lib/neo4j
    
    RUN apt-get update && apt-get install -y --no-install-recommends wget \
        && rm -rf /var/lib/apt/lists/*
    
    RUN wget --no-check-certificate \
        https://github.com/neo4j-contrib/neo4j-apoc-procedures/releases/download/${APOC_VERSION}/apoc-${APOC_VERSION}-extended.jar \
        -O ${NEO4J_HOME}/plugins/apoc-${APOC_VERSION}-extended.jar
    
    ENV NEO4J_PLUGINS='["apoc"]'
    ```
    </details>


#### Overview
  <details>
    <summary>폴더 구조</summary>
    <img width="900" height="463" alt="image" src="https://github.com/user-attachments/assets/0c987379-ea5a-45a7-b7e4-4f0c2246cc31" />
    
  </details>


----

<br>

## 🛠 기술 스택

| 분야        | 숙련  |             기술 |
|-------------|------|--------------------|
| 언어        | `★★★☆`  | ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white) |
| 백엔드      | `★★☆☆`  | ![Django](https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=django&logoColor=white) ![DRF](https://img.shields.io/badge/Django%20REST%20API-FF1709?style=for-the-badge&logo=django&logoColor=white) ![Celery](https://img.shields.io/badge/Celery-37814A?style=for-the-badge&logo=celery&logoColor=white) ![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)|
| 프론트엔드  | `★★☆☆` | ![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white) ![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white) ![CSS3](https://img.shields.io/badge/CSS-1572B6?style=for-the-badge&logo=css&logoColor=white) |  
| 데이터베이스  | `★☆☆☆` | ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white) ![Neo4j](https://img.shields.io/badge/Neo4j-008CC1?style=for-the-badge&logo=neo4j&logoColor=white) ![MariaDB](https://img.shields.io/badge/MariaDB-003545?style=for-the-badge&logo=mariadb&logoColor=white) |
| 운영환경   | `★★☆☆` | ![Gunicorn](https://img.shields.io/badge/Gunicorn-499848?style=for-the-badge&logo=gunicorn&logoColor=white) ![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white)   |
| 기타       | `★★☆☆`  |  ![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white) | 




<br>

## 📂 주요 프로젝트

> [!NOTE]
> To be written as soon as possible...

---

<br>

## 📞 연락처

- GitHub: [github.com/STIGMA01](https://github.com/STIGMA01)
- Email: stigma_19121@naver.com

---

> Backend Development History


