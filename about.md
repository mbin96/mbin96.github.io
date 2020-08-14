---
layout: article
titles: 조현종 
aside:
  toc: true

---


# 조현종
![](img/me.png){:.circle.shadow.image--lg 
    style="float: left; 
    margin-left: 0.5em; 
    margin-right: 2em"
    }


### 소개
임베디드 부터 딥러닝까지 많은 컴퓨터 공학 분야에 관심을 가지고 공부하는 학부생 입니다. 특히 최근에는 Computer Vision에 관심을 가지고, 영상처리, openCV, 딥러닝 등을 관심있게 공부하고 있습니다.  
임베디드 하드웨어와 소프트웨어를 다루며 익힌 **로우레벨 컴퓨터 지식, 영상처리 능력**과 **빠른 학습**, 다양한 리눅스 배포판을 써본 경험에서 오는 **리눅스 사용능력, 빌드환경 구축** 등이 강점입니다.

---
### Contact
- Mail : [mbin96@gmail.com](mailto://mbin96@gmail.com)
- Github : <https://github.com/mbin96/>
    
### Education
- 건국대학교 전기전자공학과 학부과정 재학중
  - 2014-03 ~ 2021-02(졸업예정) 

### Skills
- **C, C++** 
- **Python**
- Pytorch
- Java
- openCV
- arm, avr 임베디드 프로그래밍
- 리눅스, git 활용
  - 기본적인 터미널 명령어 활용과 gcc, MAKEFILE을 이용한 빌드환경 구축 등

---
# Project
### SuperResolution
![Super resolution network X4](/img/srnet_sample.png)
왼쪽이 원본이미지, 오른쪽이 SuperResolution x4 네트워크를 이용해 고해상도화 한 이미지
#### 개요
DeepLearning을 이용한 이미지 해상도 개선 프로젝트로서, Pytorch 프레임워크를 이용하여 개인 프로젝트로 수행하였습니다. 기존 모델에 새로운 아이디어를 추가하여 기존 모델을 개선하는 방식으로 이루어졌습니다.  

<details>
<summary><span style="color:red">더 읽어보기</span></summary>
<div markdown="1">

#### 특징
- 개인프로젝트
- PyTorch 사용
- 의료 영상 네트워크인 UNETPP를 베이스로 하여 CA, Back Projection등의 아이디어를 사용해 구성
  - UNETPP 네트워크는 이미지의 크기를 작게 변형하여 학습하기 때문에 Global feature을 학습하는데에 적합함 
    
![Super resolution network compatition](/img/srnet.png)
해당 네트워크는 격자 무늬와 같이 Global feature가 두드러지는 반복되는 패턴에서 좋은 결과를 보여주었습니다.

</div>
</details>

- Slide : [Link](https://1drv.ms/p/s!AvfXn2C0Rf2JhON2hb8XP4K9nC-qMg?e=Gv4geN)  
- 2020-01 ~ 2020-06  
    
    ---
  
### OOAD & UML toy project *(Object Oriented Analysis and Design)*
![](/img/ooad.png)
#### 개요
객체지향 언어의 협업 개발방법론을 익히기 위한 토이 프로젝트입니다. 알람, 세계시간, 타이머, 스탑워치등의 기능을 가진 시계를 구현하는것이 목표로, 개발시 **UML을 기반으로** 수행하였습니다. 현업에서의 개발 프로세스를 체험할 수 있었던 프로젝트로 **여러 인원과의 협업, UML 다이어그램을 활용한 개발 프로세스, 객체지향 개념 확립, git 사용** 등을 익혔습니다.

<details>
<summary><span style="color:red">더 읽어보기</span></summary>
<div markdown="1">
![](/img/ooad_use.png)
![](/img/ooad_class.png)
#### 특징
- 4인 팀 프로젝트
- 애자일 프로세스
- Planning, Analysis, Design, Implementation & Unit Test, System Testing 로 구성
- UML 다이어그램을 이용하여 UseCase, Sequence Diagram, 도메인 모델등 구성
- Implementation은 다음과 같은 환경에서 수행되었습니다.
  - Java8
  - Junit
  - Sonacube
  - Jenkins
  - Git
  - Notion (for Issue Tracking)
    
코로나 시국에 대면으로 프로젝트를 수행하는데 어려움이 있었으나, Microsoft Teams와 Git의 적극적인 활용으로 원격에서 효율적으로 협업하는 방식을 익힐 수 있었습니다. 4인이서 매일매일 teams를 사용해 할일을 나누고 그때그때 github에 커밋하며 진행하였습니다.   
평소 디자인에 관심이 많아 제가 UI 직접 디자인하였고, 사용자가 어떤버튼이 무슨일을 할지 예측 가능한 UX를 만들기 위해 팀원간에 많은 논의가 있었습니다. 
</div>
</details>


- Doc : [Link](https://drive.google.com/drive/folders/1poVJCUSLcbhl0wb8AXnfopp3gs7mR5UY?usp=sharing)
- Github : <https://github.com/mbin96/OOAD-project>
- 2020-04 ~ 2020-06  
    
    ---

### IP camera Solution on EMPOSIII Embedded board
![](/img/ipcam_pc.png)![](/img/ipcam_smart.png)
#### 개요
EMPOSIII 라는 arm11 프로세서를 사용하는 임베디드 보드 상에서 ip 카메라 솔루션을 구현하였습니다. 보드의 카메라 모듈에서 얻은 이미지를 실시간으로 웹브라우저에서 확인, 클라이언트 프로그램에서 녹화등이 가능합니다. **리눅스에서의 개발과 리눅스 시스템 이해, 로우레벨에서의 영상처리**에 많은 도움이 되었습니다.

<details>
<summary><span style="color:red">더 읽어보기</span></summary>
<div markdown="1">
#### 특징
- 3인 팀 프로젝트
- 서버 사이드 (EMPOSIII) 
  - 임베디드 리눅스 기반 
  - 카메라 모듈에서 RGB값을 받아오는 디바이스 드라이버
  - RGB raw 데이터를 전처리 하고 jpeg로 압축해 비디오 스트림으로 보내는 소켓 프로그래밍
  - 그외 jpeg 라이브러리등의 크로스컴파일
- 클라이언트 (x86)
  - openCV를 이용해 서버의 비디오 스트림을 이용해 얼굴감지, 움직임감지시 녹화 기능 구현.    
     
리눅스에 익숙한 사람이 조원 중 저 혼자고 다른 팀원은 리눅스가 처음이라 프로젝트를 진행하는데 어려움이 많았으나, 다른 조원과 많은 대화를 나누며 제가 아는것을 가르쳐 주고 서로 할수있는 영역을 잘 나누어 협업하였습니다.   
비디오 스트림으로 저성능 하드웨어에 알맞은 mjpeg를 사용하여 브라우저에서 볼 수 있게 하는 것이 목표 였는데, 인터넷상의 코드는 파이썬을 이용하는게 대부분이고 C를 이용한 코드가 없어서 소켓 프로그래밍으로 직접 구현했어야 했습니다. mjpeg mime가 제대로 서술된 문서가 없어 고생하였으나 포기하지않고 수 일간의 구글링과 테스트를 통해 mjpeg를 정확히 구현 하였습니다.
</div>
</details>
- Doc : [Link](https://github.com/mbin96/embedded_sys/blob/master/readme_report.pdf)
- Github : <https://github.com/mbin96/embedded_sys>
- 2019-11 ~ 2019-12  
   
    --- 

### Live Face AR Sticker
<video src="/img/horizen.mp4" loop="" autoplay="" muted="" width="400" ></video><video src="/img/port.mp4" loop="" autoplay="" muted="" width="400" ></video>   
#### 개요
Head Pose Estimation을 이용한 실시간 얼굴인식 AR 스티커 입니다. **OpenCV를 이용한 영상처리**와 Qt 라이브러리를 통한 Gui를 실습하였습니다.
<details>
<summary><span style="color:red">더 읽어보기</span></summary>
<div markdown="1">
#### 특징
- C++, OpenCV4, Qt5, [sdm Head Pose Estimation](https://github.com/chengzhengxin/sdm) 이용
- 위 영상과 같이 수직 수평에서 얼굴의 회전을 감지하고, 얼굴의 이마부분에만 정확하게 스티커를 합성
   
</div>
</details>
- Slide : [Link](https://docs.google.com/presentation/d/1sdEeZsQqIeRcD8_eaUN4hoxaBrsw8dIIm4W8ffJyLAw/edit?usp=sharing)
- 2019-12  
  
  ---

### Camera Image Preprocessing for AlexNet
#### 개요
건국대학교 SoC Design 랩에 학부 연구생으로 근무하며 진행한 프로젝트입니다. 임베디드 보드에서 카메라 이미지를 인터럽트로 가져와 AlexNet에 맞게 전처리하고, AlexNet의 Classification 결과를 시리얼로 확인할수 있게 하였습니다. **arm 프로세서에 대한 이해, 특히 amba bus에 대해 깊게 학습** 하였습니다.
<details>
<summary><span style="color:red">더 읽어보기</span></summary>
<div markdown="1">
#### 특징
- Xilinx Zybo 보드 사용
- 카메라 모듈 데이터를 AlexNet에 맞춰 크롭, 리사이즈, 노말라이즈 등 전처리 작업 수행
- hdmi를 통해 해당 인풋 이미지를 확인하고, AlexNet의 결과를 시리얼로 출력
</div>
</details>
- 2019-07 ~ 2019-08  
    
    ---
    
### CNN Optimization for Embedded System
#### 개요
임베디드 Xilinx Zybo 보드에서 CNN의 연산을 microprocesor에 최적화하는 프로젝트 입니다. microprocessor의 캐시와 레지스터를 고려하여 최대한 빠른 연산이 가능하도록 unrolling, tiling등의 코드 최적화와 Neon 등의 기법을 이용하였습니다. 연산 시간이 AlexNet기준 4400ms에서 550ms 정도로 약 8배가량 감소하였습니다. **SIMD나 어셈블리와 같은 로우레벨 컴퓨터에 대한 이해와 실제 구동에 대해** 자세히 알게 되었습니다.
- 2019-06