# **메모리 중심 차세대 컴퓨팅 시스템 구조 연구**
## 개요
과학기술정보통신부의 지원  하에 ETRI(한국전자통신연구원) 고성능 컴퓨팅시스템 연구실에서는 "메모리 중심 차세대 컴퓨팅 시스템 구조 연구"(과제 기간: 2018. 04. 01. - 2025. 12. 31.)과제를 수행하고 있다. 인프라 자원의 고 확장성과 대규모 메모리에 대한 일관된 접근 방식을 제공하는 고속 연결망 기반의 메모리 중심 컴퓨팅 시스템 원천기술 개발을 위해 ETRI를 주관으로 KAIST, DIGST의 연구기관과 테라텍, 컴퓨팅 산업협회가 참여기관으로 연구 개발을 수행하고 있다.

## 프로세서 중심 컴퓨팅 메모리 병목 현상
지난 70년간 컴퓨터는 CPU와 메모리를 사용하여 컴퓨터를 구동하는 폰 노이만(Von Neumann) 구조를 사용하고 있으며, CPU 집적도 증가 및 고성능 CPU 아키텍처 적용을 통한 컴퓨팅 능력을 향상시키는 프로세서 중심 컴퓨팅(Processor Centric Computing)이 주류를 이루었다. 
프로세서 중심 컴퓨팅에서는 병렬처리를 위해서 다수 프로세서의 메모리 간, 그리고 각 메모리 계층 간의 데이터 이동이 필수적이다. 하지만, 빅데이터, AI, IoT 등의 대용량 데이터의 처리 시에 데이터 이동 문제가 더욱 심각해져, CPU의 처리속도가 아닌 데이터가 컴퓨팅 성능 및 에너지에 영향을 미치는 메모리 병목 현상을 야기시킨다. 아울러, 프로세서의 성능 개선만으로는 전체 시스템 성능 향상에 기여하는 것은 물리적으로 한계가 존재한다. 
즉, 메모리가 DIMM 소켓 형태의 CPU 핀에 연결되는 형상에서 대규모 데이터 처리를 위한 메모리의 확장은 CPU의 핀수 및 DDR 채널수 등이 물리적으로 제한됨을 의미한다. 이로인하여 CPU 코어 당 메모리 대역폭은 계속 감소하고 있다.
![M1](/Data/image/00/01.png)


## 데이터센터 내 효율적 자원확장 한계

지금까지 수십 년 동안 데이터센터의 자원 단위로 CPU, 메모리, 저장장치 및 마더보드 등 하드웨어와 이를 관리하기 위한 OS가 구동되는 monolithic 서버를 사용해 왔다. 그러나, 데이터센터의 워크로드는 점점 다양해지며 데이터 크기 역시 가변적이다. 이에 자원 활용률 및 성능 측면에서 CPU와 메모리및 저장장치의 자원 균형이 적절한 monolithic 서버 시스템을 설계하는 것은 어렵다. 이와 같은 어려움으로 인하여 데이터 센터에서는 미래의 수요를 총족시킬 수 있는 충분한 서버 단위의 자원을 구축하는 것이 필요하다. 실제로, 최대 성능을 위한 초과 프로비저닝을 통해 자원을 배치한다. 이는 TCO 증가를 초래할 뿐만 아니라, 자원 활용률이나 최대 성능 대비 실제 사용되는 성능이 매우 낮은 경우가 많다.
![M2](/Data/image/00/02.png)

## MECA 과제 주요 연구내용
본 과제에서는 1단계로, CPU와 확장 메모리 간의 시스템 수준 통합을 위한 메모리 중심 컴퓨팅 시스템 기술로 고속 메모리 연결망 요소 기술, 메모리 중심 컴퓨팅 아키텍처 및 하드웨어 기술, 공유 메모리 운영관리 소프트웨어 기술을 개발한다. 랙 수준의 자원 풀 통합을 위한 랙 컴퓨팅 시스템 기술로 고속 I/O 연결망 요소 기술, 스토리지 풀 서버 기술, 랙 단위 동적 자원 관리 소프트웨어 기술을 개발한다.
2단계에는 확장 자원풀을 통합을 통한 물리 시스템의 한계를 극복하는 바운드리스 컴퓨팅 기술로 메모리-I/O 통합 연결망 기술 및 대규모 자원 운영관리 소프트웨어 기술을 개발한다.

