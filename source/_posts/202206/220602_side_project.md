---
title: 220602 종합 프로젝트 전 빅데이터 개념 종합정리
date: 2022-06-02 17:51:00
tags:
  - Bigdata
  - Hadoop
  - Data-Engineer-Projects
categories:
  - Side-project
# hidden: true
# secret: true
---

<div align="center">
  <img src="/images/post_images/220602_bigdata.jpeg" alt="Bigdata">
</div>

<br/>
<br/>

이번 포스팅에서는 `빅데이터 구축의 각 단계를 6V관점에서 살펴보고, 중요 개념과 사용되는 상세 기술에 대한 내용을 정리`하려고 한다. 사이드 프로젝트를 진행하면서 중간에 개념을 한 번 정리하는 이유는 데이터 파이프라인 구축에 있어, 요즘 AWS EMR이라는 관리형 서비스를 사용해서 손쉽게 하둡의 에코 시스템을 사용(`단 7분이면 하둡의 에코 시스템을 사용`)하고, 직접 전반적인 서비스들을 통합해서 직접 프로젝트를 진행하지 않았기 때문에 뭔가 개념적으로 정리가 되지 않은 것 같다.
그래서 이번 기회에 빅데이터의 전반적인 개념에서부터 전체적인 하둡 에코 시스템을 구성하고 있는 서비스들을 활용해서 사이드 프로젝트를 진행해보고, 좀 더 체계적으로 개념과 응용적인 부분에 대해서 정리해보려고 한다.

<!-- more -->

## <ins><b>빅데이터</b></ins>

요즘에는 데이터가 대량으로 쏟아지고 있기 때문에 빅데이터라는 개념은 우리 일상속에 쉽게 찾아 볼 수 있는 개념이다. 2020년도의 전세계적인 데이터 성장률을 살펴보면, 80%이상의 데이터 성장은 비정형 데이터(Machine data, Social media, VoIP, Enterprise data)로 구성이 되어있다. 과거에는 이러한 대량의 데이터들을 적재하고 분석하는 부분에 대한 기술이 부족했기 때문에 그냥 버리는 경우가 많았는데, 요즘에는 과거로부터 현 시점까지 쌓인 데이터를 분석해서 현재의 문제점을 이해하고, 데이터로부터 해결하는데 사용되는 통찰력을 얻기도 한다.

현재의 문제점을 해결하기 위한 통찰력 이외에도 데이터로부터 다양한 패턴들을 해석해서 미래를 예측하기 시작했으며, 조직의 중요한 의사결정에 빅데이터가 많이 사용되고 있다.

## <ins><b>3V + 2V = 1V</b></ins>

이전 포스팅에서는 Big Data 4V라는 개념에 대해서 정리를 했었는데, 기본 3V(Volume, Variety, Velocity) + 2V(Veracity(진실성), Visualization(시각화))이 있으며, 그 결과로 새로운 Value(가치)가 창출된다고 하여, `6V`로 정의된다고 한다.
2V(Veracity, Visualization)은 IBM에서 추가된 개념으로, 이 6V는 빅데이터의 기획, 설계, 분석, 운영에서 사용되는 매우 중요한 개념이다.

- ### **[ DL & DW ]**
- `Volume` : 방대한 양의 데이터(TB, PB 이상)
- `Variety` : 정형(DBMS, 전문) + 비정형(SNS, 동영상, 사진, 음성, 텍스트 등)
- `Velocity` : 실시간으로 생산이 되며, 빠른 속도로 데이터를 처리/분석

- ### **[ DM ]**
- `Veracity` : 주요 의사결정을 위해 데이터의 품질과 신뢰성 확보
  (`상품/서비스, 고객/마케팅, 리스크 관리 이 세가지 활용영역으로 DM가 만들어진다.`)

- ### **[ Insight - 데이터 분석가들의 영역 ]**
- `Visualization` : 복잡한 대규모 데이터를 시각적으로 표현

