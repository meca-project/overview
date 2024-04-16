## 1. 메모리연결망 구조
* 컴퓨팅 서버와 다수의 메모리 모듈을 포함한 메모리 풀의 분리 구조를 지향
* CPU 및 메모리 모듈과의 인터페이스를 위한 front-end bridge 및 back-end bridge와 스위치로 구성
* 메모리 연결망 프로토콜은 Gen-Z 0.7, 1.0 스펙을 준수
* CPU와 연동을 위한 별도의 device driver에서 바이트 단위, 블록 단위 접근 가능

![w](/Data/image/01/memory1.png)

![w2](/Data/image/01/memory2.png)

<메모리연결망 하드웨어 상세구조>



![w3](/Data/image/01/memory3.png)

<메모리연결망 레이어별 고도화>


![w4](/Data/image/01/memory4.png)

<메모리연결망 스위치 구조>



![w5](/Data/image/01/memory5.png)

<메모리 중심 컴퓨팅 소프트웨어 개요>



* OpenFAM, FS-DAX, PMDK를 사용한 mmap direct access 구현
* gRPC를 사용한 컨터이너간 고속 통신 프로토콜 구현(컨테이너간 스케일 문제의 안정성 확보, HTTP/2 트랜스포트 계층 사용)
* 다중 컨테이너 기반 메모리 액세스 모델 구축
* 브로커 컨테이너를 통한 메모리 할당 및 해제 제어 구조 구현(메모리 풀 access control 구현)
* 컨테이너 브로커를 사용한 Gen-Z 메모리 Pool Manager구현으로 인한 컨테이너 수준 안정성 확보
* 다중 APP의 접근 제한 모델

![w6](/Data/image/01/memory6.png)

<Gen-Z 메모리 풀 관리 SW>

![w6](/Data/image/01/memory6.png)

<확장메모리 풀>

## 2. 개발 환경
### A. 메모리 연결망 HW/SW 개발용 테스트 완료된 플랫폼
* 테스트 베드 1 : [HPE DL380 Gen 10 서버](https://www.hpe.com/kr/ko/product-catalog/servers/proliant-servers/pip.models.hpe-proliant-dl380-gen10-server.1010026818.html/)
* 테스트 베드 2 : [Dell R730 서버](https://www.dell.com/ko-kr/work/shop/povw/poweredge-r730/)
* 테스트 베드 3 : [AMD RYZEN Threadripper 기반 서버](https://www.amd.com/ko/products/ryzen-threadripper/)

### B. 메모리 연결망 HW/SW 개발보드 종류 및 규격
* Bittware XUPP3R 개발 보드

![w7](/Data/image/01/memory7.png)

<Bittware 개발 보드>

   - Xilinx xcvu9p-flgb2014-2-e FPGA 장착
   - 4 DDR4 RDIMM 슬롯지원, PCIe Gen3 x16 지원
     [제품정보](http://www.bittware.com/fpga/xup-p3r/)


* AlphaData 개발 보드

![w8](/Data/image/01/memory8.png)

<AlphaData 개발 보드>

   - Xilinx Kintex&reg; UltraScale&trade; XCKU115-2 - FLVA1517E
   - 6x PCI Express Gen3 x8 cores
   - 16GB DDR4 내장메모리
     [제품정보](https://www.alpha-data.com/dcp/products.php?product=adm-pcie-8k5/)

## 3. 메모리 연결망 HW Device Driver
<개발 SW 사양 및 툴체인 버전>
|SW| 버전 및 사양|
|:---------:|:-------------------------------------:|
|부트로더<br>(UEFI BIOS)|DELL R730 & HPE DL380 Gen10 UEFI BIOS Firmware<br>- Dell UEFI BIOS<br>- HPE UEFI BIOS
|커널|Kernel 4.4.XXX기반<br>- native kernel 4.4.0-169-generic
|root file system|- x86_64 Ubuntu 16.04 LTS<br>- x86_64 Ubuntu 18.04 LTS<br>- x86_64 Ubuntu 19.04 LTS
|Device driver|- [Gen-Z 0.7 Hardware Device Driver](https://github.com/moca-etri/Gen-Z-0.7-Hardware-Device-Driver/)<br>- [Gen-Z 1.0 Hardware Device Driver](https://github.com/moca-etri/Gen-Z-1.0-Hardware-Device-Driver/)<br>- gzd-5.0 지원예정
|DKMS<br>(Dynamic kernel Module Support)|- ver 2.2.0.3
|Native compiler<br>(GCC)|- x86_64-linux-gnu<br>- gcc 5.4.0(20160609)


## 4.구현 및 테스트
* Gen-Z 1.0 스펙 SystemVerilog RTL 코드 및 FPGA 구현
* PCIe 메모리 영역 64GB, 512GB, 1TB 할당 및 가용성 테스트
* Block, character, mmap 등 다양한 입출력 인터페이스 제공
* Gen-Z 스위치 및 Gen-Z 메모리 풀 구현중 (100G 네트워크, 4.5TB 메모리/섀시 규모)
