## 1. 랙 컴퓨팅 PoC 구조
* 자체 개발 메모리 서버, NVMe 스토리지 서버를 포함한 컴퓨팅, GPU HW 자원 풀 구성
* 자원풀은 100G 급 네트워크로 연결되며, 자원풀을 운영하기 위한 관리 SW 구성

![PoC_rev](/Data/image/02/01.png)

<랙컴퓨팅PoC 구조도>



## 2. 랙 컴퓨팅 HW 개발


### A. 스토리지 서버 개발 플랫폼
* L-Shape 형태의 KN-H620 서버보드 사용
* Intel Xeon Scalable Processor 지원
* 24개의 NVMe SSD 지원
* Omni-Path 지원 100G NIC 장착


### B. 스토리지 서버 개발 보드 종류 및 규격
* PCIe Switch 보드

![PCIe Switch](/Data/image/02/02.png)


<PCIe Switch 보드>

   - Microsemi Switchtec PM8546B-FEI 
   - PCIe Gen3 x24 Uplink, x72 Downlink 지원
   - Microsemi Switchtec PM8532B-F3EI 
   - PCIe Gen3 x8 Uplink, x24 Downlink 지원
   - MiniSAS HD Connector 8개 장착
   - PCIe Gen3 x16, x8, x8 Uplink 지원
   - SAMTEC ERM8 Highspeed Connector 5개 장착 
   - PCIe Downlink, PCIe clock, Sideband signal Interface

* NVMe Disk Backplane 보드

![NVMe Disk Backplane](/Data/image/02/03.png)


<NVMe Disk Backplane 보드>

   - SFF-8639 Connector x24 개 장착
   - NVMe SSD 24Bay 지원
   - SAMTEC ERF8 Highspeed Connector 5개 장착
   - PCIe Downlink, PCIe clock, Sideband signal Interface

* x16 PCIe Interface 보드

![x16 PCIe Interface](/Data/image/02/04.png)

<x16 PCIe Interface 보드>

   - MiniSAS HD 1x1 Connector 4개 장착
   - PCIe Gen3 x16 Uplink 지원

* x8 PCIe Interface 보드

![x8 PCIe Interface](/Data/image/02/05.png)


<x8 PCIe Interface 보드>

   - MiniSAS HD 1x1 Connector 2개 장착
   - PCIe Gen3 x8 Uplink 지원


### C. 스토리지 서버 시스템 구조 및 규격

![NVMe SSD](/Data/image/02/06.png)

<스토리지 서버 시스템 구조>

   - NVMe 스토리지 서버는 랙 컴퓨팅 시스템에서 Storage Resource 풀을 구성하는 시스템으로 외부와는 패브릭 네트워크 및 관리 네트워크로 연결되어 있으며 내부 NVMe 스토리지는 PCIe 스위치로 확장되어 Storage 자원을 제공한다.  


<스토리지 서버 시스템 규격>

|항목|규격|
|:----------:|:---------------------------------:|
|프로세서|2x LGA3647 (Socket P) processor sockets<br>- Intel Xeon Scalable Processor 지원
|메모리|24x DDR4 DIMMs(12x NV-DIMMs)- 프로세서당 6 개 채널 지원- DDR4 RDIMM/LRDIMM 지원- 2133/2400/2666 MT/s 지원
|칩셋||Intel C624 칩셋
|저장장치|24x NVMe SSD
|이더넷 포트|2x 1Gbps 이더넷 포트(RJ45 Type)
|PCI Express 슬롯|2x PCIe Gen3 x24 Riser (up to PCIe x8x8x8 3슬롯, x16x8 2슬롯 optional)<br>1x PCIe Gen3 x12 LP-Riser (up to PCIe x8x4 2슬롯) - optional
|비디오 포트|1x VGA 포트(외부), 1x VGA Pin-Header(내부)
|USB 포트|USB 포트<br>3x USB3.0 포트(외부),<br>1x USB3.0 Pin-Header(내부), 1x USB2.0 Pin-Header(내부)
|시리얼포트|1x 시리얼 콘솔 포트
|관리포트|1x IPMI 포트(RJ45 Type)
|System FAN|6x System FAN 



## 3. 랙 컴퓨팅 SW 개발

### A. SW 개발 영역
|**기능 변경점**|**-**|**인텔 RSD 2.3**|**인텔 RSD 2.5**|**2019 구현**|**2020 구현**|
|:-:|:--:|:--:|:-:|:-:|:-:|
|Redfish|-|V1.1.0|V1.6.1|-|-|
|PSME|FPGA over Fabric|Supported|Supported|미지원|지원|
|    |Optance Memory|Not supported|Supported|미지원|지원|
|    |SPDK<br>(Storage Performace<br>Development Kit)|Not supported|Supported<br>(Redfish/Swordfish)|미지원|지원|
|    |iSCSI|System level|System level|미지원|지원|
|    |Native Linux Strage|System level|Fabric level support|미지원|지원|
|    |Compute Node 변경|네트워크, FPGA,<br>스토리지|Accelerator, memory<br>모듈추가|미지원|지원|
|    |스토리지 노드|Swordfish|Swordfish|지원|지원|
|    |Compute Log|Not supported|Supported|미지원|지원|
|PODM|HA|Openstack<br>모듈이용|Kubernetis 모듈을<br>이용한 구현|지원|지원|
|    |Kubernetis|선택적 이용|기본 구성|지원|지원|
|    |Virtualization|VM 기반|Docker 기반|지원|지원|
|    |AAA|Not supported|Supported|지원|지원|


