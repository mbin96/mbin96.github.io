---
title: stereo vision을 이용해서 월드 좌표 얻기
tags: cv
---

  
카메라 한대에서 인트린식, 익스트린식 파라메터를 구해서 얻을수있는 좌표는 **카메라 좌표**에서 z 축이 없는 좌표.
여기에서 캘리브레이션을 진행해 얻을수 좌표는 캘리브레이션을 진행한 평면상에서의 **월드 좌표**. 이때, 해당 평면상 에서의 움직임만 알수있음 

우리가 원하는건 XYZ를 다 가진 월드좌표인데... 이러려면 **stereovision**을 사용해야함

# epipolar geometry
see https://en.wikipedia.org/wiki/Epipolar_geometry

기본적으로, stereovision은 [**epopolar geometry**](https://en.wikipedia.org/wiki/Epipolar_geometry)를 통해 얻게 됨. 픽셀좌표계에서의 시차를 이용해서 계산하는 방법. 사람눈이랑 비슷


![epipolar geometry](/img/2023-08-04/Epipolar_geometry.svg)

## epipole 혹은 epipolar point 
두 카메라 렌즈의 optical center(핀홀 모델에서의 핀홀) $O_L$과 $O_R$을 선분으로 이으면 현재 카메라와 상대 카메라의 이미지 평면중 각각 다른 한 지점에 투사되게 되어있음. 이점이 각각 $e_L$ 과 $e_R$ 임. 이를 epipole 혹은 epipolar point 라고 함.

## Epipolar line
왼쪽 카메라에서 봤을때, 선분 $\overline{\rm O_LX}$ 는 $O_L$을 포함한 직선이기에 이미지 상에서 점으로 보임. 하지만, 오른쪽 카메라에서 보면 $\overline{\rm e_RX_R}$ 선분으로 보이게 됨. 이 선분을 epipolar line 이라고 함. 이는 반대로도 마찬가지.
epipolar line 은 3차원 공간에서 점 $X$ 위치 함수임. X의 위치가 변하면, 왼쪽 카메라와 오른쪽 카메라 이미지 각각에서 epipolar line이 생성됨. 3차원 $\overline{\rm O_LX}$ 선분은 $O_L$을 지나가기 때문에, 오른쪽 카메라 이미지에서는 **반드시 $e_R$ 을 지나는 에피폴 라인이 생기게 될것.** 모든 epipolar line은 epipolar point를 포함하게 됨. 즉 epipolar point를 지나는 모든 선분은 epopolar line임 

## epopolar plane
점 $X, O_L, O_R$ 을 포함하는 평면을 epipolar plane이라고 함. epipolar plane은 카메라 이미지 평면과 접해서 epipolar line을 생성함. 모든 epipolar plane은 X의 위치와 상관없이 epipolar point와 epipolar line과 접함.

## epipolar constraint
점 $X$에 대해 각각 카메라의 이미지 평면상에 투영된 $X_L$, $X_R$ 이 있고, $e_R$을 알고있다고 가정하면, epipolar line 상에 $X_R$이 있어야 하는 제약이 생김. 이게 epipolar constraint. ray $\overrightarrow{O_LX_L}$  상의 모든 점은, 이 제약조건을 만족하게 됨. 이를 이용해서, $X_L$과 $X_R$이 동일한 3D 좌표상의 점인지를 확인할 수 있게 됨. epipolar constraint는 두 카메라 사이의 essential matrix와 fundamental matrix 로 설명될 수 있다.

### essential matrix
see https://en.wikipedia.org/wiki/Essential_matrix


핀홀카메라를 만족하는 스테레오 이미지에서 [동일점(corresponding points)](https://en.wikipedia.org/wiki/Correspondence_problem) 을 설면하는 $3 \times 3$ 매트릭스다. 
homogeneous **normalized image coordinates**(그러니까? image_rectification이 된???) 에 있는 두 이미지에 $y$와 $y'$점이 각각 존재하면
$$(y')^TEy=0$$ 
이면 동일한 3D 상의 point이다. 

TODO - 내용 추가하기

### fundamental matrix 
위의 essential matrix는 normalized image coordinates에서 적용되는 반면, fundamental matrix는 카메라 파라메터까지 포함 해서 실제 픽셀 좌표 사이의 기하학적 관계를 표현하는 행렬



## 삼각측량 triangulation
미안하다 이거하려고 어그로 끌었다

카메라 이미지 평면상에서 $X_L$과 $X_R$을 알아냈다면(descriptor 등으로 동일 물처의 점 찾기) $\overrightarrow{O_LX_L}$ 와 $\overrightarrow{O_RX_R}$ 프로젝션 ray도 알아낼 수 있다. 이 프로젝션 ray는 3D 좌표상의 한점인 $X$에서 교차하게 되어 삼각측량으로 좌표를 계산할수있게된다.


## 단순화
카메라 이미지 평면이 일치하면, epipolar geometry가 단순화됨. epipolar line $\overrightarrow{O_LX_L}$ 과 $\overrightarrow{O_RX_R}$이 일치하고, $\overline{\rm O_LO_R}$ 이랑 평행(parallel) 하게 된다. 즉, 점 $X$는 두 이미지에서 x축으로 평행 이동 하게 된다. 
카메라 이미지 평면이 일치 하지 않으면, 이미지를 변환 해서 일치하게 바꿔줄 수 있는데, 이를 위해서 하는게 [**image rectification**](https://en.wikipedia.org/wiki/Image_rectification) 이다.