- ### **[ Business ]**
- `Value` : 비즈니스 효익을 실현하기 위해 궁극적인 가치를 창출

전 세계적으로 `방대한 크기`의 `다양한 데이터`들이 `빠른 속도로 발생`하고 있으며, 주요 의사결정에 사용되는 데이터의 품질과 `신뢰성을 확보`하기 위해 데이터의 진실성은 중요하다.
이러한 데이터를 분석하고, `시각화`함으로써 새로운 효익을 가져다 줄 `가치를 창출`한다.

## <ins><b>빅데이터의 목적</b></ins>

사람이 기술과 대량의 데이터를 활용해서 빅데이터 시스템을 통해 과거의 현상에 대한 원인을 발견하고 그 원인을 통해 현재의 상황을 이해하고, 더 나아가 미래의 결과를 예측하는 한다.
이를 통해 의사결정을 위한 인사이트를 발견하고 적용함으로써, `"비용 절감", "수익 창출", "문제 해결"`이라는 효과를 낼 수 있다.

## <ins><b>빅데이터 인사이트의 이해</b></ins>

빅데이터의 인사이트는 `현상에 대한 이해, 발견, 그리고 예측`이라는 인사이트로 구분이 된다.
`이해 인사이트`는 시계열별 회원 가입 추이와 같은 `대규모 데이터의 통계를 통한 이해`를 말하며, 매출이 증가/감소한 원인과 같은 `발생한 현상`에 대해 이해하는 것을 `발견 인사이트`, 부도 위험이 있는 고객과 같은 `발생하지 않은 현상에 대해 예측`을 하는`예측 인사이트`이 있다.
마지막의 예측 인사이트는 ML/DL과 같이 예측 모델을 만들고 현상을 예측하는 등과 같은 높은 기술 수준이 요구된다.

## <ins><b>빅데이터 시스템 vs AI 시스템</b></ins>

AI 시스템은 빅데이터 시스템과 분리된 형태로 존재한다.
빅데이터가 AI에 대한 학습 데이터에 대해서 부담을 줄여주고 있다. (보완관계)

`빅데이터 시스템 = (DL -> DW -> AI 관련 DM)` -> `AI 시스템 (AI 개발/학습 -> 머신러닝 및 딥러닝)`

## <ins><b>빅데이터 관련 업무</b></ins>

빅데이터 관련 업무는 크게 세 가지로 구분이 되는데, `플랫폼 구축형 프로젝트`, `빅데이터 분석 프로젝트`, `빅데이터 운영 프로젝트`로 구분된다. 실제 회사에서 업무를 하게 되면, 이 세 가지 중에서 한 가지를 받게 된다.

`(1) 플랫폼 구축형 프로젝트`는 규모에 따라서 차이는 있지만 보통 3~6개월 정도의 기간동안 진행된다. 전형적인 빅데이터 SI 구축형 사업과 관련이 있으며, 빅데이터의 하드웨어와 소프트웨어를 설치하고 구성하는 것을 메인으로 한다.
(`수집 -> 적재 -> 처리 -> 탐색 -> 분석의 기능을 구현한다.`)
수 년간 쌓인 데이터를 마이그레이션하고, 간단한 지표를 알아내거나 고급 분석을 한다.

세부 파트 구성은 플랫폼 Part(설치 및 구성), 전처리 Part(수집 및 적재), 후처리 Part(처리, 탐색, 분석)으로 크게 구성하며, 규모에 따라 다르지만, 각 파트당 최소 3명이상 투입한다.

PM은 기술형 PM을 포니셔닝하며, 이유는 기술적 이슈가 발생했을때 대응해야되기 때문이다.