## 참여기관 및 추진체계
현재 본 과제는 ETRI 초성능 컴퓨팅 연구본부 고성능 컴퓨팅시스템연구실에서 주관하며, [KAIST](https://jongse-park.github.io/), [DIGST](https://cas.dgist.ac.kr/)의 연구기관과 [테라텍](http://www.teratec.co.kr/), [한국컴퓨팅산업협회](http://k-cia.or.kr/)가 참여기관으로 연구 개발을 수행하고 있다. 
![M3](/Data/image/00/03.png)

## 관련 싸이트 링크

[CXL Consortium](https://www.computeexpresslink.org/)

[Chipsalliance](https://www.chipsalliance.org/)

[CCIX Consortium](https://www.ccixconsortium.com/)

[Gen-Z Consortium](http://genzconsortium.org/)

[OpenCAPI Consortium](https://opencapi.org/)

[dRedbox Project](http://www.dredbox.eu/about/)

## 공개 소프트웨어 활동
본 과제에서는 연구 개발 단계의 각 산출물 및 노하우 공유를 위해 공개 소프트웨어 개발 및 운영 방식에 기반한 오픈소스를 본 커뮤니티와 github에 공개한다.이를 통해, 국내 관련 업체들의 아이디어 수렴 및 공동 설계를 추진하고자 한다.본 과제의 공개 소프트웨어 개발 및 운영 방식과 오픈소스 활용시 고려할 사항은 [한국컴퓨팅산업협회문서](/Data/documents/Data/documents/Pledge.docx)에서 정리하였다. 아울러, 공개 소프트웨어 구동을 위한 하드웨어 보드는 한국컴퓨팅산업협회를 통하여 대여 가능하다. 현재까지의 공개 소프트웨어 정보는 다음 표와 같다.


|소스(컴포넌트)명|라이선스명|특허 유/무|SW분야|공개일정|
|:----------------------------------:|:----------------:|:------:|:--------:|:---------:|
|[MOCA 0.7 Hardware Device Driver](https://github.com/moca-etri/gzd0.7/)|GPL v2 라이선스|무|운영체제|공개완료|
|[MOCA 1.0 Hardware Device Driver](https://github.com/moca-etri/gzd1.0/)|GPL v2 라이선스|유|운영체제|2020 Q3|
|[PMDK 지원을 위한 MOCA-PMEM 리눅스 커널](https://github.com/moca-etri/pmdk/)|GPL v2 라이선스|유|운영체제|2020 Q3|
|MOCA 전역 memory management Software|자체 개발중|유|운영체제|2021 Q2|
|[PSME](https://github.com/moca-etri/psme/)|Apache License 2.0|무|시스템관리|공개완료|
|PODM|Apache License 2.0|무|시스템관리|2020 Q4|
|[L4fame Build Container execution environment](https://github.com/moca-etri/l4fame/)|GPL v2 라이선스|무|운영체제|공개완료

## 결과물
[메모리 연결망](/Researches/Memory-Network/Memory-Network.md)

[랙 컴퓨팅 PoC](/Researches/Rack_computing_PoC/Rack_computing_PoC.md)

[결과물 동영상](/Researches/Result_Video/Result_Video.md)

[홍보물](/Data/documents/br.pdf)


## 활용방안 및 기대효과
본 과제의 연구결과는 다음과 같이 활용될 전망이다.

* 데이터센터/클라우드 컴퓨팅
  - 랙 컴퓨팅 시스템 내에서 다양한 규모의 클라우드 서비스를 동시 지원 가능하여 비용 대비 최대 시너지 효과 기대
  - 자원 요구량이 다양한클라우드 서비스의 경우, 랙 컴퓨팅 시스템 내 자원을 동적 구성하여 다수의 웹서버 서비스 가능

* 빅데이터/지능정보/IoT 처리 시스템
  - 메모리 중심 컴퓨팅 시스템을 이용하여 빅데이터 분석을 위한 분산 처리 서비스 가능
  - IoT, 기계학습, 딥러닝의 고속 실시간 데이터 처리를 위한 대규모 메모리 풀 제공

* 고속 대규모 처리 시스템
  - 메모리 중심 컴퓨팅에 의한 스케일업이 가능할 뿐만 아니라 바운드리스 컴퓨팅에 의한 랙단위 수준으로 스케일아웃이 가능

## 참고문헌
1. [(OCP) Greg Casey, “GEN-Z:　High-performance interconnect for the data-centric future,” OCP Summit 2018](/Data/documents/OCP-GenZ-March-2018-final.pdf)
2. [(FSD) A. Klimovic, et al., “Flash Storage Disaggregation,” EuroSys’16, April 2016](/Data/documents/A._Klimovic,_et_al.,_“Flash_Storage_Disaggregation,”_EuroSys’16,_April_2016.pdf)