### B. SW 개발 환경과 버전
• SW 아키텍처 구성도

![arch](/Data/image/02/07.png)

<아키텍처 구성도>

• 기능설명
  * Cluster Manager : 클러스터 자원들의 통합 관리용 오케스트레이션 API를 제공
      * Message Queue(RabbitMQ)를 통한 제어 모듈들에 Event 방식으로 상호 연결되어서 처리되어 있음.
      * 각 제어 모듈은 Micro Service 형태로 구현되어 기능적인 확장이 용이함.

![cm](/Data/image/02/08.png)

<Cluster Manager 구성도> 

  * PODM : 포드 관리자는 포드의 각 랙 내 모든 리소스를 검색하고 기록하며 상위 오케스트레이션 계층의 요청에 따라 시스템을 구성함
      * 사용 가능한 리소스를 요청한 구성에 따라 PODM은 PSME에게 필요한 작업 (스위치 매개 변수 설정, IP 주소 매핑, 네임 스페이스 및 스토리지 볼륨 생성 등)을 수행하도록 요청하고 오케스트레이션 계층에 정보를 반환함
      * 작성된 시스템에 프로비저닝 및 워크로드 분배를 수행 함

![PDOM struct ARCH](/Data/image/02/09.png)

<PODM(v2.5) 내부 구성도> 

  * PSME : 시스템 관리 엔진으로 각 리소스 모듈 제어 기능과 각 리소스 모듈의 상호 연결
      * 각 블레이드, 각 섀시, 각 드로어 또는 전체 랙에 대한 하나의 구성 요소로 실행될 수 있도록 구현
      * 스토리지 볼륨 생성 등과 같은 구성을 지원하는 데 필요한 기능을 제공하는 PSME 소프트웨어 구성 요소가 포함 되어 있음

![PSME module ARCH](/Data/image/02/10.png)

 <PSME Module 구성도>

  * RMM : 각 랙에는 RMM이 있으며 이는 PSME 및 PODM와 통신하고 다양한 랙 기능을 수행
    * 랙 전원 및 냉각 관리, 환경 및 건강 상태보고, 랙 내 각 자산의 물리적 위치 지정 및 보고가 포함되어 있음

• RSD 사용 이점</span>
   - 더 빠르고 쉬운 확장
   - 응용 프로그램 개발, 프로비저닝 및 수명주기 관리의 민첩성 향상
   - 높은 활용도, 오버 프로비저닝 감소 및 동적 워크로드 튜닝을 통한 리소스 효율성
   - 가속기(FPGA)를 포함한 맞춤형 구성을 통한 최적화 된 성능
   - capex와 opex를 모두 절약하여 새로 고침 비용 절감
   - 자동화 된 인프라 관리로 효율적인 사용 제공

|구분|개발환경|
|:-:|:-:|
|PSME server & PODM agent|Ubuntu 16.04 LTS|
|                        |GCC compiler, java(Open JDK 1.8)|
|PODM|POSTSQL 11.5.0(doker)Spring boot 3.0|
||Ubuntu Server 16.04|
||Python 3.4|
|Debian pkg|isc-dhcp-server|
||Openssh-server|
||Python3(already preinstalled on Ubuntu 16.04.1)|
||tftpd-hpa|
||ntp|
||vlan|
||acl|
|클라우드 관리자|K8s|
|PSME URL|https://github.com/moca-etri/psme/ https://github.com/moca-etri/psme|
|PODM URL|https://github.com/intel/intelRSD/tree/master/PODM/SW/ https://github.com/intel/intelRSD/tree/master/PODM/SW/|


|개발영역|내용|
|:-:|:-:|
|PSME server & PODM agent|PSME RMM agnet|
||PSME Compute agent|
||PSME Chassis agent|
||PSME Network agent|
||PSME Storage agent|
||PSME PNC agent|
||PSME NVMe Target agent|
||PSME NVMe Discovery agent|
||PSME Compute Simulator agent|
|PSME Server|PSME REST Server|
|PODM|POD Manager|
|클라우드 관리자|K8s|


### C. 구현 및 테스트
* Dynamic Server Cluster 증가
* On-Demand Server Cluster 복제 및 추가 구성 제공
* Kubernetes기반 클라우드 연동 기능 제공