`(2) 빅데이터 분석 프로젝트`는 1~3개월 일정으로 진행된다. `단기간에 성과를 내려면 안되기 때문에 장시간에 거쳐 시행착오를 많이 겪어야 완성도가 높은 데이터 결과`를 뽑아낼 수 있다. 위의 플랫폼 구축이 완료된 후에 수행하며, 빅데이터 탐색으로 데이터의 이해가 높아질 때 시간한다.
분석 주제의 영역은 크게 세 가지로, 고객 분석을 통해 맞춤형 전략을 수립하는 "마케팅/고객, 신규 제품을 개발할때, 삼품의 가격 및 출시일을 결정할때 활용된다. 그리고 내/외부 리스크를 사전에 예측(경쟁사, 평판)할때 사용된다.

`(3) 빅데이터 운영 프로젝트`는 이미 구축이 완료된 플랫폼을 중/장기적으로 유지 관리한다. 대규모 하드웨어 및 소프트웨어로 운영되기 때문에 비용이 높으며, 각 빅데이터 분야별로 전문가 그룹이 확보되어야 한다.
빅데이터란 특정 업무 부서가 아닌 전사 시스템이기 때문에 여러 부서/업무 담당자들이 빅데이터 시스템에서 분석을 통해 서로 공유를 해야한다.
`필요한 프로세스 및 역할에 대해 정의가 필요`하며, 추가적으로 `데이터에 대한 표준화가 필요`하다. 이러한 전반적인 작업이 `빅데이터 거버넌스 체계를 수립`하는 과정이다.

## <ins><b>빅데이터 업무 분담</b></ins>

기업마다 다르지만, PM 아래에 `비즈니스`, `데이터 분석`, `데이터 엔지니어링` 이렇게 세 개의 조직으로 분리를 할 수도 있으며, `비즈니스 + 데이터 분석`, `데이터 분석 + 데이터 엔지니어링`으로 조직을 분리 할 수 있다.

## <ins><b>빅데이터 조직 구성(선진화된 빅데이터 시스템 도입)</b></ins>

빅데이터 관련 부서의 배치를 `빅데이터 플랫폼팀을 IT부서의 하위에 배치`하고, `빅데이터 분석을 담당하는 부서를 CEO 직할의 빅데이터 센터의 하위에 배치`함으로써 빅데이터 관련 거버넌스에 필요한 정책 및 표준을 하위의 다른 부서들에 내려주고 역할아래에 활용하도록 구성한다.

(`빅데이터 분석팀을 하위의 부서들에 공통으로 배치하게 되면, 각 부서별로 충돌이 발생할 가능성이 있다`)

## <ins><b>하둡(Hadoop)</b></ins>

하둡은 2005년 첫 등장을 하였고, 빅데이터 생태계에서 절대적인 영향력을 행사하고 있다. Cloudera, Hortonworks, MapR 등의 업체들이 Hadoop S/W를 중심으로 빅데이터 소프트웨어를 개발하고 공개하고 있다.

## <ins><b>빅데이터 구축 단계</b></ins>

빅데이터 구축 단계는 총 4개 단계로 구분할 수 있으며, `수집 -> 적재 -> 처리/탐색 -> 분석/응용`이다.

- ### **[ 수집 ]**

  - 실시간 데이터 수집 : CEP(Complex Event Processing) 기술 적용
    `ref.` CEP란 전통적인 RDB로는 실시간 데이터 처리 및 분석이 불가능하다는 문제를 해결하기 위한 솔루션
  - 대용량 데이터 수집 : ESP(Event Stream Processing) 기술 적용

  - 조직 내/외부로부터 데이터를 수집하는 단계로, 정형/비정형 데이터를 `크롤링 및 NLP 처리 기술`을 통해 취득한다. (블로그, 포털 등 뉴스 데이터는 비정형 처리 기술을 선택한다.)
  - Volume(상) : 대용량 데이터(TB 이상) 수집
  - Variety(상) : 정형/반정형/비정형 데이터 수집 (Log, RSS, XML, 파일, DB, HTML, 음성, 사진, 동영상)
  - Velocity(상) : 실시간 스트림 데이터를 수집한다.
    `(요건의 주요도에 따라서 최적화된 아키텍처를 구축한다.)`

  - #### **[대표 기술]**
    - `Flume` : 클라우데라에서 처음 개발된 기술로, 다양한 수집 요구 사항들을 해결하기 위해 다양한 기능으로 구성된 소프트웨어이다. 로그 데이터를 깔끔하게 수집하는데 가장 최적화되어있다. 많은 기업에서 실제 서비스 로그 데이터 관리를 위해 사용중이다.
    - `스톰` : 실시간 데이터를 병렬 프로세스로 처리하기 위한 소프트웨어, 데이터를 적재하기 전에 발생과 동시에 이벤트를 감지해서 처리하는 방식을 채택한다.
    - `에스퍼` : 스트리밍 데이터가 복잡한 이벤트 처리가 필요할 경우 사용되는 룰 엔진이다. 스톰은 실시간 데이터로부터 패턴을 찾고 패턴에 따라 이벤트를 처리하는데는 기능이 부족하다. 그런데 에스퍼는 실시간 발생 데이터간의 관계를 복합적으로 판단하고 처리하는 CEP(Complex Event Processing) 기능을 제공한다.
    - `Logstash`

- ### **[ 적재 ]**

  - 수집한 데이터를 필터링(정제)하여 데이터의 품질을 향상 시킨 후 빅데이터에 저장하는 과정이다. (`분산 스토리지에 영구/임시로 적재`)

  - ### **데이터 적재시 데이터의 종류에 따라 구분 처리**

    - **[대용량 파일]**

      - (1) 대용량 파일을 `영구 저장`하기 위해서는 `HDFS`에 적재

    - **[대규모 메시징 데이터]**

      - (1) 영구 저장시에는 NoSQL인 `HBase`, `MongoDB`, `Cassandra`에 적재
      - (2) 일부만 임시 저장할 때에는 In-Memory 캐시인 `Redis`, `RAMCache`, `인피니스팬(Infinispan)`에 적재
      - (3) 전체를 버퍼링하기 위해서는 MOM(Message Oriented Middleware)인 `Kafka`, `RabbitMQ`, `ActiveMQ`등을 활용

    위와같이 구분해서 저장하는 이유는 예를들어 실시간 및 대량으로 발생하는 데이터를 HDFS에 저장하게 되면, 파일 수가 기하급수적으로 증가하면서 관리 노드와 병렬 처리의 효율성이 낮아진다. 따라서 반드시 데이터의 성격별로 구분해서 저장해야한다.

    대량의 데이터가 적재될 때는 추가적인 전처리 작업이 발생한다. `전처리 작업은` 때로는 데이터의 크기와 요건에 따라 HDFS에 적재한 후에 처리하는 `후처리를 하기도 한다.`

    `ex)` 비정형 => 정형 데이터로 가공, 개인정보로 의심되는 데이터는 비식별 처리를 선행한다.

  - Volume(상) : 대용량 데이터(TB이상)를 적재, 대규모 메시지(1,000TPS 이상) 적재
  - Variety(중) : 정형/반정형/비정형 데이터를 적재
  - Velocity(상) : 실시간 스트림 데이터 적재
  - Veracity(상) : 데이터의 품질과 신뢰성을 확보해서 적재

- ### **[ 처리/탐색 ]**

  - 하둡 에코 시스템의 20여개 오픈소스 서비스를 사용한다.
  - Adhoc 쿼리로 데이터를 탐색/서택/변환/통합/축소 작업한다.

    - 내/외부의 정형/비정형 데이터를 결합함으로써 기존 기술적 한계로 만들지 못한 새로운 데이터셋을 생성한다.
    - 정기적으로 발생하는 처리/탐색 과정은 workflow로 프로세스화/자동화 한다.
    - workflow 작업이 끝나면, 데이터셋은 특화된 저장소(DM)로 이동하고, 데이터셋이 측정가능한 구조로 만들어지게 되면서 빅데이터 분석이 빠르고 편하게 된다.
    - 대용량 저장소에 적재된 데이터를 분석에 활용하기 위해서 `데이터를 정형화, 정규화`한다.
    - 탐색적 분석 : 데이터를 이해하기 위해 지속적인 관찰을 하며, 탐색결과를 정기적으로 구조화하는 과정을 수행한다.

  - #### **[대표 기술]**

    - 대표적인 기술로는 Hue/Hive/Spark/SQL 등을 사용한다.
    - 후처리 작업으로써 자동화하는 workflow 작업을 하게 되는데, 이때는 Oozie를 사용한다.

  - Volume(상) : 대용량 데이터(TB이상)에 대한 후처리 및 탐색
  - Veracity(상) : 데이터의 품질과 신뢰성을 확보하기 위한 후처리 및 탐색
  - Visualization(상) : 후처리된 데이터셋을 시각화해서 탐색
  - Value(중)

- ### **[ 분석/응용 ]**

  - 과거의 데이터로부터 문제의 원인을 찾아, 현재의 현상을 이해하고 개선한다. 인간의 힘으로는 찾기 힘든 `패턴들을 빅데이터 분석 기술로 찾아서 알고리즘화`하고, `미래 예측 분석 모델을 생성`해서 활용 영역에 따라 `통계, 데이터 마이닝, 텍스트 마이닝, 소셜 미디어 분석, 머신러닝/딥러닝 등 다양하게 분류`를 수행한다.
  - 대규모 데이터로부터 새로운 패턴을 찾고, 패턴을 해석함으로써 새로운 통찰력(insight)를 얻게 되는 과정이다.
  - 분석과정은 선형적 확장이 가능하며, 대규모 분산 환경을 낮은 비용으로 구축할 수 있다. 분산 환경 위에서 ML 구현(`기존 분석 기술의 한계를 극복`)
  - 파일 기반의 Batch 분석에서 수십배 빠른 In-Memory 기반의 분석기술이 빅데이터 생태계에서 빠르게 발전하고 있고, 그 활용범위도 점점 넓어져가고 있다.
  - 군집/분류/회귀/추천 등 고급 분석 영역까지 확장되고 있다.

  - #### **[대표 기술]**

    - Zeppelin, R, Tensorflow
    - 외부 RDBMS에 데이터를 제공하는 과정이 진행 (`Scoop`)

  (`분석/응용 단계에서는 모든 요소가 중요하다`)

  - Volume(상) : 대용량 데이터(TB이상) 분석
  - Variety(상) : 정형/반정형/비정형 등의 다양한 데이터 분석
  - Velocity(상) : 인메모리 기반으로 실시간 데이터 분석
  - Veracity(상) : 신뢰성 높은 분석 결과를 비즈니스에 적용
  - Visualization(상) : 분석 결과 및 창출된 가치를 시각화
  - Value(상) : 분석된 결과를 비즈니스에 적용해서 가치 창출

## <ins><b>빅데이터 보안</b></ins>

빅데이터에서의 보안은 일반 시스템에서도 적용되는 보안 요소들을 포함하고 있으며, 분야에 따라 다양한 보안요소들이 고려된다. 그 중 `데이터 보안`과 `접근제어 보안`에 빅데이터 만의 특징을 가지고 있다.

- **데이터 보안과 빅데이터의 발전**

  데이터 보안과 빅데이터의 발전은 서로 trade-off 관계에 있다.
  데이터 보안에서는 개인식별이 가능한 어떠한 정보도 수집하지 않는 것을 원칙으로 하나, 이러한 개인식별 정보들을 수집하지 못하면 의미가 없다.

  따라서 개인에서 기업의 정보보호를 위한 정책 및 기술들에 따라서 개인정보를 이름에서는 성을 제외한 이름을 \*, 거주지의 상세정보를 OO, 전화번호의 일부를 XXXX로 `마스킹하거나 통계처리, 삭제, 범주화하는 등의 비식별 처리 기술을 활용`한다.

- 위와같이 비식별 처리 기술을 활용해서 데이터를 처리하게 되면, 아래와 같은 문제점이 생긴다.

  - **(1) 개인정보 재식별화** : 데이터의 식별력이 높아지게 된다. (비식별 처리된 데이터에 새로운 카테고리의 데이터가 추가되면 식별력은 더욱 높아진다) 따라서 소속/유관기관과 국가별 법령에 따라 다르기 때문에 사내 법률팀과 확인이 필요하다.

  - **(2) 비식별화 + 대체키 활용** : 개인화 서비스 및 마케팅 분야에서 데이터 활용이 어려워진다. (`1:1 마케팅 및 신용정보 점수, 구매 이력에 따른 실시간 추천`)

    - 빅데이터 시스템에서는 수시로 변경되는 마케팅 등의 현황 관리가 어렵다. 이 문제에 대해서는 관련 시스템으로 짧은 주기로 데이터를 체크하고 수집 및 업데이트함으로써 해결할 수 있다.

    - 특정 개인을 타겟팅하기 위한 경우에는 고유값이 비식별화 처리되어 타겟 분석을 이용한 서비스 개발이 어렵다. 이 경우에는 `고객 관리 시스템에서 고유하게 발급하는 대체키를 활용해서, 빅데이터에 적재된 다른 데이터와 이 대체키를 결합해서 사용`하도록 한다.

    - 엄격한 보안 정책에 따라 대체키와 매핑된 개인정보를 조회/활용함으로써 마케팅팀과 영업팀, 리스크 관리팀에서는 데이터를 활용할 수 있게 된다.

## <ins><b>접근제어 보안</b></ins>

빅데이터 저장소에 저장된 개인정보, 거래정보, 행동이력을 보관하고 있는 경우, `ID/PASSWORD를 관리하는 인증 관리자`와 `인증된 계정에 역할과 권한을 부여하는 권한 관리자` 이 두가지가 취약하다. 따라서 안전하게 데이터를 제공하기 위해서는 Third party 접근제어 기술 관련 제품을 활용하여 이러한 취약점을 해결할 수 있다.

- **[아파치 녹스]**

  - 아파치 녹스는 DMZ 영역에 설치되며, 클라이언트와 하둡 에코 시스템의 직접적인 통신을 막는다. 클라이언트와 하둡 에코 시스템이 통신을 할 때에는 LDAP, KDC로부터 개인/권한 정보를 받아서 클라이언트는 하둡 에코 시스템과 통신한다.

- **[아파치 센트리 서버]**

  - 아파치 센트리 서버는 임팔라, 하이브 서버, 하둡 네임노드 등에 각 각 센트리 에이전트를 설치하고, 계정과 권한 정보를 통합관리하고 있는 Policy MetaStore로부터 접근제어의 계정 정보를 받아서 센트리 에이전트에서 사용해서 접근하도록 한다.

- **[아파치 레인지 서버]**

  - 아파치 센트리 서버와 유사한 구조로 되어있으며, 다른 점은 레인저 플러그인이 하이브 서버, HDFS, 스톰, HBase, 녹스에 각 각 설치되어있으며, Policy MetaStore로부터 접근제어의 계정 정보를 받아서 레인저 플러그인에서 사용해서 접근하도록 한다.

- **[커베로스]**

  - 커베로스는 매우 유명한 Third party 접근제어 보안 서비스이며, 클라이언트가 Kerberos KDC(Key Distribution Center)에 인증을 요청하고, 티켓을 획득하면, 해당 티켓으로 하둡 파일 시스템에 접근을 허용받아 접근하는 방식으로 동작한다.